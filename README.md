# Principles for a modern distributed platform (WIP)

This is a collection of principles to guide developments of modern distributed systems like for example, an e-commerce platform.

### Scalability

- Ability to deal with different levels of load in an almost linear way

### Resiliency - High-Availability

- Stable & Reliable (Quality built-in and maintainable)
- Fault tolerant

### Performance


### Stateless

- When possible, be stateless. If you can’t, persist state outside the address space of the application, for example in a database.

### Immutable

- Strive for immutability whenever possible. An object is immutable if its state cannot be modified. Immutable things are automatically thread-safe, without requiring synchronization. Overall, immutability tends to result in fewer bugs and makes it easier to prove a program correct.

### Idempotent

- Whenever possible and reasonable, make service endpoints [idempotent](https://en.wikipedia.org/wiki/Idempotence#Computer_science_meaning), so that an operation produces the same result even when it’s executed multiple times. This allows clients to safely retry operations in case of timeouts due to service processing or network failures.
  - `f(f(x)) = f(x)`
  - to avoid double charges or double refunds - A good example is making a payment. If a client makes a request to pay, the request is successful, but the client times out, the client could retry this same request. With an idempotent system, the person paying would not get charged twice. With a non-idempotent system, they could.
  - (Considering Strategies For Idempotency Without Distributed Locking With Ben Darfler)[https://www.bennadel.com/blog/3390-considering-strategies-for-idempotency-without-distributed-locking-with-ben-darfler.htm]

### Sharding and Quorum

- The most common technique is using sharding. Data is horizontally partitioned using some sort of hash to assign to a partition.
- Many distributed systems have data or computations replicated across multiple nodes. In order to make sure that operations are performed in a consistent way, a voting based approach is defined, where a certain number of nodes needs to get the same result, for the operation to be successful. This is called the quorum.
