# Java Interview Questions

## Some Basic Platform Stuff

### Q1. List three Collections interfaces and the basic contract of each. List concrete implementations of each, how they differ, and performance characteristics in space and time.

**Answer:**
1. **List**
   - **Contract**: An ordered collection that can contain duplicate elements.
   - **Implementations**:
     - **ArrayList**: Dynamic array, fast random access (O(1)), slower insertions/deletions (O(n)).
     - **LinkedList**: Doubly-linked list, faster insertions/deletions (O(1)), slower random access (O(n)).

2. **Set**
   - **Contract**: A collection that does not allow duplicate elements.
   - **Implementations**:
     - **HashSet**: Backed by a hash table, provides constant time performance (O(1)) for basic operations.
     - **TreeSet**: Sorted set backed by a Red-Black tree, provides log(n) time complexity for basic operations.
     - **LinkedHashSet**: Maintains insertion order, provides constant time performance (O(1)).

3. **Map**
   - **Contract**: A collection of key-value pairs, each key maps to exactly one value.
   - **Implementations**:
     - **HashMap**: Backed by a hash table, provides constant time performance (O(1)) for basic operations.
     - **TreeMap**: Sorted map backed by a Red-Black tree, provides log(n) time complexity for basic operations.
     - **LinkedHashMap**: Maintains insertion order, provides constant time performance (O(1)).

### Q2. Describe the contract of equals and hashCode. Why is it important that if you implement one, that you implement both?

**Answer:**
- **equals**: Determines if two objects are equal.
- **hashCode**: Returns an integer representation of the object.
- **Importance**: If two objects are equal according to the `equals` method, they must have the same hash code. This is critical for the proper functioning of hash-based collections like HashMap and HashSet.

### Q3. What are generics? What is type erasure and what are the consequences? What are variance, covariance, and contravariance?

**Answer:**
- **Generics**: Allow classes, interfaces, and methods to operate on types specified as parameters.
- **Type Erasure**: The process by which generic type information is removed at runtime, leading to potential runtime errors and limitations.
- **Variance**: How subtyping between more complex types relates to subtyping between their component types.
  - **Covariance**: Allows a type to vary in the same direction as its component type.
  - **Contravariance**: Allows a type to vary in the opposite direction of its component type.
- **Example**: Cannot assign `List<Dog>` to `List<Animal>` directly; use wildcards (`List<? extends Animal>`) for covariance or `List<? super Dog>` for contravariance.

## Concurrency

### Q4. Explain how notify and notifyAll work, and the difference between the two. Why prefer notifyAll to notify?

**Answer:**
- **notify**: Wakes up a single thread waiting on the object's monitor.
- **notifyAll**: Wakes up all threads waiting on the object's monitor.
- **Preference for notifyAll**: Prevents thread starvation and ensures all waiting threads have a chance to proceed.

### Q5. What is a deadlock and how do you avoid it?

**Answer:**
- **Deadlock**: A situation where two or more threads are blocked forever, each waiting on the other.
- **Avoidance**: Use a consistent locking order, lock timeout, or use higher-level concurrency utilities.

### Q6. What is a race condition and how do you avoid it?

**Answer:**
- **Race Condition**: Occurs when the outcome of a program depends on the sequence or timing of uncontrollable events.
- **Avoidance**: Use synchronized blocks, locks, or high-level concurrency constructs like `java.util.concurrent`.

### Q7. What are some of the high-level concurrency classes provided by java.util.concurrent and how do they work?

**Answer:**
- **ExecutorService**: Manages and controls thread execution.
- **ConcurrentHashMap**: A thread-safe implementation of HashMap.
- **CountDownLatch**: Allows one or more threads to wait until a set of operations completes.
- **CyclicBarrier**: Allows a set of threads to all wait for each other to reach a common barrier point.

## Database

### Q8. What are the different statement types and why would you use each?

**Answer:**
- **Statement**: Used for executing simple SQL queries without parameters.
- **PreparedStatement**: Used for executing precompiled SQL queries with parameters, preventing SQL injection and improving performance.
- **CallableStatement**: Used for executing stored procedures in the database.

### Q9. How do you prevent SQL injection attacks?

**Answer:**
- **Use PreparedStatement**: Ensures SQL statements are precompiled and parameters are properly escaped.
- **Validate Input**: Ensure all user inputs are validated and sanitized.
- **Use ORM Tools**: Object-Relational Mapping tools like Hibernate handle query construction and prevent SQL injection.

### Q10. What are transactions? What is ACID?

**Answer:**
- **Transactions**: A sequence of database operations that are treated as a single unit of work.
- **ACID**: Ensures reliable processing of transactions.
  - **Atomicity**: All operations succeed or none.
  - **Consistency**: The database remains in a consistent state.
  - **Isolation**: Transactions are isolated from each other.
  - **Durability**: Once committed, transactions persist.

## Hibernate

### Q11. Give an overview of Hibernate and ORM. How do you load objects into the session? What does the session do with the objects while in the session? What is the difference between getting a persistent object from the session and querying for persistent objects?

**Answer:**
- **Hibernate**: A Java-based ORM tool that maps Java objects to database tables.
- **ORM (Object-Relational Mapping)**: A technique to convert data between incompatible systems (RDBMS and OOP).
- **Loading Objects**: Use `Session.get()`, `Session.load()`, or queries (`HQL`, `Criteria`).
- **Session**: Manages the lifecycle of persistent objects, caches objects to avoid repeated database access.
- **Difference**:
  - **get()**: Returns a persistent object or `null` if not found.
  - **load()**: Returns a proxy, throws an exception if not found.

### Q12. When is it better to use plain SQL instead of ORM?

**Answer:**
- When performance is critical and ORM overhead is unacceptable.
- Complex queries that are hard to express in ORM.
- When interacting with legacy databases or stored procedures.

## Java EE

### Q13. How do you configure a DataSource in WebLogic to make it available using JNDI?

**Answer:**
- **Steps**:
  1. Create a JDBC data source in the WebLogic console.
  2. Set JNDI name, database URL, and credentials.
  3. Target the data source to the server or cluster.
  4. Test the data source to ensure connectivity.

### Q14. What are some ways for the client to obtain a reference to the DataSource from the app server? (Spring is not the answer I am looking for)

**Answer:**
- **Using JNDI Lookup**:
  ```java
  InitialContext ctx = new InitialContext();
  DataSource ds = (DataSource) ctx.lookup("java:comp/env/jdbc/MyDataSource");
  ```

## Spring

### Q15. Give an overview of how Spring Dependency Injection container works. What is the purpose of DI? How to specify bean definitions? What are the different scopes? When do beans of each scope type get instantiated?

**Answer:**
- **Spring DI Container**: Manages the lifecycle and dependencies of beans.
- **Purpose of DI**: To decouple object creation from business logic and improve testability.
- **Bean Definitions**: Specified using XML, annotations (`@Component`, `@Service`, `@Repository`, `@Controller`), or Java configuration (`@Bean`).
- **Scopes**:
  - **Singleton**: One instance per Spring container.
  - **Prototype**: A new instance for each request.
  - **Request**: One instance per HTTP request (web apps only).
  - **Session**: One instance per HTTP session (web apps only).
  - **GlobalSession**: One instance per global HTTP session (web apps only).
- **Instantiation**:
  - **Singleton**: At container startup.
  - **Prototype**: When requested.
  - **Request, Session, GlobalSession**: At the start of the respective web request/session.

## Web Services

### Q16. What is the difference between SOAP-based web services and REST-based web services?

**Answer:**
- **SOAP**: Protocol-based, uses XML, supports WS-* standards, more complex and feature-rich.
- **REST**: Architectural style, uses standard HTTP methods, can use multiple formats (JSON, XML), simpler and more flexible.

### Q17. Describe SOAP and WSDL.

**Answer:**
- **SOAP (Simple Object Access Protocol)**: A protocol for exchanging structured information in web services. Uses XML for message format.
- **WSDL (Web Services Description Language)**: An

 XML-based language for describing the functionality offered by a web service.

### Q18. What exactly is REST? What is HATEOAS? What is the purpose of each of the HTTP verbs? What is idempotence? What is content-negotiation?

**Answer:**
- **REST (Representational State Transfer)**: An architectural style for designing networked applications using stateless communication.
- **HATEOAS (Hypermedia as the Engine of Application State)**: A constraint of REST that allows clients to navigate the API using hyperlinks provided dynamically by the server.
- **HTTP Verbs**:
  - **GET**: Retrieve data.
  - **POST**: Create new resources.
  - **PUT**: Update existing resources.
  - **DELETE**: Delete resources.
  - **PATCH**: Partially update resources.
- **Idempotence**: An operation that produces the same result no matter how many times it is performed (e.g., GET, PUT, DELETE).
- **Content-Negotiation**: Mechanism to serve different representations of a resource based on client preferences (e.g., JSON, XML).

## OOP

### Q19. What is decoupling? Why are loosely-coupled classes desirable? What are some drawbacks?

**Answer:**
- **Decoupling**: Reducing dependencies between classes.
- **Desirable**: Increases modularity, flexibility, and testability.
- **Drawbacks**: Can increase complexity and reduce performance if overused.

### Q20. What is cohesion? Why are highly cohesive classes desirable? What are some drawbacks?

**Answer:**
- **Cohesion**: The degree to which elements of a class belong together.
- **Desirable**: Easier to maintain and understand, promotes single responsibility.
- **Drawbacks**: Can lead to more classes and potentially more complex interactions.

### Q21. Describe polymorphism. What is the importance of contracts between interfaces and concrete types? Why is polymorphic code desirable? What are some drawbacks?

**Answer:**
- **Polymorphism**: The ability of different classes to be treated as instances of the same class through a common interface.
- **Importance of Contracts**: Ensures that implementing classes adhere to the expected behavior defined by the interface.
- **Desirable**: Promotes code reuse, flexibility, and extensibility.
- **Drawbacks**: Can make code harder to understand and debug if overused.

## Additional Resources

### Videos
- [Java Interview Questions - YouTube Playlist](https://youtube.com/playlist?list=PLF9tovyahfL2pF-DWH7WQyuN_Cmz64DTT&si=aN_3gPL8fKG1xvU4)

### Articles
- [Java Interview Questions - Simplilearn](https://www.simplilearn.com/tutorials/java-tutorial/java-interview-questions)
