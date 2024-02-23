# What is ACID?

ACID stands for four properties of a [[database transaction]]:
- [[Atomicity]]: each transaction is one unit of work.
- [[Isolation]]: minimize effects of transactions' operations to each other.
- [[Consistency]]:
- [[Durability]]:

# [[Database transaction]]

- A ==**collection**== of queries that are treated as ==**one unit of work**==.
- A transaction could be read-only, which provides a snapshot of the data at the time of execution, so that it is not affected by other transactions or queries.
- Transaction Lifespan:
	- Transaction **BEGIN**
	- Transaction **COMMIT**: This is when the changes are written to the disk (persist the data)
	- Transaction **ROLLBACK**
	- Transaction unexpected ending = **ROLLBACK** (e.g. crash)
- A transaction would be started implicitly by the database even if the user does not define it (e.g. for a single query).

# [[Atomicity]]

- One unit of work.
- All queries in a transaction must succeed.
- If one query fails, all prior successful queries in the transaction should rollback.
- If the database went down prior to a commit of a transaction, all the successful queries in the transactions should rollback.

# [[Isolation]]

- Tries to solve the problems created by running transactions concurrently.
- Defines how a transaction would be affected by changes from other transactions.
- There are four isolation levels: read uncommitted, read committed, repeatable read, serializable.

# [[Consistency]]

- 

# Durability

- 
