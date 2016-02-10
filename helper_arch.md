Helper Function Architecture
============================

Goals:
* Need to be able to stream a single large file without seeking
  * If there are several large files, stream each in parallel allocating a chunk on demand
* If using job aggregation, select a strategy to not allocate chunks
* If a user does not need single file streaming, allow for complete random access, possibly opening many file descriptors to the same file
* These options should be selectable via a strategy type pattern, there should be some interface describing the general pattern which can be implemented internally and externally
* Users should be able to write their own strategy to replace ours
 
Possible interfaces for the strategy:

```csharp

public interface ChunkStrategy {
    IEnumerable<Blob> getNextBlobs(IDs3Client client, IJob job);
    
    // Create a new stream for every blob returned by getNextBlobs
    boolean createNewStreams();
} 

public class RandomAccessStrategy : ChunkStrategy {
    IEnumerable<Blob> getNextBlobs(IDs3Client client, IJob job) {
        // get available chunks, and returns the blobs in each of the chunks
        // only returning those chunks that we've not processed
    }
    
    boolean createNewStreams() {
        return true;
    }
}

public class StreamStrategy : ChunkStrategy {
    
    // have a stream to chunk mapping, and a set of what chunks have been allocated
    
    IEnumerable<Blob> getNextBlobs(IDs3Client client, IJob job) {
        // allocate the next blob in the existing streams
    }
    
    boolean createNewStreams() {
        return false;
    }
}

public class NoAllocateStrategy : ChunkStrategy {

    // have a list of all the blobs that were returned by start bulk put

    IEnumerable<Blob> getNextBlobs(IDs3Client client, IJob job) {
        // return all the blobs in the job that haven't been returned already
    }
    
    boolean createNewStreams() {
        return true;
    }
}
```
