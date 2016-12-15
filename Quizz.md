# Quizz

## Week 4: Naming

### A name:
- [x] is a way to refer to a resource
- [x] can be a value for another name
- [ ] can exist in at most one context
- [x] can map to multiple values

### In Lampson's hierarchical approach:
- [ ] values are globally uniqe
- [ ] properties are globally uniqe
- [ ] entities are globally uniqe
- [ ] directory names are globally uniqe
- [x] directory identifiers are globally unique

### Reliability in Lampson's name service is achieved through:
- [ ] hierarchy
- [x] redundancy
- [ ] sweeps
- [ ] abstraction

**Explanation**  
Reliability is ensured by keeping multiple copies of each directory.  
Sweeps are mechanisms to keep the copies synchronized.

### Sweep:
- [ ] creates a copy of a directory
- [x] synchronises copies of a directory
- [x] requires visiting all directory copies
- [ ] improves reliability of each server holding a directory copy

### To ensure the correct value of each name in cached mapping, Lampson's name service:
- [ ] uses periodic sweeps
- [x] limits the rate at which the mappings can change
- [x] forbids changes of a given mapping until the associated expiration time elapses
- [ ] uses itself as a name service

**Explanation**  
Lampson's name service forbids changes of a given mapping until the associated expiration time elapses.  
As a side effect, it limits the rate at which the mappings can change.

### Lampson's name service insures idempotency of updates:
- [ ] through commutativity
- [ ] by ensuring that the order in which two updates are applied does not affect the result.
- [x] by ensuring that applying the same update twice has the same effect as applying it once
- [ ] None of the above. Updates are idempodent by definition.

**Explanation**  
The idempotency property means that applying the same update twice has the same effect as applying it once.

### Updates in Lampson's system:
- [x] rely on timestamps
- [x] can be applied in any order without changing the result
- [ ] are possible because the system guarantees well-defined behavior
- [ ] are necessary for caching

## Week 5: Locality

### How is performance of DRAM devices related to locality?
- [x] Sequential accesses help improve DRAM bandwidth
- [ ] DRAM is optimized for random accesses which are preferred over sequential accesses
- [x] Sequential accesses help improve DRAM latency
- [ ] There are no performance differences between random and sequential DRAM accesses, but there are energy implications.

**Explanation**  
When we access a DRAM location, a larger chunk (several KB) of surrounding data is read and moved into an internal buffer (called row-buffer).  
This is a heavy operation with respect to both time and energy.  
Reading from the buffer is, however, fast and consumes much less energy compared to the previous operation.  
Subsequent reads from the buffer allow quick placement of data onto the bus, thus improving latency, bandwidth and energy.  
Random accesses to DRAM, on the other hand, require frequent data movements from DRAM cells to the buffer and vice versa, sacrificing latency and bandwidth and wasting energy.  

### Consider an execution of a range-scan query over a table with many attributes that has no indices:
- [x] Row-stores consume more memory bandwidth
- [ ] Column-stores consume more memory bandwidth
- [ ] Row- and column-stores consume the same memory bandwidth
- [ ] Row-stores exhibit better cache behavior
- [x] Column-stores exhibit better cache behavior
- [ ] Row- and column-stores exhibit the same cache behavior
- [x] Row-stores consume more disk bandwidth
- [ ] Column-stores consume more disk bandwidth
- [ ] We can't really say, depends on the selectivity of the query

**Explanation**  
Row-stores need to fetch entire tuples, sacrificing both disk and memory bandwidth and polluting caches.  
Column-stores use those resources more efficiently and can further employ better compression techniques to minimize both bandwidth and storage requirements.  

### What is true about today's social graphs:
- [ ] They have small cuts, which is why we can easily partition them for almost independent processing
- [ ] The logical distance between any two vertices is short
- [ ] The physical distance between any two vertices is short
- [ ] The number of edges per vertex follows a power-law distribution

**Explanation**  
Social graphs are mostly random and dense, which makes them impossible to perfectly partition.  
Thanks to the "small-world phenomenon", any two vertices can be, most of the time, connected through only several intermediate vertices, although they can be spatially far from each other.  
The number of edges per vertex follow a power law (typically Zipfian) distribution, common to all natural graphs.  

### Locality in balanced binary trees is achieved by:
- [ ] storing all children close to their parents
- [x] keeping nodes at the leaf level close to each other
- [ ] creating many indexes on the data

**Explanation**  
It is impossible to keep children close to parents in a balanced binary tree as the number of children grows exponentially with number oflevels.  
But it is possible to store the leaf level of the tree locally to allow quick scans over this level.  
Indexes have nothing to do with locality.  

### Which algorithms will be relatively easy to parallelize?
- [x] computing a synchronized country-wide train and metro schedule
- [ ] analyzing friendship information on a popular social network
- [x] finding a multiflight connection with Lufthansa

**Explanation**  
It is easier to parallelize an algorithm working on a graph with small cuts.  
The train and metro schedule graph can be divided by cities. There are not that many railroad lines between cities.  
Similarly, most traditional airlines, like Lufthansa, operate using hubs.  
There are many flight to a local hub and not so many connections between hubs.  

### Consider an example of matrix multiplication:
  for i in 0..n  
    for j in 0..m  
      for k in 0..p   
        C[i][j] = C[i][j] + A[i][k] * B[k][j];  
Assume that the matrices are large enough not to fit in L1/L2/L3 caches.  
The matrices are stored in row-major order, that is, the rows of a matrix are listed in sequence.  
Which of the following is the optimal loop ordering?  
- [ ] i, j, k
- [x] i, k, j
- [ ] j, i, k
- [ ] j, k, i
- [ ] k, i, j
- [ ] k, j, i

**Explanation**  
Efficient algorithms for matrix multiplication exploit spatial (and temporal) locality.  
With row-major order, it is advantageous to refer to several memory addresses that share the same row.  
By keeping the row number fixed, the second element changes more rapidly, meaning the memory addresses are used more consecutively.  
Since j affects the column reference of both matrices C and B, it should be iterated in the innermost loop (this will fix the row iterators, i and k, while j moves across each column in the row).  
This will not change the mathematical result, but it improves efficiency.  

### Block Nested Loops Join:
- [x] achieves better performance than Nested Loop Join because it minimizes number of disk reads
- [x] achieves better performance than Nested Loop Join because it utilizes the main memory as a buffer more efficiently
- [ ] achieves better performance than Nested Loop Join because it minimizes the size of outer relation
- [ ] achieves worse performance than Nested Loop Join because it requires more I/O operations
- [x] works for both equality and inequality joins

**Explanation**  
Block Nested Loops Join uses the entire available main memory to store data.  
That allows to reduce the number of disk reads and therefore improves performance.  
As values in join column of each relation are directly compared, the used operator may be equality as well as inequality.  

### Hash-join:
- [x] consists of three phases
- [ ] works for both equality and inequality joins
- [x] requires two different hash functions
- [ ] requires one hash function that needs to be called twice for each tuple
- [ ] actually has nothing to do with hashing

**Explanation**  
There are two different hash functions.  
One splits tuples into buckets on disk, the other splits tuples from one bucket in main memory.  
Because of the way hashing works, only equality comparison is possible.  

## Week 6: Atomicity and Consistency

### A transaction schedule is serializable if:
- [x] during the execution there is no interleaving of read/write actions from different transactions
- [ ] none of the transactions violate consistency
- [x] the effect of the execution is identical to executing transactions in some serial order regardless of the initial database state
- [ ] the effect of the execution does not depend on the order of execution of the transactions

**Explanation**  
A transaction schedule is serializable if it is equivalent (having the same effect) to some serial execution of the transactions.  
Notice that a serial schedule is always serializable, but the opposite does not necessarily hold.  

### Two schedules are equivalent if:
- [ ] for any order of actions the effect of executing both schedules is identical
- [x] for any database state, the effect of executing both schedules is identical
- [ ] for any order of transactions, the effect of executing both schedules is identical
- [ ] for any database state, actions in both schedules do not interleave

**Explanation**  
A schedule defines the order of actions.  
Two schedules are identical if executing actions in order defined by any of them, would always give the same result.  

### Which types of anomalies does the following schedule exhibit?  
T1:R(A), T1:W(B), T2:R(B), T2:W(A), T1:R(A), T1:COMMIT, T2:COMMIT
- [x] dirty read
- [ ] phantom read
- [x] unrepeatable read
- [ ] write-write conflict.

**Explanation**  
T2 reads uncommited data B (dirty read), T1 reads two different values of A (unrepetable read).  
There are no insertions or deletions (phantom read), nor WW conflicts.

### Which of the ACID properties are guaranteed to hold in any system that executes all transactions serially ?
- [ ] Atomicity
- [ ] Consistency
- [x] Isolation
- [ ] Durability

**Explanation**  
In a serial execution order, when some transaction is executed, all other transactions are either completed or not started yet, which guarantees the isolation property.  
However, atomicity, consistency and durability are not guaranteed (e.g., all of these properties might be broken if a system crashes while executing a transaction).  

### In the strict two-phase locking protocol a transaction must:
- [ ] acquire all the locks before before reading any value
- [ ] acquire all the locks before before updating any value
- [x] acquire all the locks before releasing any lock
- [ ] acquire all the locks at once
- [x] not release any locks until the end of transaction

**Explanation**  
The two-phase locking protocol enforces transactions to acquire the locks for all the data they will access before releasing any lock.  
The strict two-phase locking protocol additionally requires the transactions to release all the locks at once when the transaction ends, which is done by the system when the transaction gets committed or aborted, thus is not explicitly initiated by the transaction.  

### Choose statements that are always correct:
- [x] if a schedule is conflict serializable, it is also serializable
- [ ] if a schedule is serializable it is also conflict serializable
- [x] if a schedule is view serializable, it is also serializable
- [ ] if a schedule is serializable, it is also view serializable
- [ ] if a schedule is view serializable, it is also conflict serializable
- [x] if a schedule is conflict serializable, it is also view serializable

**Explanation**  
Check the lecture at 20:35. serializable > view serializable > conflict serializable.

### Consider the following schedule involving two transactions T1 and T2:  
T1:R(A), T1:W(A), T2:R(A), T1:W(B), T1:COMMIT, T2:R(B), T2:W(B), T2:COMMIT  
The schedule is:  
- [ ] no serializable
- [x] view-serializable
- [x] conflict-serializable

**Explanation**  
The schedule is conflict-serializable, thus view-serializable too.  
The schedule corresponds to a serial execution of T1 followed by T2.  

### Which of the following statements are true?
- [x] 2 Phase Locking (2PL) ensures acyclic dependency graphs.
- [ ] Strict 2 Phase Locking (S2PL) ensures immunity from deadlocks.
- [ ] 2PL avoids cascading aborts.
- [ ] Locks can be acquired and released in both phases of 2PL.

**Explanation**  
2PL and S2PL ensure acyclic dependency graphs, but deadlocks can appear in both. S2PL avoids cascading aborts.  
Locks can be acquired (released) only in the first (second) phase of 2PL.  

### Consider the schedule  
T1:R(C), T3:W(B), T2:R(A), T1:W(C), T3:W(A), T2:R(C), T3:COMMIT, T1:COMMIT, T2:COMMIT  
Which of the following protocols does allow the actions to occur in precisely the order shown?  
- [x] 2PL
- [ ] Strict 2PL
- [ ] None of the above.

**Explanation**  
The schedule is allowed under 2PL:  
T1:lock(C) T1:R(C) T3:lock(B) T3:W(B) T2:lock(A) T2:R(A) T1:W(C)  
T1:unlock(C) T2:lock(C) T2:unlock(A) T3:lock(A) T3:W(A) T3:unlock(B)  
T3:unlock(A) T2:R(C) T2:unlock(C) T3:COMMIT T1:COMMIT T2:COMMIT  

### In the Kung-Robinson optimistic concurrency control model:
- [ ] during the first phase transactions read from and write to a private copy of the database
- [ ] during the first phase transactions can write to a copy of the database visible to other transactions
- [x] during the first phase transactions write to a private copy of the database, but read from the globally visible database
- [x] writing the locally modified values to the globally visible database must be done atomically

**Explanation**  
During the first phase transactions read from the globally visible database, but can write only to local copies, which must be written back atomically.

### Optimistic concurrency control:
- [ ] provides methods for deadlock detection and prevention
- [x] works best if conflicts are rare
- [ ] never requires transactions to abort
- [x] relies on three tests to make sure no conflicts occured

**Explanation**  
The most important assumption for optimistic concurrency control is that majority of transactions are independent and do not conflict.  
It does not prevent conflicts from happening and therefore aborting a transaction might be required.  
There are three tests used to determine if two transactions are in conflict.  
Finally, optimistic concurrency control does not use locks and therefore there are no deadlocks.

### Which of the following schedules is/are allowed under Optimistic Concurrency Control?
- [ ] T1:R(X), T2:R(X), T1:W(X), T2:W(X), T1:COMMIT, T2:COMMIT
- [ ] T1:W(X), T2:R(Y), T1:R(Y), T2:R(X), T1:COMMIT, T2:COMMIT
- [x] T1:R(X), T2:R(Y), T3:W(X), T2:R(X), T1:R(Y), T1:COMMIT, T2:COMMIT, T3:COMMIT
- [ ] None of the above.

### Which of the following schedules is/are allowed under the multiversion protocol?
- [ ] T1:R(X), T2:R(X), T1:W(X), T2:W(X), T1:COMMIT, T2:COMMIT
- [x] T1:W(X), T2:R(Y), T1:R(Y), T2:R(X), T1:COMMIT, T2:COMMIT
- [x] T1:R(X), T2:R(Y), T3:W(X), T2:R(X), T1:R(Y), T1:COMMIT, T2:COMMIT, T3:COMMIT
- [x] T1:R(X), T1:R(Y), T1:W(X), T2:R(Y), T3:W(Y), T1:W(X), T2:R(Y), T1:COMMIT, T2:COMMIT, T3:COMMIT
- [ ] None of the above.

### Snapshot isolation:
- [x] provides each transaction with an abstraction of working on a copy of a database
- [ ] guarantees serializability
- [ ] is frequently used to implement multiversion concurrency control
- [ ] requires using locks
- [x] is popular in many modern DBMS

**Explanation**  
Snapshot isolation is often used by DBMS to provide consistency control.  
Each transaction has an impression of working on its own copy of a database.  
But there are counterexamples showing that SI cannot guarantee serialazbility.  
It can be implemented using multiversion CC, not the other way round.

### Which of the following schedules is/are allowed under Snapshot Isolation?
- [ ] T1:R(X), T2:R(X), T1:W(X), T2:W(X), T1:COMMIT, T2:COMMIT
- [x] T1:W(X), T2:R(Y), T1:R(Y), T2:R(X), T1:COMMIT, T2:COMMIT
- [x] T1:R(X), T2:R(Y), T3:W(X), T2:R(X), T1:R(Y), T1:COMMIT, T2:COMMIT, T3:COMMIT
- [x] T1:R(X), T1:R(Y), T1:W(X), T2:R(Y), T3:W(Y), T1:W(X), T2:R(Y), T1:COMMIT, T2:COMMIT, T3:COMMIT
- [ ] None of the above.

### TenStore is distributed key-value store replicates data across 10 nodes.
An update operation in TenStore is considered successful if 6 replicas acknowledge the write completion.  
To ensure strong consistency, how many read operations should be performed at least?  
- [ ] 1
- [ ] 4
- [x] 5
- [ ] 6
- [ ] 10
- [ ] Strong consistency cannot be guaranteed

**Explanation**  
N=10, W=6. R+W>N, thus R must be at least 5.  
With 4 or less read operation it is possible that all the read values are stale, even if they are the same.
