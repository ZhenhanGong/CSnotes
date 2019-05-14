# PowerLyra

## Graph are Everywhere
- Traffic network graphs
- Biological network
- Social network
<br>
<br>
<br>

## Think like a vertex
  Coding graph algorithms as **vertex-centric** programs to process *vertices* in parallel and
communicate along *edges*.
<br>
<br>
<br>

## Power-law degree distribution
> "*most* vertices have relative *few* neighbors while a *few* have *many* neighbors."
<br>
<br>
<br>

### Challenge: Locality vs. Parallelism
  **Low-degree vertex** prefer *locality* over parallelism, since making resource locally
accessible can **reduce network latency**. As for parallelism, it is not worthwhile since it
will introduce more communication, computation and synchronization overhead.<br>
  **High-degree vertex** prefer *parallelism* over locality, since parallelism can evenly
**parallelize the workloads to avoid load imbalance**. As for locality, it is not worthwhile
since it will incur imbalance, high contention and heavy network traffic.
<br>
<br>

### Dilemma in natural graph
  However, in natural graph, both Low-degree vertex and High-degree vertex can not be
ignored, for example, in Sina Blog, there are *100M* users who has *100* followers, and there
are *100* users who has *100M* followers. Therefore both Low-degree vertex and High-degree
vertex are important.<br>
  This necessitate a partition algorithm to take care of both **locality for low-degree vertex**
and **parallelism for high-degree vertex**.
<br>
<br>
<br>

## Existing efforts
<br>

### Pregel & GraphLab
  Focus on exploiting *Locality* <br>
  Partition: use *edge-cut* to evenly assign *vertices* along with all edges <br>
  Computation: *aggregate* all resources (i.e. messages or replicas) of a vertex on local 
machine <br>

<img src="graphlab_pregel.png" alt="Pregel GraphLab" width="350"/>
<br>

### PowerGraph & GraphX
  Focus on exploiting *Parallelism* <br>
  Partition: use *vertex-cut* to evenly assign *edges* with replicated vertices <br>
  Computation: *decompose* the workload of a vertex into multiple machines <br>

<img src="powergraph.png" alt="PowerGraph" width="250"/>
<br>
<br>
<br>

## PowerLyra
  **PowerLyra** adopts differentiated graph computation & partition strategies on skewed graphs.
And it embraces both **locality** for *low-degree vertex* and **parallelism** for *high-degree 
vertex*.
<br>
<br>
<br>

### Graph partitioning
  *Both* vertex cut & edge cut will use *replicas*.
<br>
<br>

#### Vertex cut
  **Vertex cut** will evenly assign **edges** with replicated vertices.
  Replicas store **incomplete** edges info.
  Computation will be parallelize on all replicas.

<img src="edge-vertex-cut.png" alt="vertex cut & edge cut" width="500"/>
<br>

#### Edge cut
  **Edge cut** will evenly assign **vertices** along with all edges.
  Masters store **complete** edges info.
  No computation task run on replicas.
<br>
  
TO BE CONTINUED
  **Hybrid-cut**: differentiate graph partitioning for low-degree & high-degree vertices.
- Low-cut (like edge-cut)
- High-cut (like vertex-cut)

#### low-cut
hash vertices to machines

#### high-cut
heuristic



graph store: edge-list



## Graph computation
hybrid-mode

