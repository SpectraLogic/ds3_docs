DS3 SDK Feature Matrix
======================

## AWS Calls

|                      | Java | C# | C | Python | Ruby |
|----------------------|:----:|:--:|:-:|:------:|:----:|
|Get Service           |  X   |  X | X |   X    |  X   |
|Create Bucket         |  X   |  X | X |   X    |  X   |
|Get Bucket            |  X   |  X | X |   X    |  X   |
|Head Bucket           |  X   |  X |   |        |      |
|Delete Bucket         |  X   |  X | X |   X    |  X   |
|Put Object            |  X   |  X | X |   X    |  X   |
|Get Object            |  X   |  X | X |   X    |  X   |
|Head Object           |      |  X |   |        |      |
|Delete Object         |  X   |  X | X |   X    |  X   |
|Multi Object Delete   |      |  X |   |        |      |
|Initial Multipart     |      |    |   |        |      |
|Put Part              |      |    |   |        |      |
|Complete Multipart    |      |    |   |        |      |
|Abort Multipart       |      |    |   |        |      |
|List Multipart Parts  |      |    |   |        |      |
|List Multipart Uploads|      |    |   |        |      |

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

