# What is read phenomena?

Read phenomena occurs when a transaction retrieves data that another transaction might have updated.

There are ==three types== of read phenomena:
- Dirty read (write-read conflict)
- Non-repeatable read
- Phantom read

# Problems with read phenomena

It leads to inconsistencies between queries of the transaction and put the database in an unreliable state.

# Types of read phenomena

## Dirty read

### What is dirty read?

Dirty read occurs when a transaction retrieves a value that has been updated by another transaction that is not yet committed.

### Consequences:

- There would be inconsistencies between queries of the transaction.
- The transaction could read data that is considered never to have existed (hence the dirty).

### Isolation level:

This could be prevented by applying [[Isolation#Isolation levels#Read committed|Read Committed Isolation]].

### Example:

| Transaction 1 | Transaction 2 |
| ---- | ---- |
| `BEGIN;`<br>`SELECT age FROM users WHERE id = 1;`<br>`-- retrieves 20` |  |
|  | `BEGIN;`<br>`UPDATE users SET age = 21 WHERE id = 1;`<br> |
| `SELECT age FROM users WHERE id = 1;`<br>`-- retrieves 21`<br>`COMMIT;`<br> |  |
|  | `ROLLBACK;`<br> |

## Non-repeatable read

### What is non-repeatable read?

- Non-repeatable read occurs when a transaction retrieves a row twice, and that row has been updated by another transaction that is committed in between.
- Compare to dirty read, the data that Transaction 1 have read would be existed at some point in the database.

### Consequences:

- There would be inconsistencies between queries of the transaction.

### Isolation level:

This could be prevented by applying Repeatable Read isolation level.

### Example:

| Transaction 1 | Transaction 2 |
| ---- | ---- |
| `BEGIN;`<br>`SELECT age FROM users WHERE id = 1;`<br>`-- retrieves 20` |  |
|  | `BEGIN;`<br>`UPDATE users SET age = 21 WHERE id = 1;`<br>`COMMIT;`<br> |
| `SELECT age FROM users WHERE id = 1;`<br>`-- retrieves 21`<br>`COMMIT;`<br> |  |

## Phantom read

### What is phantom read?

A phantom read occurs when a transaction retrieves a set of rows twice and new rows are inserted into or removed from that set by another transaction that is committed in between.

### Consequences

- There would be inconsistencies between queries of the transaction.

### Isolation level:

This could be prevented by applying Serializable isolation level.

### Example:

| Transaction 1 | Transaction 2 |
| ---- | ---- |
| `BEGIN;`<br>`SELECT name FROM users WHERE age > 17;`<br>`-- retrieves Alice and Bob` |  |
|  | `BEGIN;`<br>`INSERT INTO users VALUES (3, 'Carol', 26);`<br>`COMMIT;`<br> |
| `SELECT name FROM users WHERE age > 17;`<br>`-- retrieves Alice, Bob and Carol`<br>`COMMIT;`<br> |  |
