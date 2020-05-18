# augmented_log

This is an improved version of the [basic_log](https://github.com/chrislessard/key-value-store), supporting some functionality common to SSTables, namely the creation, merging and compaction of segments. The interface is as follows:

1. store {key} {data} : store the pair (key, value) in the database
2. get {key} : retrieve the most recent value on disk associated with key
3. compact_segments : run the compact and merge algorithm on the segments on disk.
4. load_index : scan the current segment, and load its values into the index. this requires a linear parse of the file and is slow!
5. save_index_snapshot {filename} : save a snapshot of the index to disk, as a pickle dump named {filename}
6. load_index_snapshot {filename} : load an aforementioned snapshot on the index to disks
7. set_threshold {number of bytes} : set the new segment threshold for the db in bytes

The main improvement over the basic_log comes in the use of an index to perform fast lookups on key values pairs, and the introduction of segments and the compaction algorithm to reclaim diskspace and speed up reads.

## Dependencies

The project requires python3.

## Run

Invoke `python main.py`.

## Testing

Invoke `python augemented_log_tests.py`.

## Benchmarking

Invoke `python augmented_log.py`