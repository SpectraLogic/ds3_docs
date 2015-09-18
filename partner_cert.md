Client Partner Certification Process
====================================

* Need overview of BP interactions (architecture diagram and API calls
  used)
* Tests
  * Single Large object (100GB or greater so that a single file will be chunked) (This could be set smaller so that they could use 20MB instead of 100GB)
  * 1,000 objects of various sizes (1KB to 1GB)
  * Try to retrieve an object that doesn't exist in Black Pearl
  * If the customer has requirements where they need to know when an object is fully persisted by using the job polling or using notifications
  * Resuming a job where a connection has failed when doing a object PUT
  * Access Black Pearl with invalid credentials
  * Access a bucket that the user does not have access to (PUTs and GETs)
  * Listing all the objects in a bucket or at least setting the `max_keys` property on S3 GetBucket call to force the request to paginate
  * Doing a Bulk GET on an object not in BlackPearl cache (in 1.2 this means a server restart, in 2.4 we can use the cache reclaim api)
  * Cache full events - a client only has to do one or the other depending what which method they are using:
    * Test cache full events when using GetAvailableChunks (either by using an intermediate proxy or artificially limit the cache size)
    * Test cache full events when using naked S3 PUTs (this can be simulated as well)
