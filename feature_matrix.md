DS3 SDK Feature Matrix
======================

## AWS Calls

|                                  | Java | C# | C | Python | Ruby |
|----------------------------------|:----:|:--:|:-:|:------:|:----:|
|Get Service                       |  X   |  X | X |   X    |  X   |
|Create Bucket                     |  X   |  X | X |   X    |  X   |
|Get Bucket                        |  X   |  X | X |   X    |  X   |
|Head Bucket                       |  X   |  X |   |        |      |
|Delete Bucket                     |  X   |  X | X |   X    |  X   |
|Put Object                        |  X   |  X | X |   X    |  X   |
|Get Object                        |  X   |  X | X |   X    |  X   |
|Get Partial Object                |  X   |  X |   |        |      |
|Head Object                       |      |  X |   |        |      |
|Delete Object                     |  X   |  X | X |   X    |  X   |
|Multi Object Delete<sup>1</sup>   |      |  X |   |        |      |
|Initial Multipart<sup>1</sup>     |      |    |   |        |      |
|Put Part<sup>1</sup>              |      |    |   |        |      |
|Complete Multipart<sup>1</sup>    |      |    |   |        |      |
|Abort Multipart<sup>1</sup>       |      |    |   |        |      |
|List Multipart Parts<sup>1</sup>  |      |    |   |        |      |
|List Multipart Uploads<sup>1</sup>|      |    |   |        |      |

<sup>1</sup> - No planned support in the SDKs

Meta-Data Features
==================

|                               | Java | C# |      C       | Python | Ruby |
|-------------------------------|:----:|:--:|:------------:|:------:|:----:|
|Put Meta Data w/Object         |  X   | X  | X<sup>1</sup>|        |      |
|Get Meta Data w/Object         |      | X  |              |        |      |
|Head Meta Data                 |      | X  |              |        |      |
|Put Meta Data w/Helper Function|      |    |              |        |      |
|Get Meta Data w/Helper Function|      |    |              |        |      |

<sup>1</sup> - This can be accomplished with the `ds3_request_set_custom_header`

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

<sup>1</sup> - This API call is deprecated

Get Bucket Params
=================

|         | Java | C# | C | Python | Ruby |
|---------|:----:|:--:|:-:|:------:|:----:|
|Marker   |  X   | X  | X |   X    |   X  |
|Delimiter|  X   | X  | X |   X    |   X  |
|Prefix   |  X   | X  | X |   X    |   X  |
|Max Keys |  X   | X  | X |   X    |   X  |

Helper Functions
================

**Note:** Currently only the Java and C# SDK have helper functions

|                          | Java | C# |
|--------------------------|:----:|:--:|
|Bulk Put                  |   X  |  X |
|Bulk Get                  |   X  |  X |
|Partial Object Get        |      |  X |
|List all Objects in Bucket|   X  |  X |
|Recover Read Job          |      |    |
|Recover Write Job         |      |  X |
|Ensure Bucket Exists      |   X  |  X |
