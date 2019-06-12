# Distributed System Consistency

## 1. What is Consistency
> **Consistency model** defines rules for the apparent **order** and **visibility** of updates.
1. local memory:
  **Single object** consistency is also called "coherence".
2. database:
  Consistency across **multiple objects** (all or nothing).
![Consistency](what_is_consistency.png)

## 2. Consistency is hard in Distributed System
  Consistency is hard in distributed systems.
- Data replication.(Caching)
- Concurrency.(no shared locks)
- Failure.(machines or network)

## 3. Difference between Consistency and Coherence.
  **Coherence** occurs in systems that are cached or cache-less, and it deals with when writes
to a **single variable** are seen by all processors. A memory is coherent if a *read* operation
always retrieve the value of most recent *write* operation.<br>
  **Consistency** deals with the ordering of operations to **multiple variable** with respect to
all processors.<br>

## 4. Consistency Models
  **Consistency Models** are used in distributed systems like **Distributed Shared Memory** 
systems or distributed data store(such as **File Systems**, **Database**).<br>
  **Consistency Models** specify some rules, if those rules are followed, memory will be 
consist, and the results of *reading*, *writing*, or *updating* memory will be predictable.<br>
  There are several DS consistency models, including **Strict Consistency**, **Sequential 
Consistency**, **Causual Consistency**, **Release Consistency**, and **Eventual Consistency**.<br>

### 5. Strict Consistency
  Strict Consistency is the strongest consistency model. And it is impractical to 
implement.<br>
  Under this model, each operation is stamped with a global wall-clock time.

### 5.1 Sequential Consistency
<br>

### 5.2 Release Consistency
<br>

### 5.3 Causual Consistency
<br>

### 5.4 Eventual Consistency
<br>


## Mutual Exclusion

  CPU 0: W(X) R(Y)
  CPU 1: w(Y) r(X)

  All possible inter-leavings:

- W(X)1  R(Y)0  w(Y)1  r(X)1   (CPU 0 enters critical section)
- W(X)1  w(Y)1  R(Y)1  r(X)1   (none enters)
- W(X)1  w(Y)1  r(X)1  R(Y)1   (none enters)
- w(Y)1  W(X)1  R(Y)1  r(X)1   (none enters)
- w(Y)1  W(X)1  r(X)1  R(Y)1   (none enters)
- w(Y)1  r(X)0  W(X)1  R(Y)1   (CPU 1 enters critical section)
