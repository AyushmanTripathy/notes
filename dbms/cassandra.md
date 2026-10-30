# Apache Cassandra

Defined by
1. NoSQL
2. Wide column: No of columns in each row can vary
3. Distributed: Spreads data across multiple nodes
4. Built for write throughput
5. linear scaling: Double nodes mean double throughput

Originated from Google Bigtable

### Different from columnar (column-oriented) Db

- Clickhoues, Google BigQuery are columnar
- Instead of storing data of a row together, they do columns
- Efficient for queries like SUM, AVG on columns

### How cassandra works?

```
Client <-> Coordinator <-> Replica
```

- Here coordinator is any node, 

## Log strucutred merge tree

- This is the write pattern behind cassandra
- Also used by ScyllaDB (rewrite of cassandra), RocksDB etc

### How a Write works?

1. Append to the WAL
2. Insert into memtable
    - memtable is a sorted in memory structure
    - Data inserted into memtable by key
    - if key is already present, old value is replaced.
    - Write is Acknowledged. (after log append + memory insert)
3. memtable becomes immutable
    - when memtable reaches size limit (ex. 64mb), it is frozen
    - new WAL segment & memtable takes over. So writes are not blocked
4. Flush to SSTable
    - For sorted memtable, each entry is written into data blocks
    - for each key timestamp is attached.
    - Sparse index is created (first key of block to offset in file)
    - Bloom filters (set of keys to skip file during reads)
    - memtable & WAL is released once SSTable is flushed.
5. Compaction
    - Merges SSTables into fewer, larger ones.
    - Reads sequentially from both files, resolves conflicts (newer timestamps are kept)
    - Tombstones are purged after a grace period, default 10days.
    - New index, bloom filters and metadata are created.
    - Full sequential IO, hence fast.
Updates are new writes, Delete writes a tombstone

### How a Read works?

1. Client requests to a coordinator
2. Coordinator hashes the key to find replicas that own the data
3. Coordinator request from replica based on consistancy level
    - A full data requests to one replica (usually closest one)
    - Digest requests to others.
4. On each replicas
    - first check the memtable
    - Then find relevant SSTablee, using metadata & bloom filters
    - Locate data inside SStables, using key cache or sparse in-memory index.
    - Find relevant data block, decompress it, verify checksum
5. Merge the fragments column by column
6. Replicas responds and coordinator reconciles
    - If digests match, returns data to client
    - If digests dont match, it request full data from replicas and returns newest verison
    - On mismatch, coordinator sends correct version to out of date replicas.

### LSM vs BTree

- Btree updates pages in place on disk.
- LSM always writes sequentially and never updates in place.
- Trades read performace for write performance.
