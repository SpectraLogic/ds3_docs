DS3 SDK Feature Matrix
======================

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
|Head Bucket                       |      X      |  X |   |        |      |
|Delete Bucket                     |      X      |  X | X |   X    |  X   |
|Put Object                        |      X      |  X | X |   X    |  X   |
|Get Object                        |      X      |  X | X |   X    |  X   |
|Get Partial Object                |X<sup>1</sup>|  X |   |        |      |
|Head Object                       |             |  X |   |        |      |
|Delete Object                     |      X      |  X | X |   X    |  X   |
|Multi Object Delete               |      X      |  X |   |        |      |
|V2 Auth                           |      X      |  X | X |   X    |  X   |
|V4 Auth<sup>2</sup>               |             |    |   |        |      |
|Initial Multipart<sup>3</sup>     |             |    |   |        |      |
|Put Part<sup>3</sup>              |             |    |   |        |      |
|Complete Multipart<sup>3</sup>    |             |    |   |        |      |
|Abort Multipart<sup>3</sup>       |             |    |   |        |      |
|List Multipart Parts<sup>3</sup>  |             |    |   |        |      |
|List Multipart Uploads<sup>3</sup>|             |    |   |        |      |

* <sup>1</sup> - Currently limited to a single range 
* <sup>2</sup> - Still determining when this will be developed
* <sup>3</sup> - No planned support in the SDKs

Meta-Data Features
==================

|                               | Java | C# | C  | Python | Ruby |
|-------------------------------|:----:|:--:|:--:|:------:|:----:|
|Put Meta Data w/Object         |  X   | X  |    |        |      |
|Get Meta Data w/Object         |      | X  |    |        |      |
|Head Meta Data                 |      | X  |    |        |      |
|Put Meta Data w/Helper Function|      |    |    |        |      |
|Get Meta Data w/Helper Function|      |    |    |        |      |


DS3 API Calls
=============

|                              | Java | C# | C | Python | Ruby |
|------------------------------|:----:|:--:|:-:|:------:|:----:|
|Bulk Put                      |   X  | X  | X |   X    |   X  |
|Bulk Get                      |   X  | X  | X |   X    |   X  |
|Get Job                       |   X  | X  | X |   X    |   X  |
|Get Jobs                      |   X  | X  |   |        |      |
|Delete Job                    |   X  | X  | X |   X    |   X  |
|Modify Job                    |   X  | X  | X |   X    |      | 
|Get Available Job Chunks      |   X  | X  | X |   X    |   X  |
|Allocate Job Chunk<sup>1</sup>|   X  | X  | X |   X    |   X  |
|Get Physical Placement        |      |    | X |        |   X  |

* <sup>1</sup> - This API call is deprecated

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


Helper Functions
================

**Note:** Currently only the Java and C# SDK have helper functions

|                          | Java | C# |
|--------------------------|:----:|:--:|
|Bulk Put                  |   X  |  X |
|Bulk Get                  |   X  |  X |
|Checksum Calculation      |      |    |
|Partial Object Get        |      |  X |
|List all Objects in Bucket|   X  |  X |
|Recover Read Job          |      |    |
|Recover Write Job         |      |  X |
|Ensure Bucket Exists      |   X  |  X |
