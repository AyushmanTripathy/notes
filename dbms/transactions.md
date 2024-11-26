## Concurrency Control

### Transaction

single logical unit of work

### Schedule

series of operation from one or more transactions.

- Serial Schedule, one after another
- Concurrent Schedule, in parrallel

### problems

1. Lost update problem (w - w - c)
    - t1 reads and t2 reads 
    - both writes different then commit
1. Dirty Read problem (w - r - f)
    - t1 writes
    - t2 reads
    - t1 then fails and rollbacks
1. Unrepeatable read problem (r - w - r)
    - t1 reads
    - t2 writes
    - t1 reads again, different value this time

### Concurrency Control Protocols

1. Lock-based protocol
    - Shared Lock, only read
    - Exclusive Lock, write allowed
    - Two Phase Locking
        - Growing phase & Shrinking phase
    - Strict Two Phase Locking
        - release exclusive lock only after commit
    - Rigorous Two Phase Locking
        - relase all locks only after commit
1. Timestamp-based protocol
    - every transaction has timestamp attached
    - conflicts are resolved by timestamp

### Conflict Serializaility

- conflict pair, 2 transaction have atlest one write on same data item
- non conflict pairs can be swapped
- check if equivalent shedule is serial

1. Percedence Graph
    - start from first, until last
    - find conflict pairs in other transactions
    - draw directed edges
    - if cycle present, its conflict serializable
    - if not, can't say

### View Serializaility


### Deadlocks

two or more transaction waiting indefinitely for each other's resources.  

Prevention
- no cyclic wait, either all lock or none
- preemptive (requesting transaction has priority)
    - once another lock is request, transaction dies
- non preemptive
    - wait-die, wait if smaller timestamp
    - wound-wait, wait if larger timestamp

Detection

- wait-for graph has cycles

Recovery

- one of transaction has to be rollbacked
- maybe partial or total
- **Starvation**, is same transaction is alwayed rollbacked

## Recoverability

if a transaction fails, it has to be rollbacked.
any transaction that has read from the transaction also need to be rollbacked.

### Recoverable Schedule

if t1 reads from data written by t2.
commit of t2 must be before t1

### Cascading rollbacks

if a rollback, triggers a lot of rollbacks.

## ACID

### Atomicity

either the entire transaction completes, or none at all  
operation are,

- Abort
- Commit

Transaction Manager's resposibility

### Consistency

- refers to correctness of the database
- integrity constraints must be maintained before and after a transaction
- Application programmer's resposibility

### Isolation

- Transactions occur idependently without interference
- Concurrency control Manager's resposibility

### Durability

- A Transaction once commited must be permanent
- Recovery Manager's resposibility

## Recovery Techiniques

1. Log based recovery
    - Deferred Updates
    - Immediate Updates
1. Shadow Paging
    - copying db
