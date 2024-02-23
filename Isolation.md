# What is isolation?

Isolation is one of four properties ([[ACID]]) of a [[database transaction]]. Isolation defines how a transaction would perceive changes from other transactions and vice versa. It is the goal of [[Concurrency control|concurrency control]].

# Why isolation?

Database transactions usually run concurrently, which could lead to problems like:
- [[Read phenomena]]: dirty read, non-repeatable read, phantom read
- [[Lost update]]: two transactions try to update the same value at the same time, which lead to the result of one of the transaction is overridden.
- [[Incorrect summary]]: while one transaction takes a summary over the values of all the instances of a repeated data-item, a second transaction updates some instances of that data-item, which leads to incorrect summary.

Isolation aims to minimize these problems with four defined [[Isolation#Isolation levels|isolation levels]].
# Isolation levels

- Isolation levels define restrictions that database must obey when executing transactions concurrently.
- The higher the level, the more restriction and the less concurrency effects. 
- Higher level also means requiring more system resources and increasing the chances that one transaction will block another.
- Depending on the [[Concurrency control|concurrency control]] of the [[Database Management System|DBSMs]], isolation levels' implementations could vary from one to another.

## Read uncommitted

- The lowest isolation level.
- [[Read phenomena#What is dirty read?|Dirty reads]] are allowed, no restrictions required.

## Read committed

- One level higher than read uncommitted.
- Any read data is guaranteed to be committed.
- Avoid [[Read phenomena#What is dirty read?|dirty reads]].

## Repeatable read

- One level higher than read committed.
- If one transaction is running and have read a value, other transactions must not update this value until the transaction has been committed.
- If one transaction is running and have updated a value, other transactions must not read or update this value until the transaction has finished.
- Avoid [[Read phenomena#What is non-repeatable read?|non-repeatable]] reads.

## Serializable

- The highest isolation level.
- Not only restrict read and write access of a value like repeatable read, but also a range of value if there are any queries in the transaction involve multiple rows (e.g. when using the `WHEN` clause).
- Avoid [[Read phenomena#What is phantom read?|phantom read]].


