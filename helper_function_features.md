Helper Feature Matrix
======================

## Features

* Retry during a 'short' Network interruption (should be tranparent to the user) for Puts and Gets
* Have the ability to test for cache full, with tries, but with a maximum number of retries (our RetryAfter feature)
* Job restart capabilities
* Consistent Strategies across .net and java
* Make the list commands lazy
* Client side filtering

## Object Failure Conditions
* Too many retries
* Can't read the local file
* File not found
* FailedRequestException\BadRequestException

## On Error Conditions
* IO/Network errors are not considered a failure
* FailedRequestException is a failure

## Retry Conditions
* Any IO/Network error - make configurable, and should be done on a per request basis

## Brainstorming
* Add onBlobFailure event, when we detect an error, or when we fail a object.  Only emit it when an object is failed, rather than when we encounter a single io error
* Extend Ds3NoMoreRetriesException for CacheFull conditions, and possibly other retry failure conditions (like Ds3NetworkFailures)
* Best effort - we continue sending up to some failure threshold, or no progress can be made (ie we are not getting any more chunks allocated)
* Live lock detection after a threshold

Feature Matrix
========
|                                  |    Java     | C# | C | Python | Ruby |
|----------------------------------|:-----------:|:--:|:-:|:------:|:----:|
|                  |            |    |   |        |      |
|                             |             |    |   |        |      |
|                             |             |    |   |        |      |
