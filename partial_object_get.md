Partial Object Recovery
=======================

## S3 Clients

Standard S3 clients can use the regular [Amazon S3 Partial Object GET](http://docs.aws.amazon.com/AmazonS3/latest/API/RESTObjectGET.html#ExampleGetRangeRequestHeaders)
for objects that only consist of a single blob.

## DS3 Clients

DS3 clients can add an offset and length to the object list when
starting a bulk get job. Clients may specify multiple ranges within the
same object.

In the example below, we're fetching two ranges within the same object.
Note that when we put the object, we configured the default blob size to
10MiB rather than 100GiB.

###### Request

    PUT http://192.168.56.103:8080/_rest_/bucket/bucket-name?operation=start_bulk_get HTTP/1.1 
    Date: Tue, 20 Jan 2015 17:33:25 GMT 
    Authorization: AWS c3BlY3RyYQ==:35U60mIiJ4eEE5uJYP/7tGStIcE= 
    Naming-Convention: s3 
    Content-Length: 222
    Proxy-Connection: Keep-Alive 
    User-Agent: Jakarta Commons-HttpClient/3.1 
    Host: 192.168.56.103:8080 
    
    
    <Objects ChunkClientProcessingOrderGuarantee="NONE">
        <Object Name="dir5/file1.dat" Offset="1048576" Length="5242880" />
        <Object Name="dir5/file1.dat" Offset="7340032" Length="5242880" />
    </Objects>

###### Response

    HTTP/1.1 200 OK
    Server: Apache-Coyote/1.1
    RequestHandler-Version: 1.30BEC24B83CC2C896865E83E25E3B82F
    Content-Type: text/xml;charset=UTF-8
    Content-Language: en
    Content-Length: 1507
    Date: Tue, 20 Jan 2015 17:54:34 GMT
    
    
    <MasterObjectList
            BucketName="bucket-name"
            CachedSizeInBytes="0"
            ChunkClientProcessingOrderGuarantee="NONE"
            CompletedSizeInBytes="0"
            JobId="5e9f9371-59cb-46ba-8ca9-cea650a5da61"
            OriginalSizeInBytes="20971520"
            Priority="HIGH"
            RequestType="GET"
            StartDate="2015-01-20T17:54:34.000Z"
            UserId="e2fab710-f285-4aed-9eb3-1d75a7256fbc"
            UserName="spectra"
            WriteOptimization="CAPACITY">
        <Nodes>
            <Node
                    EndPoint="10.0.2.15"
                    HttpPort="8080"
                    HttpsPort="443"
                    Id="f7e68137-a013-11e4-bc5b-080027d0a940"/>
        </Nodes>
        <Objects
                ChunkId="bfa77b2e-24e8-487a-ab09-45f5351b9c1a"
                ChunkNumber="0"
                NodeId="f7e68137-a013-11e4-bc5b-080027d0a940">
            <Object
                    InCache="true"
                    Length="10485760"
                    Name="dir5/file1.dat"
                    Offset="0"/>
        </Objects>
        <Objects
                ChunkId="d90fe41d-f9fe-48ad-96ec-dc23ee939d6f"
                ChunkNumber="1"
                NodeId="f7e68137-a013-11e4-bc5b-080027d0a940">
            <Object
                    InCache="true"
                    Length="10485760"
                    Name="dir5/file1.dat"
                    Offset="10485760"/>
        </Objects>
    </MasterObjectList>

The response above does not contain what you probably expect. It does *not*
list the same offsets and lengths that we requested but rather a server-defined
list of ranges that include all of the ranges that we requested.

For each <Object> node, the client must perform exactly one GET Object request
with the `offset` and `job` query string parameters and optionally a
standard
HTTP `Range` header.

Here's a simple diagram for this example:

                     0
    Client requests: | +-+ +---+
    Full Object:     +--------------------+
    Server returns:  +------+------+

The rest of this document assumes that the `<Object..../>` nodes
represent data
in cache. In practice you will have to run the "get chunks available for
client
processing" request just as you would in a regular DS3 bulk GET
operation to
determine which object ranges are in cache and which are not.

To retrieve the data we want, we can perform the following GET Object
requests:

##### Request

    GET http://192.168.56.103:8080/bucket-name/dir5/file1.dat?job=5e9f9371-59cb-46ba-8ca9-cea650a5da61&offset=0 HTTP/1.1
    Date: Tue, 20 Jan 2015 17:54:35 GMT
    Authorization: AWS c3BlY3RyYQ==:deJX+Fs9vG9LFteyGymNkgd/rfs=
    Range: bytes=1048576-6291455,7340032-10485759
    Naming-Convention: s3
    User-Agent: Jakarta Commons-HttpClient/3.1
    Host: 192.168.56.103:8080
    
    

##### Response

    HTTP/1.1 206 Partial Content
    Server: Apache-Coyote/1.1
    RequestHandler-Version: 1.0A842389520F0E213B1ABFF420A4779C
    x-amz-request-id: 184
    ETag: "7f7dd758fe0f30e1e6c277cbf050f6b6-6"
    Content-Range: bytes 1048576-6291455,7340032-10485759/53026319
    Accept-Ranges: bytes
    Content-MD5: YoSrJEAxt2QJrYoucYDLqg==
    Content-Language: en
    Content-Length: 8388608
    Date: Tue, 20 Jan 2015 17:54:34 GMT
    
    
    *object contents*

Here's our diagram again. The last line demonstrates the parts of the
object
that we are retrieving during this request.

                         0
    Client requests:     | +-+ +---+
    Full Object:         +--------------------+
    Server returns:      +------+------+
    GET Object Request:    +-+ ++

This is a standard S3 GET Object request, with the following DS3
specific parameters:

* The `job=5e9f9371-59cb-46ba-8ca9-cea650a5da61` query string parameter
  specifies which DS3 job this GET request belongs to.
* The `offset=0` query string parameter specifies the offset that the
  server specified in its first `<Object.../>` node.
* The `Range: bytes=1048576-6291455,7340032-10485759` header specifies the
  object ranges that the client needs within the range that the server
  provided.
  * While the DS3 `<Object.../>` elements specify byte ranges in terms
    of offsets and lengths, these HTTP ranges specify inclusive start and end
    byte offsets within the object.
  * The client specifies two ranges in this case.  Remember that in our example
    the client requests two ranges within the same object. The first originally
    requested range falls entirely within the first range returned by the
    server. The second originally requested range overlaps both the first and
    the second range returned by the server. So when the client performs a GET
    Object request for the first range returned by the server, it must ask for
    the entire first requested range and the part of the second requested range
    that overlaps the first returned range.
  * These ranges must be within the range specified by the server, but the offsets
    are still relative to the entire object.

##### Request

    GET
http://192.168.56.103:8080/bucket-name/dir5/file1.dat?job=5e9f9371-59cb-46ba-8ca9-cea650a5da61&offset=10485760
HTTP/1.1
    Date: Tue, 20 Jan 2015 17:54:35 GMT
    Authorization: AWS c3BlY3RyYQ==:deJX+Fs9vG9LFteyGymNkgd/rfs=
    Range: bytes=10485760-12582911
    Naming-Convention: s3
    User-Agent: Jakarta Commons-HttpClient/3.1
    Host: 192.168.56.103:8080
    
    

##### Response

    HTTP/1.1 206 Partial Content
    Server: Apache-Coyote/1.1
    RequestHandler-Version: 1.0A842389520F0E213B1ABFF420A4779C
    x-amz-request-id: 185
    ETag: "7f7dd758fe0f30e1e6c277cbf050f6b6-6"
    Content-Range: bytes 10485760-12582911/53026319
    Accept-Ranges: bytes
    Content-MD5: eyy7q5wQb0Azw9xtmHKIUQ==
    Content-Language: en
    Content-Length: 2097152
    Date: Tue, 20 Jan 2015 17:54:34 GMT
    
    
    *object contents*

This is again a standard S3 GET Object request, with additional DS3 specific
parameters. Note that this time we're only specifying one range, because we're
only retrieving the contents of the second requested range that overlap
the second range returned by the server.

Here's the diagram one last time. Again the last line demonstrates the
range
of data retrieved during this last GET Object request.

                         0
    Client requests:     | +-+ +---+
    Full Object:         +--------------------+
    Server returns:      +------+------+
    GET Object Request:         +--+

### Checksum Validation

DS3 manages end-to-end CRC by assigning one checksum to each "blob" of an
object. In order to verify the contents of a partial object GET, the client
must omit the Range header when requesting each blob. This means the client
will retrieve the entire contents of each blob even if the blobs contain more
data than the partial object ranges originally requested. It's still the
client's responsibility to figure out what data to save where.
