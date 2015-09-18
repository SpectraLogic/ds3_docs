Client Partner Certification Process
====================================

* Need overview of BP interactions (architecture diagram and API calls
  used)
* Tests
  * Single Large object (100GB or greater so that a single file will be chunked) (This could be set smaller so that they could use 20MB instead of 100GB)
  * 1,000 objects of various sizes (1K to 1GB)
  * Doing a Bulk GET on an object not in BlackPearl cache (in 1.2 this means a server restart, in 2.4 we can use the cache reclaim api)
