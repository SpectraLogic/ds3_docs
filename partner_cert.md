Client Partner Certification Process
====================================

* Need overview of BP interactions (architecture diagram and API calls
  used)
* Tests
  * Single Large object (100GB or greater so that a single file will be chunked) (This could be set smaller so that they could use 20MB instead of 100GB)
  * 1,000 objects of various sizes (1K to 1GB)
  * Doing a Bulk GET on an object not in BlackPearl cache (in 1.2 this means a server restart, in 2.4 we can use the cache reclaim api)
  * Cache full events - a client only has to do one or the other depending what which method they are using:
    * Test cache full events when using GetAvailableChunks (either by using an intermediate proxy or artificially limit the cache size)
    * Test cache full events when using naked S3 PUTs ()
