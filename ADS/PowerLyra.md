# PowerLyra

## Graph are Everywhere
- Traffic network graphs
- Biological network
- Social network


## Think like a vertex
  Coding graph algorithms as **vertex-centric** programs to process *vertices* in parallel and
communicate along *edges*.<br>


## Power-law degree distribution
> "*most* vertices have relative *few* neighbors while a *few* have *many* neighbors."


## Challenge: Locality vs. Parallelism
  **Low-degree vertex** prefer *locality* over parallelism, since making resource locally accessible
can **reduce network latency**. As for parallelism, it is not worthwhile since it will introduce 
more communication, computation and synchronization overhead.<br>
  **High-degree vertex** prefer *parallelism* over locality, since parallelism can evenly
**parallelize the workloads to avoid load imbalance**. As for locality, it is not worthwhile since
it will incur imbalance, high contention and heavy network traffic.<br>
  However, in natural graph, both Low-degree vertex and High-degree vertex can not be ignored,
for example, in Sina Blog, there are *100M* users who has *100* followers, and there are *100* users
who has *100M* followers. Therefore both Low-degree vertex and High-degree vertex are important.
This necessitate a partition algorithm to take care of both **locality for low-degree vertex**
and **parallelism for high-degree vertex**.<br>


## Existing efforts

### Pregel & GraphLab
Focus on exploiting *Locality* <br>
Partition: use *edge-cut* to evenly assign *vertices* along with all edges <br>
Computation: *aggregate* all resources (i.e. messages or replicas) of a vertex on local machine <br>

![Pregel GraphLab](graphlab_pregel.png)

### PowerGraph & GraphX
Focus on exploiting *Parallelism* <br>
Partition: use *vertex-cut* to evenly assign *edges* with replicated vertices <br>
Computation: *decompose* the workload of a vertex into multiple machines <br>

![PowerGraph](powergraph.png)


## PowerLyra
differentiated graph computation & partition

### graph partitioning
Hybrid-cut
Low-cut (like edge-cut)
High-cut (like vertex-cut)

#### low-cut
hash vertices to machines

#### high-cut
heuristic



graph store: edge-list



## graph computation
hybrid-mode

