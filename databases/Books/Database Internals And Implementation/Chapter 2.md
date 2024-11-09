## Terminology
- T(n) : n-th transaction
- S(n) : n-th select operation
- U(n) : n-th update operation
## Problems without Transaction Isolation
- Dirty read:
	- T1 has some updates to a row
	- T2 reads the changes made by T1 even before T1 commits (not still in progress, T1 would have completed executing all it statements)
		- DOUBT: Is it actually just before `commit`? Does this term cover just that case?
	- This become problematic if T1 rollbacks, cause then T2 read the wrong data
- Non repeatable reads:
	- T1 reads same data multiple times, let's say two times S1 & S2, so T1 is made up of two queries: S1 S2
	- T2 updates after S1 but before S2
	- T1 gets different data for same read
	- Note that here we are talking about interaction between two distinct transactions and not within a single transaction
	- A good way to think about it:
		- Let's say we are in the timeline of transactions, and T1 is always fixed to start before T2
		- Now in non-repeatable case T2 could happen before/after any of the reads/operations in T1. This makes the outcome of any read non-predictable.
		- Meanwhile if T2 always happens after T1, it would mean any select in T1 will always yield the same data whatever be the case. How is this achieved is explained in isolation levels down below.
- Phantom reads:
	- T1: S1 S2
	- T2 comes and insert new rows after S1 and before S2, so now there are more rows to read when compared to S1
## Transaction Isolation Levels
- Read Uncommitted
	- Hell loose, prevents nothing
- Read Committed
	- Prevents dirty read only
	- Reads only committed data, each read creates a new version of the data
		- Let's say T1 has S1 and S2 
		- S1 happens and it creates a version of row with tag T1
		- T2 updates the row
		- S2 now creates another version of the data and proceeds to work on it
	- Understand how in example we only read committed data, i.e. what T2 committed, so that would prevent dirty read. But at the same time, we got different row between S1 and S2. Now T2 could also have pushed some new rows, so this isolation level does not provide repeatable reads and does not prevent phantom reads
- Repeatable Reads
	- Default in InnoDB(MySQL)
	- Prevents dirty read, non-repeatable reads and phantom reads
	- Each transaction only works row with it's own tag, in Read Committed, two transactions could read committed data with each other's tag. As that is not possible in this case, one of the transaction needs to retry.
	- With this snapshot style isolation level, one transaction would only read committed data preventing dirty read. Same select would return same data hence repeatable reads is preserved. And finally, new rows added would also be done on transaction's own snapshot, hence it prevents also the cases.
- Serializable
	- Enforces strict ordering among transactions to only happen one after the other
	- This also prevents all problems but at a much more higher cost

## Locking
- Shared locks: used by multiple transacations at a time, when all are reading same data (no writes)
- Exclusive lock: Taken by a transaction who wants to write to a particular row
- Gap locking: This was mentioned [here](https://planetscale.com/blog/mysql-isolation-levels-and-how-they-work#repeatable-read) ,(maybe it's part of MySQL only?). When this lock is tried to be taken, it sees the `where` condition in the query ( it needs a `where` condition to operate), check rows which satisfy the condition and prevents any modifications on them.
	- This is useful in cases like: let's say an operation is repeated multiple times. Normally DB would look over indexes to match the `where` condition, but if that is not present, it would have to take a table level lock. Once that is taken it would apply a gap lock so that it prevents any other updates to those rows and operations don't have to table lock repeatedly for same task.