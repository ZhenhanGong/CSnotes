# Tiled-MapReduce

## Previous work
Phoenix: A MapReduce runtime for shared-memory.

Features
Parallelism : **threads**
Communication: shared address space

Intermediate buffer
each column correspond to a thread
each row correspond to a same key's hash value

Final buffer


## Deficiency of MapRecude on Multicore(Phoenix)
- High memory usage: keep whole input data in main memory
- Poor data locality
    temporal locality: access recent read data which is stored in cache
    spatial locality: sequential scan disk
- Strict dependency barriers


## Solution: Tiled-MapRecude
"Tiling Strategy": Divide large MapRecude job into multiple independent small sub-jobs

Requirement
Reduce function must be Commutative and Associative


### OPT1 Memo

### OPT2 Locality

