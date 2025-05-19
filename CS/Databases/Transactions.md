# Explanation
Transactions: some operations grouped to serve some goal and must be done in same order and sequential, and must be done all, or it will be failed 
## ACID Properties
Some properties that have to be in any transaction, but not all are important
- A for Atomicity
	- All or nothing
	- that means the full operations in the transaction must be done or if anyone failed the hole transaction will be failed
- C for Consistency
	- After any transaction the data must be valid due to constrains that defined for this table or this DB
	- Eventual Consistency
		- That mean the data can be consistent but not directly, it can take some time like in distributed databases
- I for Isolation
	- Transactions don't affect each other
	- Lost Update
		- The last update cover all updated that happened, so the final value is totally wrong
	- Dirty Read
		- read value that updated in other transaction but still not committed 
	- Non-Repeatable Read
		- each time you read it have a new value
	- Isolation Levels
		- Read uncommitted
			- No Isolation
			- Any Transaction can read uncommitted data even if this transaction is failed
		- Read Committed
			- Each operation in transaction can only rad committed data
			- still more than one operation can read different values each time
		- Repeatable read
			- only read thing committed before cur transaction 
		- Serializable
			- work as each one is alone
- D for Durability
	- anything committed must be available even if there is bad happened 
## Schedules
Some order of operations in the transaction, each different order is a different schedule 
- Conflicting Operations
	- Must have some conditions to happen
		- They belong to different transactions
		- they access the same object
		- at least one of them is writing operation 
	- Read-Write conflict
		- it's a read op then a write op with the same variable
	- Write-Read conflict
		- it's a write op then read op with the same variable
	- Write-Write conflict
		- it's a two write op with the same variable
- Schedule Recoverability
	- Recoverable Schedule
		- if T1 writes X then T2 read/write X then T1 must commit before T2
	- Cascading Rollback
		- one transaction is roll backed, and you have to rollbacks some other transaction because it
	- Cascading Schedule
		- Subset of recoverable with no cascading rollback 
			- for any W/R the first transaction must commit before the second one read
	- Strict Schedule
		- Subset of cascadeless with stricter conditions 
			- not only for W/R like cascading, we will check for W/R and also W/W 
	- ![](Pasted%20image%2020250402073343.png)
- Schedule Serializability 
	- Serial Schedule
		- no intersect between transactions
		- n! Possible schedules for n transactions
	- Serializable Schedule
		- a Schedule that is equivalent to a serial Schedule 
		- Types of equivalence 
			- Conflict Equivalence
				- we say two schedule are conflict equivalence if the order of conflicts are same in the two of them
		- if schedule that is conflict equivalent to serial schedule we say it's a *Conflict Serializable* 
		- Conflict Serializable: it's a schedule that we can reorder some operations in it so we can make it a serial schedule
	- Dependency Graph 
		- a directed graph where each node is a transaction and each edge is just a conflict operation
		- if the graph have a cycle we say it can not be serial
	- ![](Pasted%20image%2020250402080106.png)

---
# Sources
[Amr Elhelw Lec1](https://youtu.be/ziH5Y4tvQJE?si=8N4E9VKeulAZYuYM)
[Amr Elhelw Lec2](https://youtu.be/KRZTwTWiUek?si=d23IKvtMOj_TDOns) 