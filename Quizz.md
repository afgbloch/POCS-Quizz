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





## Week 2: Layering

### A layer typically:
- [x] is a well-defined module
- [x] exposes a specific abstraction
- [x] manages a namespace
- [ ] has to use a bus layer to communicate with other layers

**Explanation**
Buses are used to create stacks, but not required as part of a layer

### Which of the following statements is/are true?
- [ ] Stacking layers reduces the management complexity of a system.
- [x] Layering generally leads to strong separation of concerns in a system.
- [x] In a well-designed system, stacking layers decreases the number of dependencies among them.

**Explanation**
Increased management complexity is an emergent property of an overly-layered design. The separation of concerns is a natural consequence of the combination of modularity and abstraction property of the layer.

### The compute stack allows direct execution (layered bypass). Which of the following statements are true:
- [x] This improves systems performance
- [ ] The hardware guarantees that applications cannot tamper the OS
- [x] The OS must ensure that certain resource are never presented to the application
- [ ] The OS is fundamentally exposed

**Explanation**
Layered bypass, as architected in the compute stack, does not pose a fundmental problem. But only as long as the OS correctly prevents the application's access to critical resources.

### In the information stack:
- [ ] filesystems and volumes are interchangeable
- [x] filesystems are layered on top of volumes
- [ ] volumes and filesystem present the same abstraction

### Can a database be deployed directly on a raw disk drive ?
- [x] Yes: the filesystem and volume management layer don't exist in this instance
- [ ] Yes: because of layer bypass
- [x] Yes: because the operating system can expose a raw disk directly
- [ ] No. This is impossible.

**Explanation**
In that mode, there is no filesystem and no OS-managed volume, hence no bypass. It is however absolutely possible for a DB (or any program) to directly interact with a raw block device.

### SCSI is
- [x] an RPC protocol
- [x] the interface exposed by rotating disks and SSD
- [ ] a filesystem driver
- [ ] exposed by VFS

### In a client/server model:
- [ ] client and server run on separate machines
- [x] client and server communicate through a communication channel
- [x] a client cannot access server's memory directly
- [ ] a client has to get restarted if the server fails

###  When sending an RPC, a client may:
- [x] guarantee that the call is executed at least once
- [x] guarantee that the call is executed at most once
- [x] guarantee that the call is executed exactly once

###  When an HTTP client receive a 404 (file not found)
- [ ] this indicates a failure in the "at most once" semantic of HTTP
- [ ] this indicates a failure in the "at least once" semantic of HTTP
- [x] the RPC succeeded

**Explanation**
The HTTP protocol has "at most once" semantics. Which means, that in the absence of a reply, the command will have been applied zero or more times. A 404 simply indicates that the URI is not present on the server. But the client did receive a reply, and the RPC succeeded.

### How many layers are there in the network model?
- [ ] 3
- [ ] 5
- [ ] 7
- [ ] 8
- [x] it depends on who is counting

**Explanation**
"But mine goes to 11" (Spinal Tap)

### Techniques like mapped or recursive composition are used to:
- [x] provide compatibility
- [x] provide extended functionality
- [ ] used mainly in academia
- [ ] add a fourth layer to the 3-layer networking stack

### When a switch is also a router, then:
- [ ] this is a case of layer bypass
- [x] the device supports multiple protocols
- [ ] the device becomes the end-to-end layer
- [ ] the device support all 3-layers (of the 3-layer model)

###  When a link fails in the middle of the network
- [ ] the host's link layer is affected
- [x] the link layer of two routers is affected
- [ ] the link layer of >2 routers can be affected
- [ ] the state of two routers is affected
- [x] the state of at least two routers is affected





## Week 3: End-to-End Principle

### Choose functions that can't be implemented in the network alone according to the end-to-end argument:
- [ ] multicast routing
- [x] in-order data delivery
- [ ] packet fragmentation
- [x] reliable data delivery
- [ ] capacity reservation
- [x] duplicate suppression

### What can be and end point for the end to end argument:
- [x] a user of a system
- [x] an end host
- [x] a process

**Explanation**
They all can be considered as end points, depending on the system.

### Which of the following processor design approaches follows the end-to-end principle?
- [ ] complex instruction set computing (CISC)
- [x] reduced instruction set computing (RISC)
- [ ] both
- [ ] none, the end-to-end argument is not applicable to processor design

**Explanation**
The RISC argument is that the user of the architecture will get better performance by implementing only the basic instructions needed by everyone, efficiently and using primitive tools; any attempt by the computer designer to anticipate the user's requirements for an esoteric feature will probably (1) miss the target slightly (2) sacrifice the performance of commonly used features and (3) the user will end up reimplementing that feature anyway. Any unnecessary feature once added to the ISA highly likely stays there forever, due to the backward-compatibility requirement.

### What could be a valid reason for implementing a function at layer X even though it needs to be implemented at a higher layer anyway?
- [ ] enforcing authority
- [x] optimizing performance
- [ ] ensuring security





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





## Week 7: Virtualization

### Virtualization:
- [x] is a layer that exposes the same abstraction as the layer below
- [ ] is a layer that hides the abstraction of the layer below
- [x] provides isolation
- [ ] provides fault tolerance
- [x] ensures modularity
- [ ] increases complexity

**Explanation**
Virtualization is a layer that exposes the same abstraction as the layer
below. It also hides the physical names used in the layer below providing
isolation, ensures modularity and reduces the complexity of computer systems.

### Choose examples of application of virtualization:
- [x] threads
- [ ] CPUs
- [x] virtual memory
- [ ] physical memory
- [ ] von Neumann architecture
- [x] sockets
- [x] virtual machines

**Explanation**
A thread is a virtual CPU core, socket virtualizes a link and virtual memory
virtualizes the physical memory. Virtual machines are a canonical example of
virtualization, providing an abstraction of the underlying hardware.

### Choose correct statements:
- [x] Multiplexing can expose the same resource multiple times
- [ ] Multiplexing can expose multiple resources as a single resource
- [ ] Aggregation can expose the same resource multiple times
- [x] Aggregation can expose multiple resources as a single resource


### As a form of virtualization, emulation is used to:
- [x] execute code written for other ISAs
- [x] implement RAM disks
- [ ] reduce the overhead of other virtualization mechanisms
- [x] enable the Java Virtual Machine

**Explanation**
Emulation is a software technique that provides an abstraction of a virtual
resource radically different than the physical resource. Examples of frequently
emulated resources include hardware components (e.g., RAM disk) and non-native
code (e.g., other ISAs, Java bytecode). It is considered the slowest
virtualization mechanism as it typically lacks hardware support.

### A virtual machine:
- [x] is a duplicate of a real machine
- [ ] is an isolated operating system
- [ ] allows to run programs with improved performance
- [x] allows to run programs with minimum decrease in speed
- [x] can share the same physical machine with other virtual machines

**Explanation**
A virtual machine is an isolated, efficient duplicate of a real machine that
exposes similar resources as the real machine. An efficient implementation must
not have significant effect on application performance. Many VMs can run in
isolation on the same physical machine.


### People lost interest in virtual machines in 1990s because:
- [ ] they required hardware support that is not provided
- [ ] they limited operating system's functionality
- [x] the operating systems seemed to offer better opportunities for innovation
- [ ] they were inefficient

**Explanation**
People did not see any reasonable use cases for virtual machines.

### A virtual machine monitor (VMM):
- [x] has absolute control over the system
- [ ] introduce significant application slowdown
- [ ] is more complex compared to operating systems
- [ ] can coexist with other VMMs on the same machine in isolation
- [x] can be more easily adapted to hardware compared to an operating system

**Explanation**
A virtual machine monitor has absolute control over the system. As such, there
can be only one VMM per machine. An efficient implementation, with hardware
support, introduces minimal performance overhead, if any. It implements much
less functionality compared to operating systems, and therefore is less complex
and easier to change.

### A virtual machine monitor:
- [ ] emulates CPUs
- [x] emulates IO devices
- [ ] emulates memory
- [x] multiplexes CPUs
- [x] multiplexes memory
- [ ] multiplexes IO devices

**Explanation**
Each VM sees an abstraction of its own CPU cores and physical
memory. IO devices like network device or keyboard are emulated in software.

### A virtual machine monitor layer:
- [ ] lies between an application and an operating system
- [x] lies between an operating system and hardware
- [x] allows application to issue instructions directly on a CPU
- [x] allows an operating system to issue instructions directly on a CPU
- [x] can issue instructions directly on a CPU

**Explanation**
A VMM is a layer between the operating system and the hardware, but it allows
for a bypass between OS and a CPU as well as application and a CPU. This is
called direct execution.

### To access the host physical memory, a VM:
- [ ] relies on an operating system modified by a VMM
- [ ] bypasses a VMM directly to the host memory
- [x] requires an additional level of indirection, mapping the guest physical
  addresses to host physical addresses
- [x] may use shadow page tables
- [ ] may use cloned page tables
- [x] may use nested page tables

**Explanation**
The physical memory addresses observed in a VM need to be translated to host
memory addresses. Such a mapping can be realized by shadow or nested page
tables.

### Shadow page tables:
- [ ] require architectural support
- [x] require a VMM to keep a mapping between each page in the VM page table and
  a corresponding page in the VMM page table
- [ ] require two hardware to walk through two page tables at the same time

###  Nested page tables:
- [x] require architectural support
- [ ] require a VMM to keep a mapping between each page in the VM page table and a
corresponding page in the VMM page table
- [x] require the hardware to walk through two page tables at the same time

### Choose correct statements:
- [x] Type I VMM perform resource scheduling
- [ ] Type II VMM perform resource scheduling
- [ ] KVM is an example of Type I
- [x] Xen is an example of Type I
- [ ] VMware Workstation is an example of Tpe I

**Explanation**
Type I VMM allocate and schedule physical resources. The examples of this VMM
type include: Xen, VMware vSphere and Microsoft Hyper-V. Both types are equally
popular.

### A virtual machine monitor can provide direct execution only if:
- [ ] all OS instructions are privileged
- [x] all sensitive instructions are privileged
- [ ] no sensitive instruction is privileged
- [ ] no sensitive instruction can cause a trap
- [ ] semantics of sensitive instructions vary based on the privilege level

**Explanation**
According to the Popek/Goldberg theorem, a virtual machine monitor can provide
direct execution only if if the semantics of those instructions is not a
function of the privilege level, i.e., if all sensitive instructions are
privileged and cause a trap.

### Disco aims to:
- [x] allow many VMs running on a machine with ccNUMA architecture
- [x] perform resource management along with resource multiplexing
- [ ] allow a single VM to run on multiple connected machines
- [x] avoid unnecessary replication of data in memory
- [ ] limit the CPU utilization
- [x] optimize locality

**Explanation**
Disco is a VMM that allows many VMs to share the same ccNUMA machine. Besides
resource multiplexing, it performs resource management (type II). Disco solves
two memory related challenges: minimizes memory overheads and optimizes locality.

### Double swapping problem occurs when:
- [ ] a guest OS and then a VMM swap out the same page
- [x] a VMM and then a guest OS swap out the same page
- [ ] a guest OS and then a VMM swap the same page in
- [ ] a VMM and then a guest OS swap the same page in

**Explanation**
Double swapping problem occurs when first, a VMM swaps out a page X. Then, a
guest OS decides to swap out the same page as it doesn't know the page is
already swapped. As a result, the VMM needs to first swap the page X in, just to
swap it out again.

### To allow VMs for network communication, Disco:
- [ ] implements its own networking stack
- [x] emulates a software Ethernet switch
- [x] emulates a NIC for each VM
- [ ] requires multiple copies of data to transport a packet between VMs

### Efficient memory resource management becomes increasingly important in virtualized environment because:
- [x] memory footprints of virtual machines keep increasing
- [x] virtual machine migration happens more and more frequently
- [ ] of the increasing complexity of virtual machine monitors
- [x] of the increasing number of virtual machines hosted by a physical machine

### Disco’s copy-on-write approach achieves savings in:
- [ ] memory bandwidth
- [x] memory capacity
- [ ] the number of delta disks
- [ ] the capacity of delta disks
- [x] shared disk bandwidth
- [x] shared disk capacity

**Explanation**
By enabling sharing with the copy-on-write semantics both for memory and disk, Disco saves on memory capacity, and as a side effect, on disk capacity. Page sharing avoids reading the same content from the disk, reducing the disk bandwidth.





## Weak 8: Data Center Systems

### Every day in 2012 Amazon was increasing its compute capacity by the same amount as:
- [ ] it did every year in 1990s
- [x] Amazon.com needed for 5 years in 1990s
- [ ] the global computing capacity in 1990s
- [ ] Amazon.com needed between 1994 and 2012

**Explanation**
This piece of information was really highlighted in the video. If you got it
wrong, please watch the lecture one more time because you clearly were not
paying attention.

### Moore's law applies to:
- [x] the semiconductor density
- [x] the economy of scale
- [ ] network hardware ASICs
- [x] memory

**Explanation**
Moor's law applies to various areas of computer science, not only to numbers of
transistors. Innovation in technology makes it possible to quickly improve
parameters of other components as well.

### Compared to the number of personal computers, the estimated total number of computers in all data centers worldwide:
- [x] is significantly lower
- [ ] is comparable
- [ ] is significantly higher
- [ ] is impossible to compare

**Explanation**
Despite the size of each data center, there are still much less computers there
than there are desktops and mobile devices.

### Price of building and maintaining a data center can be lowered by:
- [ ] using specialized, custom made server parts
- [x] using commodity, general purpose server parts
- [ ] using specialized networking equipment
- [x] using commodity networking equipment

**Explanation**
It is cheaper to build a data center out of commodity parts. Even though they
individually do not guarantee high reliability, fault tolerance or high
performance, the low price make it possible to buy many such parts. Then, such
features are provided using redundancy and replication.

### What are the main differences between the Giant Scale Service architecture in 2001 and nowadays:
- [x] service no longer needs to be located in a single data center
- [ ] load balancers are no longer used
- [x] RAID replaced by 3-way replication
- [x] the network design
- [ ] lack of clients

### Fault tolerance and performance metrics relevant for cloud services measure:
- [ ] the number of running servers
- [x] the fraction of queries a service is able to process
- [x] the fraction of data available in the service
- [ ] the time since the last failure happened in the service
- [ ] the fraction of correct search results

### Assume that the amount of data used to respond to a query increases 2 times,while the system's capacity stays constant. The query rate for this system:
- [ ] decreases n times
- [ ] decreases 4 times
- [ ] decreases 2 times
- [ ] stays unchanged
- [ ] increases 2 times
- [ ] increases 4 times
- [ ] increases n times
- [ ] it is impossible to tell

**Explanation**
According to the DQ "principle", the number of queries per second times data per
query is constant.

### A system uses 10 storage nodes. The administrator adds 10 additional storage nodes.
- [ ] yield increases 10 times
- [ ] yield increases 2 times
- [ ] yield stays the same
- [ ] yield decreases 2 times
- [ ] yield decreases 10 times
- [x] it is impossible to tell

**Explanation**
It depends whether the storage is the system's bottleneck or not.

### The CAP theorem states that a distributed system cannot achieve all of the following properties at the same time:
- [ ] high Concurrency
- [x] Availability
- [ ] high Performance
- [ ] Composability
- [ ] tolerance to network Attacks
- [x] tolerance to network Partitioning
- [ ] eventual Consistency
- [ ] Atomicity
- [ ] tolerance to network Congestion
- [x] strong Consistency

**Explanation**
The CAP theorem states that a distributed system can achieve at most two of the following properties: strong Consistency, high Availability, and tolerance to network Partitioning.

### Systems/protocols that achieve consistency and tolerance to network partitioning, but compromise availability, include:
- [ ] Dynamo
- [ ] single-site Oracle databases
- [ ] DNS
- [x] majority protocols
- [ ] Web Caching

### The CAP theorem:
- [ ] is a hypothesis generally believed to be true based on practical experience
- [x] has been proven to be correct
- [ ] claims that a system can achieve at least one of the three properties
- [ ] claims that a system can achieve at least two of the three properties
- [ ] claims that a system can achieve at most one of the three properties
- [x] claims that a system can achieve at most two of the three properties
- [ ] claims that a system can achieve all three properties

**Explanation**
CAP theorem claims that at most two out of three properties: Consistency, Availability and tolerance to network Partitions can be achieved by a system. This claim has been proven. The theorem cannot guarantee that any system achieves any of these properties. Bad design systems may fail to guarantee any of them.

### An on-line, distributed plane ticket selling system can achieve:
- [x] Consistency and Availability
- [x] Consistency and tolerance to network Partitions
- [x] Availability and tolerance to network Partitions
- [ ] Consistency, Availability and tolerance to network Partitions
- [ ] none of the above

**Explanation**
Such a system can achieve Consistency and Availability sacrificing tolerance to network Partitions and simply stop working in case of partition. It can also sacrifice Availability, by not selling tickets in one of the separated network partitions. Finally, the system may continue selling tickets in both partitions, but this may lead to inconsistent state (e.g., service sells the same seat in both partitions).

###  The latency of a cloud service:
- [ ] is of secondary importance if throughput is high
- [x] depends on the slowest subtask required to generate the response
- [x] can be characterized by the long tail

### The TCP incast problem:
- [ ] happens when a node sends a sub-request to many nodes
- [x] happens when a node receives a response from many other nodes at the same time
- [x] is usually caused by congestion on the link connected to the server
- [ ] is usually caused by overall congestion in the network
- [x] affects latency
- [x] affects throughput

**Explanation**
The incast problem usually happens when the server access link gets congested because of many responses coming to the same server at roughly the same time. This congestion, and resulting lost packets lead to significant drop in throughput and increase in latency.

### Consider a service that responds to queries in: 100ms for 800 out of 1000 queries, 150ms for 100 out of 1000 queries, 200ms for 80 out of 1000 queries, 250ms for 16 out of 1000 queries and 500ms for 4 out of 1000 queries. The 99th percentile latency of this service equals:
- [ ] 100ms
- [ ] 150ms
- [ ] 200ms
- [x] 250ms
- [ ] 400ms
- [ ] 220ms
- [ ] 117ms
- [ ] the median latency of this service

**Explanation**
The 99th percentile latency means that 99% of the queries can be answered at most in this time. Or in other words, if we sort response times and look the the 99th percent value in this seqiuence we get a 99th percentile latency. In this case 99% out of 1000 is 990, so the 99% latency equals 250ms. Note that many cloud scale services need to care about even higher percentile, for example 99.9

### Consider a service that responds to queries in: 100ms for 800 out of 1000 queries, 150ms for 100 out of 1000 queries, 200ms for 80 out of 1000 queries, 250ms for 16 out of 1000 queries and 500ms for 4 out of 1000 queries. The 50th percentile latency of this service equals:
- [x] 100ms
- [ ] 150ms
- [ ] 200ms
- [ ] 250ms
- [ ] 400ms
- [ ] 220ms
- [ ] 117ms
- [x] the median latency of this service

**Explanation**
Following the explanation for the previous question, the 50th percentile latency for this service equals 100ms. Median is by definition equal to 50th percentile.





## Week 9: Redudancy and Fault-Tolerance

### Redundancy through coding can by achieved by:
- [ ] mirroring
- [x] using checksums
- [ ] replication of content
- [x] adding nonessential information

**Explanation**
Redundancy through coding relies on adding additional information to the encoded data. This information is not essential to read the data, but it helps detecting and recovering from errors. A checksums is an example of such additional information.

### Choose examples of incremental redundancy techniques:
- [x] CRC
- [x] TCP checksum
- [ ] starting a new HDFS node when the old one fails
- [ ] RAID 1
- [x] RAID 5

**Explanation**
Incremental redundancy increases the data size by just a small percent. CRC and TCP checksum achieve redundancy by encoding additional information. RAID 5 requires just 1 additional disk to provide redundancy.

### In computer systems, data replication can be used to:
- [x] increase data durability
- [x] detect errors in data values
- [x] discover correct data values
- [ ] reduce the probability of data corruption in one replica.

**Explanation**
The probability of data corruption in one replica is independent from that in other replicas.

### Choose techniques that are used to avoid faults.
- [ ] redundancy through coding
- [ ] redundancy through replication
- [ ] error containment
- [ ] error masking
- [x] none of the above

**Explanation**
They are all techniques used in fault tolerance. Fault avoidance is impossible.

### A fault tolerance process requires:
- [x] error detection
- [x] error containment
- [ ] error amplification
- [x] error masking
- [ ] error propagation

**Explanation**
As explained in the video, fault tolerance requires each module to perform error detection, containment and masking.

### Failures are
- [ ] faults that are latent.
- [ ] faults that are masked.
- [x] faults that turn into errors.
- [ ] faults that are detected.

**Explanation**
Failures are caused by active faults that cannot be detected or masked.

### Error-correcting code memory can:
- [ ] detect but not mask single-bit errors
- [x] detect and mask single-bit errors
- [x] detect but not mask double-bit errors
- [ ] detect and mask double-bit errors

**Explanation**
See the "Responding to active faults -- example" slide.

### Tandem computer systems achieve single fault tolerance using:
- [ ] only reliable hardware and software modules with negligible chances of failure
- [x] replicated hardware modules
- [x] redundant paths between hardware modules
- [x] process pairs with synchronized states

**Explanation**
See the "Tandem NONSTOP Mechanisms" slide.

### Enforced modularity is used to
- [ ] simplify errors
- [x] enable errors containment
- [ ] mark errors

**Explanation**
Enforced modularity provides state isolation between different modules, enabling to contain detected errors within a part of the system before they affects the states of other modules.

###  If a component's failure rate follows the bathtub curve:
- [x] if is likely to fail at the beginning of its use
- [ ] it is unlikely to fail at the beginning of its use
- [ ] the probability of a failure grows linearly with time
- [ ] the probability of failure grows exponentially with time
- [ ] the probability of failure starts high and decreases with time

**Explanation**
The bathtub curve has a shape of a bathtub. It is high at the beginning and at the end and is low in the middle.

### The availability of a computer system is 95%. What is the availability of the system after halving the mean-time-to-repair (MTTR)?
- [ ] 95%
- [x] 97.4%
- [ ] 97.5%
- [ ] 99%
- [ ] it depends on additional variables

**Explanation**
Let F=MTTF, R=MTTR. Then R/(R+F) = .05 = 1/20, and F=19R.
If R' = R/2, then downtime= R'/(R'+F) = 0.5xR / (0.5xR+19R) = 0.5/19.5.
Availability works out ot 97.4%

### Say you have two hard drives with MTTF of 100 years connected into RAID-0 (zero redundancy) array. What is the MTTF of the array ?
- [x] less than 100 years
- [ ] = 100 years
- [ ] more than 100 years

**Explanation**
The zero-redundancy system will survive only as long as all of its components are operational, hence its MTTF is smaller than the smallest among the components MTTF (or equal to it, if the probability distribution is singular, but that is not the case for hard drives).

### Separating durable and transient application state to provide high availability:
- [x] uses the sweeping simplification principle
- [ ] provides a hot spare
- [x] avoids creating a synchronized application replica
- [ ] makes it impossible for an application and the storage to fail at the same time

**Explanation**
H/A applies the sweeping simplification principle by simply ignorning all transient state, and rebuilding it upon failure on the spare by using only the durable state.

### Recovery-oriented computing aims to:
- [x] minimize MTTR
- [ ] minimize MTTF
- [x] increase availability
- [x] reduce the harmful effects of software bugs

**Explanation**
Recovery-oriented computing recognizes software bugs as inevitable and aims to reduce their harmful effects. This approach shortens the application recovery time, which in turn increases availability.

### SCSI Reservations are often used to:
- [x] ensure consensus between the nodes on who is the active node (and who is the passive)
- [ ] ensure the durability of data
- [x] signal a change of active node
- [x] avoid split-brain syndrom

**Explanation**
The SCSI reservation mechanism will reject any write from a server that does not have the latest "key". This provides atomicity in takeover (each disk write is a transaction), and ensures consensus between the nodes as to who is the primary.

### Choose the key properties of consensus:
- [x] agreement
- [ ] durability
- [x] integrity
- [ ] majority
- [x] termination
- [x] validity

**Explanation**
agreement - no two nodes decide differently
validity - if all correct nodes propose the same value, they all choose this value
termination - every correct node finally decides
integrity - every correct node decides at most once and what it decides must have been proposed by some node

### Select examples of Byzantine Failures:
- [x] not sending a message that you're supposed to send
- [x] sending an incorrect message because of a bug
- [x] sending an incorrect message on purpose
- [x] nondeterministically sending correct and incorrect messages
- [ ] when the entire system crashes
- [ ] when nodes in a system can't reach consensus

**Explanation**
A Byzantine Failure is any incorrect behavior of system's node. Whether on purpose or not.

### What is the minimum of replicas that a system needs in order to be able to reach consensus in the presence of n Byzantine failures (in the general case)?
- [ ] n + 1
- [ ] 2n
- [ ] 2n + 1
- [x] 3n + 1

### A fault-tolerant system using 7 replicas can survive at most:
- [ ] 2 simultaneous "fail-stop" failures
- [x] 3 simultaneous "fail-stop" failures
- [x] 2 simultaneous Byzantine failures
- [ ] 3 simultaneous Byzantine failures

**Explanation**
BFT requires (3f+1) nodes. But distributed processes that operate in a fail-stop manner only require majority (2f+1)

### Consensus in a distributed system is used to
- [x] detect failures
- [x] recover from failures
- [x] ensure consistency of the system
- [ ] improve performance of the system

### How does consensus related to agreement?
- [ ] agreement subsumes consensus
- [ ] agreement and consensus are the same
- [x] consensus subsumes agreement correct

### In the synchronous model of a distributed system, how could we model the corruption of messages while in-transit on a network link between two nodes?
- [x] as a corruption of the message occuring at the sending node
- [x] as a corruption of the message occuring at the receiving node
- [ ] it is not possible to model Byzantine links in the synchronous model
- [x] can introduce an intermediary node that receives the correct message and forwards the corrupt version

### A stamp in Windows Azure Storage:
- [ ] relies on high-end fault tolerant hardware to ensure high availability
- [ ] should scale to hundreds or thousands of racks
- [x] keeps replicated copies of data
- [ ] is geographically distributed

**Explanation**
A stamp in Windows Azure Storage is a storage unit that spans 20-30 racks. It uses commodity hardware but provides high availability by replicating data. A single stamp is not geographically distributed, but multiple geographically distributed stamps keeps copies of the same data to provide high availability.

### When does the split brain syndrome occur:
- [ ] as a consequence of data corruption
- [x] in circumstances that can lead to data corruption
- [x] when both the primary and backup servers simultaneously conclude they are the primary server
- [x] when corpus callosum connecting the two hemispheres of the brain is severed to some degree (in the medical field)

### Which of the following statements are true:
- [x] Vertical scaling assumes shared hardware components
- [ ] Vertical scaling requires a process-pair design
- [x] Horizontal scaling is generally more cost-effective
- [ ] Vertical scaling generally uses a scale-out server deployment model

**Explanation**
H/A clusters (not only process-pairs) run on vertically-scaled hardware.
Vertical scaling is associaed with scale-up server designs. Horizontal scaling = scale-out.

## Week 10: Fault Tolerant services and the transaction concept
### No video lecture.

## Week 11: Verification and Testing

### Domain specific languages are developed to:
- [ ] limit the wide applicability found in general-purpose languages
- [x] provide more appropriate abstractions to the programmer for a particular domain
- [x] increase programmer productivity
- [ ] reduce compiler construction efforts
- [x] provide expressive power in the target domain in a compact manner 

### Language virtual machines are primarily used to:
- [x] support late binding
- [ ] improve performance
- [x] allow late compilation
- [ ] avoid interpretation
- [ ] virtualize resources
- [x] improve portability 
**Explanation**
The goal of the language virtual machines is not to virtualize resources. Although important, performance is not the primary purpose of language VMs. 

### Staged compilation:
- [x] is organized as a series of stages
- [ ] can improves performance, but compromises bytecode portability
- [x] allows for hardware-specific optimizations
- [x] provides better memory protection 
**Explanation**
Staged compilation is organized as a series of stages, with the final stage taking place at runtime, allowing for runtime memory checks and low-level optimizations. 

### Programs written in high level languages can run faster than programs written in low level languages because:
- [x] compilers may be better at optimizing than humans
- [x] higher level abstractions allow for more flexible optimizations
- [ ] they are shorter
- [ ] none of the above. 

### Which of the following do exist:
- [x] a program that can write itself
- [ ] a program that can decide if another program always terminates
- [ ] a Turing machine that can decide if another Turing machine always terminates
- [x] a compiler for language L written in language L 

### Declarative languages:
- [ ] precisely specify the control flow of a program
- [x] express what a program should do
- [ ] express what a program can do
- [x] include, for example, SQL and Scala
- [ ] include, for example, Java and C++ 
**Explanation**
Declarative languages specify what a system should do, describing the logic of a program without describing the implementation. Examples include SQL and functional languages, such as Scala. In contrast, imperative languages, such as Java or C++, are used to describe the implementation, typically through program control flow. 

### Choose the benefits of using declarative languages compared to imperative languages:
- [x] they are easier to program with
- [ ] they are more expressive
- [x] they give better opportunity for optimization
- [ ] programs are more modular
- [x] they are more robust 

### First-order logic permits:
- [x] simple predicates (e.g., “A holds only if B does not”)
- [x] existential quantifiers (e.g., “there exists”, “for some”)
- [ ] qualifiers such as “possibly”, “necessarily”
- [x] universal quantifiers (e.g., “for every”, “given any”)
- [ ] qualifiers such as “always”, “eventually” 
**Explanation**
First order logic extends propositional logic with the universal and existential quantifiers. Expressions that qualify the truth, such as “possibly” and “necessarily” belong to modal logic, or to temporal logic, if relate to time (e.g., “always”, “eventually”).

### What is true about relations in Datalog:
- [x] Relations from extensional database (EDB) can appear only in the body (right-hand side) of a program rule
- [ ] Relations from EDB can appear only in the head (left-hand side) of a program rule
- [ ] Relations from EDB can appear both in the body and the head of a program rule
- [ ] Relations from intensional database (IDB) can appear only in the body
- [ ] Relations from IDB can appear only in the head
- [x] Relations from IDB can appear both in the body and head 
**Explanation**
EDB includes the knowledge base, i.e., known facts. Thus, EDB relations cannot appear in the head of a rule. In contrast, IDB includes inferred facts. As such, IDB relations can appear in both in the body or in the head of a program rule.

### Compare the three ways to define the semantics of Datalog programs:
- [ ] The model-theoretic semantics is superior as it seeks to find the MINIMUM set of facts that satisfy the program’s rules
- [ ] The fixpoint semantics is the most complete because it computes ALL facts that can be proven based on the program’s rules and known facts through an iterative process
- [ ] The fixpoint semantics is superior because it evaluates Datalog programs in a bottom-up manner
- [ ] The proof-theoretic semantics is superior because it evaluates Datalog programs in a top-down manner
- [ ] The proof-theoretic semantics is superior because it elegantly constructs new facts using trees
- [x] All the three approaches give the same semantics 
**Explanation**
Although not obvious, all the approaches to giving semantics to Datalog programs are equivalent. The semantics of Datalog is independent of the evaluation mechanism, which can be either top-down or bottom-up.The top-down evaluation naturally follows the definition of the proof-theoretic semantics, while the bottom-up approach is based directly on the fixpoint semantics.

### According to the closed world assumption:
- [ ] facts not in the database have to be false
- [x] facts that are neither in the database nor can be inferred are considered false
- [ ] facts that cannot be proven are considered unknown 

### Prolog:
- [ ] is a fully declarative language
- [x] is Turing-compete
- [ ] has the fixpoint semantics
- [x] is more succinct compared to C
- [ ] cannot express everything that a language such C can express
- [ ] can express more compared to C 
**Explanation**
Prolog is a Turing-complete language, and as such can express everything that can be expressed in C, but in a more succinct way. It uses the proof-theoretic semantics. However, Prolog contains imperative elements, such as operator "cut", which requires the programmer to think about Prolog internals. As such, Prolog is not a fully declarative language. 

### Mark all correct statements:
- [x] Adding more facts to the knowledge base in Datalog never gives fewer results
- [ ] Adding more facts to the knowledge base in Datalog can give fewer results, because Datalog supports negations
- [ ] Non-monotonic logic has no practical importance, as it gives multiple minimal models as solutions
- [x] Answer set programming is more expressive than Datalog 
**Explanation**
Datalog supports monotonic logic, which means that extending the knowledge base always returns at least as many results as before.
Non-monotonic logic may result in multiple minimal models, each being a correct solution, but we can define an appropriate semantics that accepts such solutions.
Answer set programming, unlike Datalog, supports negation, and is able to express NP-hard problems in a very succinct way. 

### What properties should a well-designed declarative language have:
- [x] be easy to understand
- [ ] provide limited functionality
- [x] not have too high computational complexity
- [ ] allow for arbitrary computations 


## Security: 
### Why is it difficult to defend against computer attacks over the Internet?
- [ ] it is difficult to use many passwords
- [x] attacks are fast
- [x] attacks are cheap
- [ ] attackers rely on audits
- [x] attackers are well organized 

### Why is it difficult to prove that a system is secure?
- [ ] security properties are unspecified
- [x] it requires reasoning about all possible attack scenarios
- [x] one insecure component makes the entire system insecure
- [ ] attackers often choose one component and attack it until they succeed 
**Explanation**
To be 100% sure a system is secure, one needs to analyze all possible attack scenarios. This task is hard (often infeasible) to complete. It is enough that just one attack scenario succeeds to compromise the entire system. Moreover, it takes just one faulty component for the attacker to get access to the whole system. Finally, attackers often look for different weak points that, attacked together, may lead to a security problem.

### When specifying a security policy:
- [x] secrecy refers to who can read the data
- [ ] secrecy refers to who can modify the data
- [ ] secrecy refers to when the data is safe
- [ ] integrity refers to who can access the data
- [x] integrity refers to who can modify the data
- [ ] integrity refers to when the data is correct 

### Popular assumptions made in a threat model are that an adversary: 
- [x] can control some computers connected to the Internet
- [ ] can control all computers connected to the Internet
- [x] can control some software on computers belonging to other users
- [x] knows some other users' passwords
- [ ] an adversary can provide a system with insecure hardware 

### In the guard model, the guard implements the following functionalities:
- [x] correct identification of the user
- [x] authorization
- [x] deciding whether a particular user is allowed to perform the requested operation on the requested resource
- [x] authentication
- [ ] None of the above 
**Explanation**
The guard is responsible for authentication — i.e., identifying the user and verifying that the user is who they claim they are, and authorization, i.e., deciding whether a particular user is allowed to perform the requested operation on the requested resource.

### According to the principle of least privilege,
- [x] some component(s) of the system is (are) trusted
- [ ] no component of the system can be trusted
- [x] a minimal subset of components should be trusted to enforce the security policy
- [ ] every component should be responsible for enforcing the security policy
- [x] every piece of code on the server side should have the lowest privilege necessary to complete its function
**Explanation**
According to the principle of least privilege, the number of trusted components, the number of components responsible for the system security and the privileges any piece of code is granted should be minimal.

### Systems that follow the principle of least privilege
- [x] achieve better security as the system scales
- [ ] centralize all security-related functionality into one component
- [x] reduce the number of security bugs
- [ ] sacrifice modularity for security
- [x] are easier to reason about 
**Explanation**
The principle of least privilege decentralizes the security-related functionality, implementing it within the corresponding components, thus improving modularity. This leads to less complexity and, as a result, to better system scalability and fewer bugs.

### Mark all correct statements regarding security:System components should not provide security mechanisms; instead, policies should be implemented end-to-end
- [ ] Each policy must have its own mechanism(s)
- [ ] Policies and mechanisms should never be separated
- [x] Mechanisms should provide an efficient implementation for one or more policies 

### In password-based authentication: 
- [x] legitimate users must always be given access, once they authenticated correctly
- [ ] the adversary is not allowed to guess passwords
- [x] password guessing must be expensive 
**Explanation**
Password guessing must be the only way an adversary can try to authenticate themselves. Regardless of the number of guesses required for a correct guess, password guessing must be expensive in terms of time, preventing the adversary to perform many repeated attempts within a short amount of time. 

### The salting approach
- [ ] mitigates the collision problem found in cryptographic hash functions
- [x] makes password guessing more complicated in case of stolen databases of password hashes
- [ ] even if the database wasn't stolen, salting still makes password guessing more difficult
- [ ] assumes that each password is hashed, and the hash is stored along with a predefined key referred to as “salt”
- [ ] assumes that each password is hashed, and the hash is stored along with a random string referred to as “salt”
- [x] improves the security of weak passwords in case of stolen databases of password hashes
- [ ] improves the security of weak passwords unless the password database is stolen 
**Explanation**
 In the salting approach, each password is hashed together with a random string, and then stored in the database along with that random string ("salt"). In case the encrypted password database is stolen, this approach makes the guessing process (e.g., using rainbow tables) harder; the use of the random string makes weak passwords in particular hard to guess. 
 
### Session keys:
- [ ] completely avoid the use of passwords
- [x] are used to minimize the transmission of user credentials
- [ ] cannot be used by an adversary if stolen
- [ ] consist of the user ID, expiration time, and a user-known secret
- [x] consist of the user ID, expiration time, and a server-known secret 
**Explanation**
 Session keys consist of a combination of the user ID, expiration time, and a secret known only by the user. They are used to minimize the transmission of user credentials over the network. They can be used by an adversary if stolen, but only for a limited amount of time.

### The challenge-response protocol is used to:
- [ ] avoid the transmission of the username from a client to the server
- [x] avoid the transmission of the password from a client to the server
- [x] authenticate the client on the server side
- [x] authenticate the server on the client side
- [ ] prevent an adversary from tracking the communication between the server and the client
- [ ] prevent a man-in-the-middle attack 
**Explanation**
 In the challenge-response protocol, the password (or even a hash thereof) is never directly transmitted from the client to the server. Instead, the server sends a random string, to which the user replies with a hash of the concatenation of the password and the string. This prevents a man in the middle from obtaining the password, but it does not prevent him from taking actions on behalf of the user. It can be used by both the client and the server to authenticate each other. 
 
### The one-time password approach
- [ ] requires the user to reset their password upon every successful log in
- [x] relies on recursive hashing
- [ ] is resistant to man-in-the-middle attacks
- [ ] is used to prevent the adversary from inverting the hashed password
- [x] is used to prevent the adversary from reusing the learned (hashed) password
- [x] requires the user to hash their password recursively, a different number of times for every authentication 
**Explanation**
 The one-time password approach is used to prevent the adversary from reusing the learned password multiple times. It is implemented through recursive hashing, which means that the user always sends a password recursively hashed a number of times. The client and the server must be synchronized with respect to how many times the password is hashed. 
 
### When creating a threat model for networked systems it is usually assumed that an adversary can:
- [x] observe any network packet
- [x] modify any network packet
- [x] read the payload of any network packet
- [ ] make undetected modifications to any message 
**Explanation**
The main goal of security in networked systems is to ensure that an adversary cannot understand or silently modify messages exchanged by others even if an adversary can see and modify all packets.

### Message encryption: 
- [x] is mainly used to ensure secrecy
- [ ] is mainly used to ensure integrity
- [ ] is mainly used to ensure that an adversary cannot make undetected changes to a message
- [x] is mainly used to ensure that an adversary cannot learn the contents of a message
- [ ] is mainly used to ensure that an adversary cannot intercept messages
- [x] produces output that is typically at least as long as the message itself 
**Explanation**
 Encryption is used to ensure that an adversary cannot make learn the content of a message. Adversaries can read the encrypted content or even modify it, but cannot restore the original content without the encryption key. The output of encryption is usually slighly longer than the original unencrypted content.
 
### Message authentication codes (MACs): 
- [ ] are used to ensure secrecy
- [x] are used to ensure integrity
- [x] are used to ensure that an adversary cannot make undetected changes to a message
- [ ] are used to ensure that an adversary cannot learn the content of a message
- [ ] are used to ensure that an adversary cannot intercept messages
- [ ] are typically at least as long as the message itself 
**Explanation**
Message authentication codes are used to ensure integrity — i.e., that an adversary cannot make undetected changes to a message. A MAC is a message supplement and as such it does not prevent adversaries from intercepting, learning and modifying the content of messages. However, any modification to the original message will be detected. A MAC is essentially a hash of a message, and is typically shorter than the message itself.
 
### Select the main goals of secure channels:
- [ ] guarantee message delivery
- [x] guarantee message secrecy
- [x] guarantee message integrity
- [ ] guarantee in-order delivery
- [ ] avoid cryptography
- [x] prevent an adversary from replaying messages 

### Exchanging keys for the first time cannot be secure
- [ ] if done over a network
- [ ] if an adversary can observe all messages
- [ ] in case of a man-in-the-middle attack
- [x] none of the above 
**Explanation**
The basic Diffie-Hellman protocol allows to exchange keys securely even if an adversary can intercept all messages. It fails if an adversary uses a man-in-the-middle attack, but as hinted at the end of this lecture, it can be improved.

### If all messages between two communicating parties are digitally signed, an adversary:
- [x] can observe the content of the messages
- [x] can understand the content of the messages
- [x] can intercept a message from the sender and send them to another receiver
- [x] can reorder messages
- [ ] can modify the content of the message without detection
- [ ] None of the above 
**Explanation**
Digital signatures guarantee authenticity. An adversary can observe messages, reorder them and forward to other parties, and even understand the content, unless encryption is used. The adversary however cannot secretly modify the message because the signature of each message depends on its content. Updating the signature upon content modification is practically infeasible without the private key of the sender. 

### In the Diffie-Hellman key exchange protocol, digital signatures are used to:
**TODO**
- [ ] ensure privacy
- [ ] ensure secrecy
- [ ] ensure integrity
- [ ] prevent man-in-the-middle attacks
- [ ] avoid traditional handwritten signatures 
 
### Mark all correct statements about Secure Shell (SSH): 
- [ ] SSH is resistant to man-in-the-middle attacks
- [ ] the public key of the remote host is distributed by a central trusted authority
- [x] the public key of the remote host is provided by the remote host itself
- [x] the public key of the remote host is cached locally 
**Explanation**
In SSH, the public key of the remote host is provided by the remote host itself, which makes the protocol susceptible to man-in-the-middle attacks. Once obtained, the key can be cached locally.

### Digital certificates for entity E consists of
- [ ] E’s public key signed by E
- [ ] E’s private key signed by E
- [x] E’s public key signed by a certificate authority
- [ ] E’s private key signed by a certificate authority 
**Explanation**
Digital certificates for an entity contains its public key signed by a certificate authority.

### Certificate revocation lists are used 
- [ ] to update certificate expiration dates
- [x] to mitigate problems caused by certificate authority errors
- [x] to announce invalid certificates
- [ ] by certificate authorities to obtain public keys 
**Explanation**
 Certificate revocation lists are maintained by certificate authorities and include known invalid certificates. Such lists can mitigate problems caused by certificate authority errors in issuing certificates.
