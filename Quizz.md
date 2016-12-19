# Quizzes

## Week 1: Modularity and Abstraction

### A reliable computer system
- [ ] does not allow intruders to penetrate it
- [ ] cannot cause catastrophic events
- [x] with high probability behaves as expected
- [ ] achieves high performance
**Explanation**
As described on slide 7, reliability pertains to the system meeting its specification most of the time. Of course, one could imagine placing security/safety/performance properties in the specification, but keeping the domains of interest separate simplifies discussion.

### Consider the following property of a car: "If the brakes are applied, then the car's speed after applying the brakes is lower than its speed prior to the application of the brakes." Is this a
- [x] safety property
- [ ] security property
- [ ] reliability property
- [ ] manageability property
**Explanation**
The failure of a car to uphold this property can have catastrophic consequences (e.g., loss of life), so it is a safety property. In contrast, a property like "after pressing the radio's on button, the radio is on" would be a reliability property, because failure of the radio to come on would not have catastrophic consequences.

### A well designed system
- [ ] has minimal interactions with its environment
- [ ] has isolated components that do not interact with each other
- [ ] is free of bugs
- [x] enables predicting the system-level behavior based on the behavior of its components
**Explanation**
Careful attention to slides 3 and 8 directly gives the answer to this question.

### The ultimate reason the GE XA/21 energy management system failed was that
- [x] one of its components behaved in an unexpected way
- [ ] the environment behaved in an unexpected way
- [ ] the system interface exposed unexpected behavior
- [ ] the interaction between multiple components was unexpected
**Explanation**
The only truly unexpected behavior (i.e., behavior for which the system had not been provisioned) was the failure of the backup server. The primary server was expected to fail (since there was a backup provisioned), and the environment did not behave any differently from other hot August months. While the system indeed exhibited unexpected behavior at its interface, that was not the reason the GE XA/21 failed. Finally, the interactions between components were not unexpected, they proceeded exactly as intended.

### Say a program has two functions F1() and F2(). F2 is called from two places inside F1. Two developers, Alice and Bob, are asked to write unit tests for these functions such that all paths through the tested function are covered. Alice dutifully writes unit tests for F1 and then unit tests for F2. Bob decides to inline F2 and write unit tests only for F1 (since F2 no longer exists). Who ends up having to write the most unit tests in order to reach the 100% path coverage target?
- [ ] Alice
- [ ] Bob
- [x] sometimes Alice must write more unit tests than Bob, and sometimes it's the other way around
**Explanation**
Each test case corresponds to one execution path.
Let Fx be Bob's version of F1 that has F2 inlined. Let N1 be the number of paths in F1, N2 the number of paths in F2, and Nx the number of paths in Fx.
Alice has to write N1+N2 tests, whereas Bob has to write Nx tests.
If F2 is called from two different paths in F1, the paths for F2 have to be tested multiple times.
If, on the other hand, both F1 or F2 only have a single path, the inlined version will only have a single path. Therefore, the number of paths of the inlined version is fewer in this case.

### Consider a program that has N if-then-else branches and takes an integer as an input. If this program is tested with all possible integer inputs, what is the minimum number of distinct paths exercised through this program?
- [x] 1
- [ ] N+1
- [ ] Nˆ2
- [ ] 2ˆN
**Explanation**
The minimum number of paths results when each if-then-else branch has exactly one possible outcome, regardless of input, such as "if (1 > 0) { ... } else { ... }".
In this case, invoking the program with any number of distinct tests will still execute the same path through the code, because there exists only one feasible path. Therefore, the minimum number of paths is 1.


### How many lines of code (LOC) were verified in the seL4 operating system kernel?
- [ ] several hundred
- [x] several thousand
- [ ] several tens of thousands
- [ ] several hundreds of thousands
**Explanation**
7,500 LOC were verified (see slide 8).


### The lecture talked about testing and verification. Which of the following statements are always correct?
- [ ] Given a fixed time budget, verification always finds more bugs than testing
- [ ] Given a fixed time budget, testing always finds more bugs than verification
- [x] Verification can demonstrate the absence of bugs
- [x] Testing can demonstrate the presence of bugs
**Explanation**
The first two options cannot be decided a priori, it depends on the code and the testing/verification being done.
The last two options are always correct by definition: verification produces a proof that a system always meets its specification (i.e., is free of bugs), while testing looks for ways in which the system fails and finds input values for which these failure manifest (i.e., it finds inputs that prove the system has bugs).


### At which stage of building a system is it important to reduce complexity?
- [x] design
- [x] implementation
- [x] refactoring
**Explanation**
A system builder should try to reduce complexity any time (s)he can.

### Say you are in charge of developing a fairly complex system, and it's starting to look like you will miss the promised release deadline. Which of the following actions is most likely to help you meet the deadline?
- [x] reduce the number of requirements correct
- [ ] increase amount of testing to ensure that there will be no surprises before the deadline
- [ ] deploy to alpha testers to get some understanding of what are the usage scenarios
- [ ] increase the team size
**Explanation**
There is a (at least) quadratic relationship between the number of requirements and the complexity of a system; complexity is often tightly correlated to the success of a development project. Thus, reducing requirements by a little bit is likely to significantly reduce the complexity of the system.
None of the other options have this quadratic effect. Furthermore, unless the development tasks are easily partitionable among developers, increasing the team size is likely to slow down the development effort, at least initially.

### Consider two systems, S1 and S2. S1 has N components, and each component is interconnected with half the other components. S2 has Nˆ2/2 components, with each component connected to at most two other components. Which system is more complex?
- [ ] S1
- [ ] S2
- [x] Insufficient information to decide correct
**Explanation**
The number of components and interconnections does not, by itself, determine complexity (even though they are good indicators). One has to also look at what amount of regularity exists in the system.

### Consider a standard Linux/Windows/Mac OS system; which of the following actions are likely to make the system simpler to manage?
- [x] replace all dynamically linked binaries with statically linked ones
- [ ] restrict the maximum number of concurrent users to 10
- [ ] remove all drivers for printers and scanners
- [ ] empty the trash and/or delete everything in /tmp
**Explanation**
Anything that reduces the number of components (such as removing all support for printers and scanners) or the number of interconnections (such as removing dynamic linking) is likely to make the system simpler overall. The number of concurrent users does not directly relate to any of the complexity metrics, and emptying the trash or /tmp does not reduce the number of components or interconnections (but it could confuse some running daemons, thus creating management headaches).


### Consider a standard e-commerce site, like Amazon.com. During the holiday period, when the number of visitors to the site increases dramatically, the sysadmins decide to double the number of Web servers on the front-end. What should they do with the number of database servers?
- [ ] double it, since they have to serve increased database load
- [ ] halve it, since the Web servers can carry now more load
- [ ] keep it the same
- [x] depends on the other parts of the system
**Explanation**
A complex system like an e-commerce site is likely to have properties of incommensurate sclaing, so it is difficult to predict how the load on the database back-end will vary if the front-end doubles the number of users it can handle. It also depends on user behavior: doubling the number of visitors does not mean that there will be twice as many transactions to execute, since it may happen that Amazon.com's prices are too high, and all visitors go to the competitor.


### Consider the BitTorrent file distribution protocol. When run on two nodes, exchanging a file over BitTorrent is no faster then just copying it from one node to another. However, when the number of nodes grows to thousands, disseminating the file to all of them over BitTorrent becomes significantly faster then copying it from one node to all the others. Which of the system properties shown in lecture are good explanations of this behavior?
- [x] Emergent properties
- [ ] Propagation of effects
- [x] Incommensurate scaling
- [ ] Inevitable trade-offs
**Explanation**
This is a clear case of incommensurate scaling, because the system's bandwidth for disseminating copies of the file increases quadratically in the number of nodes, which is faster than linear. This is an example where incommensurate scaling is beneficial. It is also a case of an emergent property, in that a handful of BitTorrent nodes is not particularly useful, but putting many of them together significantly transforms the system's utility.
The other two options are not related to the performance of disseminating a file to all nodes.

### Which of the following statements are true about modularity?
- [x] it can limit the propagation of effects
- [x] it can make component replacement easier, without having to rebuild the system from scratch
- [ ] it enables a component to treat all other components solely based on their interface specification
- [x] it makes it possible to test components in isolation from each other
**Explanation**
Modularity walls off data and functionality into a "box", thereby reducing the amount of propagation of effects, allowing the box to be moved (including replaced) with minimal disruption, and operating on it (including testing) separately from the rest.
However, modularity says little about the interface we assign to the module. That aspect belongs to abstraction.

### In previous lectures we saw that, the larger a system is, the harder it is to test and/or verify. Does splitting a system into modules make the task of system testing/verification simpler?
- [ ] No, because the total number of paths through the system still depends exponentially on code size
- [ ] Yes, because the total number of paths through the system is now a sum of the numbers of paths through each module
- [x] It depends
**Explanation**
In general the answer is likely to be Yes, but one cannot tell a priori. Refactoring into modules should normally reduce complexity, and thus make testing/verification easier. However, the definition of interfaces between the modules may end up introducing irregularity that was not there before, as well as seemingly introduce new behaviors.
Consider, for example, factoring out some code into a separate function/module. If somewhere else in the system an indirect function call exists, and the target of that call cannot be determined at compile time, the system now technically has a new connection between that call site and the newly factored-out function. Furthermore, if the new function takes a pointer as an argument, more connections are introduced between the function parameters and the data structures that pointer could alias.

### Which of the following statements is true?
- [x] An abstraction defines the behavior of a module
- [x] An abstraction excludes possible behaviors of a module
- [x] Abstraction is impossible without modularity
- [ ] Modularity cannot exist without abstraction
**Explanation**
The first two choices are duals of each other, and are correct by definition.
The third choice is correct because abstraction defines the behavior of a module, so it cannot exist without that module.
The fourth choice is not correct, and we saw an example of modularity without abstraction in the #define macro: it simply groups syntactically several program statements without definining what they actually do. Metaphorically speaking, one can encapsulate behavior into a box without defining what the encapsulated behavior is, in which case there is no abstraction.


### Which of the following statements is true?
- [ ] Abstraction specifies how a component is to be implemented
- [ ] Modularity specifies how a component is to be implemented
- [x] Modularity+abstraction enable decoupling functionality from implementation
**Explanation**
The first two choices are somewhat non-sensical, given the definitions of modularity and abstraction.
For the third choice, by using modularity and abstraction, we can encapsulate implementation into a module and use an interface to specify the abstraction that module implements.







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
- [x] The logical distance between any two vertices is short
- [ ] The physical distance between any two vertices is short
- [x] The number of edges per vertex follows a power-law distribution

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
