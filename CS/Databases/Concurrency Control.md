# Explanation

### Using Locks
have two operations lock and unlock 

#### Shared and Exclusive Locks
- Shared is same as Read Lock *S-Lock* 
- Exclusive is Write Lock *X-Lock* 
- Only Shared Locks can work together 
#### Two Phase Locking
- Phase 1 Growing
	- Transactions can acquire locks without releasing any locks they have
- Phase 2 Shrinking
	- Transactions can release locks without acquire new locks
#### Cascading Rollback
ways to solve it
- Strict 2PL
	- transactions can only release X-Locks only when ended "Committed or rolled back" 
	- prevents dirty read and cascading rollbacks
	- produces strict schedules 
- Strong Strict 2PL
	- transactions can only release all locks only when ended "Committed or rolled back" 
	- more restrictive than Strict 2PL
	- easier to implement 
#### Deadlocks
circle waiting between transactions locks
##### Deadlock Detection
build waits-for graph:
- each node is transaction 
- edge from Ti top Tj is waiting for lock held by Tj
- cycle mean there is a deadlock
how to solve:
- Victim Selection
	- select a transaction and kill it
	- possible criteria
		- Newest
		- The Least number of writes done
		- Number of locked items
		- The Least number of rollbacks
		- etc.
##### Deadlock Prevention
try to avoid deadlock from first
how to:
- Conservative 2PL
	- Transaction request all locks at first
	- if any lock is unavailable don't acquire any locks
- Timestamp Based
	- Each Transaction has a timestamp ts
	- if transactions request a lock held by another one, either block or abort one of them based on ts

#### Lock Hierarchy
- Database not very common
	- Table Very common
		- Page common
			- Row Very common
				- Attribute rare

#### Intent Locking
new type of locks which is a lock acquired on a higher level object to allow the transaction to lock a lower level object

##### Types:
- Intent Shared Lock (IS)
	- intent to get S-Locks at lower level
- Intent Exclusive Lock (IX)
	- intent top get X-Locks at lower level
- Shared + Intent Exclusive Lock (SIX)
	- S-Lock at higher level, intent to get X-Locks at lower level

![](Pasted%20image%2020250426192009.png)

#### Explicit Locking
Manual lock table my DBMS



# Sources
[Amr Elhelw Lec1](https://youtu.be/s8w-GplT6K4?si=uJ0bFfsqEp1sR_gY) 
[Amr Elhelw Lec2](https://youtu.be/4Ll7zlC9f4w?si=Vjp2gB6MEWyrzs0H) 