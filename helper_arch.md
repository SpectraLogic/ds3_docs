Helper Function Architecture
============================

Goals:
* Need to be able to stream a single large file without seeking
* If using job aggregation, do not allocate chunks
* If a user does not need single file streaming, allow for complete random access, possibly opening many file descriptors to the same file
* These options should be selectable via a strategy type pattern
* Users should be able to write their own strategy to replace ours
