DS3 SDK Feature Matrix
======================

Code Gen
========
|                                  |    Java     | C# | C | Python | Ruby |
|----------------------------------|:-----------:|:--:|:-:|:------:|:----:|
| Request/Response                 |     X       |    |   |        |      |
| Model                            |             |    |   |        |      |

V2.x Features
=============

#### Core Features
* ACL Support
* ABM Commands
  * Tape Specific
  * Pool Specific


#### DS3 Calls

|                                  |    Java     | C# | C | Python | Ruby |
|----------------------------------|:-----------:|:--:|:-:|:------:|:----:|
|Modify User                       |             |    |   |        |      |
|                    |             |    |   |        |      |

#### Checksum Support

|                                  |    Java     | C# | C | Python | Ruby |
|----------------------------------|:-----------:|:--:|:-:|:------:|:----:|
|MD5                               |      X      | X  | X |        |      |
|CRC32                             |      X      | X  | X |        |      |
|CRC32C                            |      X      | X  | X |        |      |
|SHA256                            |      X      | X  | X |        |      |
|SHA512                            |      X      | X  | X |        |      |

#### New Helper Functions

|                                  |    Java     | C# | C | Python | Ruby |
|----------------------------------|:-----------:|:--:|:-:|:------:|:----:|
|Native FS ACL Storage/Retrieval   |             |    |   |        |      |

#### Update S3 Backed Calls to DS3 Calls

|                                  |    Java     | C# | C | Python | Ruby |
|----------------------------------|:-----------:|:--:|:-:|:------:|:----:|
|Create Bucket                     |             |    |   |        |      |


#### Deprecated Calls to Remove

|                                  |    Java     | C# | C | Python | Ruby |
|----------------------------------|:-----------:|:--:|:-:|:------:|:----:|
|Allocate Chunk                    |             |    |   |        |      |

V1.1 Features
=============
#### C# and Java Features
* Core S3 Calls
* Core S3 Meta-data features
* Core DS3 Calls (excluding notification service api calls)
* Recover Write Job Helper Function

#### C Features
* Core S3 Calls
* Core S3 Meta-data features
* Core DS3 Calls (excluding notification service api calls)
* Helper functions to come after initial release

## AWS Calls

|                                  |    Java     | C# | C | Python | Ruby |
|----------------------------------|:-----------:|:--:|:-:|:------:|:----:|
|Get Service                       |      X      |  X | X |   X    |  X   |
|Create Bucket                     |      X      |  X | X |   X    |  X   |
|Get Bucket                        |      X      |  X | X |   X    |  X   |
|Head Bucket                       |      X      |  X | X |   X    |      |
|Delete Bucket                     |      X      |  X | X |   X    |  X   |
|Put Object                        |      X      |  X | X |   X    |  X   |
|Get Object                        |      X      |  X | X |   X    |  X   |
|Get Partial Object                |X<sup>1</sup>|  X |   |        |      |
|Head Object                       |      X      |  X | X |   X    |      |
|Delete Object                     |      X      |  X | X |   X    |  X   |
|Multi Object Delete               |      X      |  X | X |   X    |      |
|V2 Auth                           |      X      |  X | X |   X    |  X   |
|V4 Auth<sup>2</sup>               |             |    |   |        |      |
|Initial Multipart<sup>3</sup>     |      -      |  - | - |   -    |   -  |
|Put Part<sup>3</sup>              |      -      |  - | - |   -    |   -  |
|Complete Multipart<sup>3</sup>    |      -      |  - | - |   -    |   -  |
|Abort Multipart<sup>3</sup>       |      -      |  - | - |   -    |   -  |
|List Multipart Parts<sup>3</sup>  |      -      |  - | - |   -    |   -  |
|List Multipart Uploads<sup>3</sup>|      -      |  - | - |   -    |   -  |

* <sup>1</sup> - Currently limited to a single range 
* <sup>2</sup> - Still determining when this will be developed
* <sup>3</sup> - No planned support in the SDKs
* <sup>4</sup> - In progress

Meta-Data Features
==================

|                               | Java | C# | C  | Python | Ruby |
|-------------------------------|:----:|:--:|:--:|:------:|:----:|
|Put Meta Data w/Object         |  X   | X  | X  |    X   |      |
|Get Meta Data w/Object         |  X   | X  | X  |    X   |      |
|Head Meta Data                 |  X   | X  | X  |    X   |      |
|Put Meta Data w/Helper Function|      |    |    |        |      |
|Get Meta Data w/Helper Function|      |    |    |        |      |

<sup>1</sup> - In progress

DS3 API Calls
=============

|                              | Java | C# | C | Python | Ruby |
|------------------------------|:----:|:--:|:-:|:------:|:----:|
|Bulk Put                      |   X  | X  | X |   X    |   X  |
|Get Objects                   |   X  | X  | X |   X    |      |
|Bulk Get                      |   X  | X  | X |   X    |   X  |
|Get Job                       |   X  | X  | X |   X    |   X  |
|Get Jobs                      |   X  | X  | X |   X    |      |
|Delete Job<sup>2</sup>        |   X  | X  | X |   X    |   X  |
|Modify Job                    |   X  | X  | X |   X    |      | 
|Get Available Job Chunks      |   X  | X  | X |   X    |   X  |
|Allocate Job Chunk<sup>1</sup>|   X  | X  | X |   X    |   X  |
|Get Physical Placement        |      | X  | X |   X    |   X  |
|Get Physical Placement - Full |      | X  | X |        |      |
|Verify Physical Placement     |      |    |   |        |      |
|Folder Delete                 |   X  | X  | X |   X    |      |
|Get Tapes                     |   X  |    |   |        |      |
|Get Tape                      |      |    |   |        |      |
|Delete Tape                   |   X  |    |   |        |      |
|Inspect All Tapes             |      |    |   |        |      |
|Inspect Tape                  |      |    |   |        |      |
|Get Tape Failures             |   X  |    |   |        |      |
|Delete Tape Failure           |      |    |   |        |      |
|Get Tape Drives               |   X  |    |   |        |      |
|Get Tape Drive                |   X  |    |   |        |      |
|Delete Tape Drive             |   X  |    |   |        |      |
|Get Tape Libraries            |   X  |    |   |        |      |
|Get Tape Library              |   X  |    |   |        |      |
|Get Tape Partitions           |      |    |   |        |      |
|Get Tape Partition            |      |    |   |        |      |
|Get Tape Partition Failures   |      |    |   |        |      |
|Delete Tape Partition         |   X  |    |   |        |      |
|Verify System Health          |   X  | X  | X |   X    |      |
|Get System Information        |   X  | X  | X |   X    |      |

* <sup>1</sup> - This API call is deprecated
* <sup>2</sup> - Need to add the `force` flag for 2.x behavior

Get Bucket Params
=================

|         | Java | C# | C | Python | Ruby |
|---------|:----:|:--:|:-:|:------:|:----:|
|Marker   |  X   | X  | X |   X    |   X  |
|Delimiter|  X   | X  | X |   X    |   X  |
|Prefix   |  X   | X  | X |   X    |   X  |
|Max Keys |  X   | X  | X |   X    |   X  |

Notification Service
====================

**Note:** This is planned but only the Java sdk has started development on this.
 
|                            | Java | C# | C | Python | Ruby |
|----------------------------|:----:|:--:|:-:|:------:|:----:|
| Notification Registrations |   X  |    |   |        |      |

Logging Support
===============

|                            | Java | C# | C | Python | Ruby |
|----------------------------|:----:|:--:|:-:|:------:|:----:|
|  File Logging              |   X  |  ? | X |   ?    |      |

* ? - need to determine

Helper Functions
================

**Note:** Currently only the Java and C# SDK have helper functions

|                          | Java | C# | C/C++ |
|--------------------------|:----:|:--:|:-----:|
|Bulk Put                  |   X  |  X |       |
|Bulk Get                  |   X  |  X |       |
|Checksum Calculation      |      |    |       |
|Partial Object Get        |      |  X |       |
|List all Objects in Bucket|   X  |  X |       |
|Recover Read Job          |   X  |  X |       |
|Recover Write Job         |   X  |  X |       |
|Ensure Bucket Exists      |   X  |  X |       |
|Metadata                  |      |    |       |
