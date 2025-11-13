# Explanation
## What is a transaction 
is a collection of queries that treat as one unit to finish some work
### Transaction Lifespan
- transaction begin
- transaction have some work in it
- transaction commit and finish its work
- or transaction rollback if any wrong happens
### Nature of Transactions
- basically transactions used to update or change data 
- sometimes you can use transaction to only read data, when you tell db that you will use it to only read data, it will take a snapshot for the time you ask about it and any changes will not affect it, like if you want a report you can use only read so changes after you request the report doesn't affect it
## Atomicity
it means all queries in transaction must succeed to commit the transaction, if any query failed for any reason, all queries in transaction must be rollback 
## Isolation
### Read Phenomena 
- dirty read: which is read data that other transactions wrote but didn't commit yet
- non-repeatable: reads which mean in same transaction you read row again and again, and it changes due to another transactions
- phantom reads: which mean you run the same query twice and in each time it read different rows each time due to another transaction insert or delete some rows
- lost updates: when two transactions read the same value, modify it, and one overwrites the other's changes, causing the first update to be lost
### Levels
- read uncommitted: allows reading uncommitted data from other transactions. No isolation - permits dirty reads, non-repeatable reads, phantom reads, and lost updates. Lowest isolation level.
- read committed: only reads committed data. Prevents dirty reads, but allows non-repeatable reads, phantom reads, and lost updates
- repeatable read: guarantees that row you've read won't change during your transaction. Prevents dirty reads and non-repeatable reads. Phantom reads may still occur (though some databases like MySQL/InnoDB prevent them).
- snapshot: each transaction works with a consistent snapshot of data as it existed when the transaction started. All reads see the same committed data throughout the transaction, even if other transactions commit changes. Prevents dirty reads, non-repeatable reads, and phantom reads.
- serializable: highest isolation level. Ensures the result is equivalent to transactions running serially (one after another), even though they may actually run concurrently. Prevents all read phenomena. Usually implemented with optimistic concurrency control or predicate locks.
### Database Implementation of isolation 
- Pessimistic (locking): Acquires locks (row-level, page-level, or table-level) before accessing data to prevent conflicts. Prevents lost updates by blocking other transactions. Can cause blocking and deadlocks but ensures safety
- Optimistic (no locks): Assumes conflicts are rare. Transactions proceed without locks, then validate at commit time whether data was modified by others. If conflicts detected, transaction aborts and must retry. Better performance when conflicts are uncommon
- Repeatable Read can be implemented with locks on rows read (expensive for large result sets) or with MVCC (Multi-Version Concurrency Control) which keeps multiple versions of data and is more efficient
- Serializable is often implemented with optimistic concurrency control (especially Serializable Snapshot Isolation/SSI), but can also use pessimistic techniques like predicate locks or range locks to prevent phantoms. Implementation varies by database.
## Consistency 
it means that after any transaction the data must be consistent due to some constrains that defined in database or by user, also it can take some time to be consistent like in distributed databases 
### In data
is that the data is consistent anyway and anytime, like if you have two tables and the second table have a foreign key from first, if we have in first sum and that sum is the count of rows in the second, so in second we must have same number of rows and sum and the reverse, if we have row in the second it's value must be counted in first 
### In reads
which means when one transaction commit, and you try to read a value changed by this transaction it must be the new one to be consistent
## Durability
it means that once a transaction is committed, the changes are permanently stored and will survive any system failure (crash, power loss, hardware failure, etc.).
Key Guarantee: If the database tells you "transaction committed successfully," that data is SAFE forever, even if the server crashes 1 second later.
### Durability Techniques
- WAL write ahead log: which is just save changes as logs and when you want to get the final data again you can just go with the log and make the changes in same order, and it will lead to last version of consistent data
- Asynchronous snapshot: which is in the background we save a snapshot of data at once to the disk from the memory
- AOF append only file: similar to WAL
## Eventual Consistency
it's the case when we have a distributed database instances, and we update value in the leader node so it takes some time to propagate the update to the follower nodes, and due to that time you maybe read the value, but the return is the old value as it not updated yet in this instance


# Source
[Fundamentals Of DB Engineering](https://www.udemy.com/course/database-engines-crash-course) 