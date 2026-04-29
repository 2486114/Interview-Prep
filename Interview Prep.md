Interview Prep

Bean lifecycle
instantiation
init()-postdeclaration
service
destroy()-predestroy

Maven
Default Lifecycle (Build & Deploy)
This is the most commonly used lifecycle, covering everything from validation to deployment.
Phases include:
validate – Check project structure and configuration.
compile – Compile source code.
test – Run unit tests.
package – Bundle compiled code into JAR/WAR/etc.
verify – Run integration checks.
install – Place artifact in local repository.
deploy – Push artifact to remote repository.

JDBC
// Online Java Compiler
// Use this editor to write, compile and run your Java code online
import java.sql.*;
class Main {
    public static void main(String[] args) {
        Connection conn = null;
        PreparedStatement st = null;
        ResultSet rs = null;
        try{
            Class.forName("com.mysql.cj.jdbc.Driver");
            conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/db_name","root","root");
            st = conn.prepareStatement("Select * from user");
            rs = st.executeQuery();
            while(rs.next()){
                System.out.println(rs.getString("name"));
                System.out.println(rs.getString("email"));
                System.out.println(rs.getInt("age"));
            }
        }catch(ClassNotFoundException e){
            System.out.println("The class is not found:"+e);
        }
        catch(Exception e){
            System.out.println("Exception occurred:"+e);
        }finally{
            rs.close();
            conn.close();
            st.close();
        }
    }
}

Core java

6 characterisitics of OOPs
1. An Object is a basic unit of Object-Oriented Programming that represents real-life entities. State - attributes, Behavior - methods, Identity - name

2. A Class is a user-defined blueprint or prototype from which objects are created. It represents the set of properties or methods that are common to all objects of one type.

3. Abstraction in Java is the process of hiding implementation details and showing only the essential features of an object. It helps users focus on what an object does rather than how it does it. Ex: ATM, Coffee machine

4. Encapsulation is the process of wrapping data and methods into a single unit, usually a class, and restricting direct access to the data. It acts as a protective shield that prevents data from being accessed directly from outside the class.
Data members are hidden using the private access modifier.
Access to data is provided through public getter and setter methods.
It improves data security, maintainability, and controlled access.

(Association is an OOP concept that defines a relationship between two or more classes that are connected to each other. In association, objects of one class are related to objects of another class, but they can exist independently. 
Types: Aggregation (Weak Association) - One object can exist without the other; Composition is a strong form of association where one class owns another class. Child object cannot exist without the parent.)

5. Inheritance is a core OOP concept in Java that allows one class to acquire the fields and methods of another class using the extends keyword. It represents an “is-a” relationship between classes.

6. Polymorphism is an OOP principle that allows one method or interface to represent multiple behaviors depending on the context. At compile-time, this is achieved through method overloading, and at runtime, through method overriding. 
Context: in overloading is type or number of args; in overriding, it is the type of actual object.



why is string immutable in java?

Strings are often used to store sensitive data like passwords, usernames, and connection URLs. Immutability prevents malicious code from altering these values after they are created, ensuring data integrity. 

Java uses a String Pool to store string literals. When a string is created, it is stored in this pool, and any subsequent references to the same string reuse the existing object. Immutability ensures that one reference cannot alter the value for others, saving memory and avoiding unnecessary duplication.
Also, Thread safe

volatile ensures visibility: all threads see the latest value in main memory.
But it does not make compound operations atomic.
count++ is actually three steps: read → increment → write.
Another thread can sneak in between these steps, causing race conditions.
To guarantee atomicity, you can use:
synchronized blocks/methods: Lock the resource so only one thread executes the critical section at a time.
Atomic classes (java.util.concurrent.atomic): e.g., AtomicInteger, AtomicLong. They provide atomic operations like incrementAndGet() without explicit synchronization.
Use volatile for simple flags.
Use synchronized or atomic classes for counters, collections, or any compound operations.

To perform atomic operations (like increment, decrement, update) on variables without explicit synchronization.
Atomic classes in Java are part of the java.util.concurrent.atomic package. They provide lock‑free, thread‑safe operations on single variables using hardware‑level atomic instructions like Compare‑And‑Swap. Unlike volatile, which only guarantees visibility, atomic classes guarantee both visibility and atomicity. They are more efficient than synchronized for simple counters or flags, and are widely used in concurrent programming to avoid race conditions without explicit locks.
Examples: AtomicInteger, AtomicLong, AtomicBoolean, AtomicReference.
Methods Provided:
get() → returns the current value
set() → sets a new value
incrementAndGet() → atomically increments and returns the new value
compareAndSet(expected, update) → atomically updates if current value equals expected

Garbage Collection is the process of automatically freeing memory by destroying objects that are no longer reachable.
Types of Garbage Collectors:
Serial GC: Single thread, suitable for small applications
Parallel GC: Multiple threads, default in JDK 8
CMS GC (Concurrent Mark Sweep): Low pause times
G1 GC (Garbage First): For large heap memory, default since JDK 9
ZGC: Scalable low-latency GC

Error vs Exception
Errors indicate serious problems that occur mostly due to the environment or JVM state, such as OutOfMemoryError, StackOverflowError, or VirtualMachineError.  Exceptions are events that disrupt the normal flow of a program. 
Recoverability: Errors are not recoverable; exceptions often are.
Type: Errors are always unchecked; exceptions can be checked or unchecked.
Cause: Errors stem from JVM/environment issues; exceptions are usually due to program logic or external resources.
Handling: Avoid catching errors; handle exceptions to maintain program stability

Threads/Multithreading
Methods:
yield()
join()
sleep()

Reflection API

java 8 features:

1. New Date/Time API (java.time) Immutable, thread-safe classes like LocalDate, LocalDateTime, ZonedDateTime replace the old Date/Calendar.
LocalDate today = LocalDate.now();
LocalDate future = today.plusDays(5);

2. Default \& Static Methods in Interfaces Allow adding new methods to interfaces without breaking existing implementations.

3. Functional Interfaces Marked with @FunctionalInterface, they work seamlessly with lambdas. Examples: Runnable, Comparable, Comparator, Predicate(boolean), Function, Consumer, Supplier. package: java.util.functional.
1 abstract method and 0 or more implemented methods.
@FunctionalInterface is not mandatory, but if in case u/ some developer tries to add another method, it helps compiler to throw an error.
Related concept: Marker interface - with 0 methods; purpose-?

4. Stream API Introduces a declarative way to process collections with operations like filter, map, reduce, and supports parallel processing.
source/object.stream()
source, intermediate(filter, map, sorted, distinct), terminal operations(reduce, count, findAny, findFirst).

5. Optional Class Helps avoid NullPointerException by wrapping values and providing safe access methods like orElse, ifPresent.
Optional<String> opt = Optional.ofNullable(null);
System.out.println(opt.orElse("Default"));

6. Lambda expression: implementation of abstract method of a Functional Interface.
For Predicate: test(arg)
Ex: Predicate<Integer> isEven = i -> i % 2 == 0;
System.out.println(isEven.test(4)); // Output: true
Predicate<Integer> isPositive = i -> i > 0;
Predicate<Integer> isEvenAndPositive = isEven.and/or/isEqual(isPositive);isEven.negate();
System.out.println(isEvenAndPositive.test(4)); // Output: true
Rules:
1. Types can be inferred Or declared explicitly
2. Single Parameter Can Omit Parentheses
3. No Parameters Use Empty Parentheses
4. Single Statement Can Skip Braces
5. Return Keyword Not Required for Single Expression

 Collectors used in stream API


java 14 features
Helpful NullPointerExceptions: adding the capability to point out what exactly was null in a given line of code.
text blocks now have two new escape sequences:
    \: to indicate the end of the line, so that a new line character is not introduced
    \s: to indicate a single space
Switch Expressions: 
    Arrow Syntax (->): Introduces a new label form that automatically breaks after the matching case, preventing accidental fall-through to subsequent blocks.
    Return Values: A switch can now evaluate to a single value, allowing it to be assigned directly to a variable.
    Multiple Case Labels: You can group multiple constants in a single case separated by commas (e.g., case 1, 2, 3 -> ...).
    The yield Keyword: Used to return a value from a multi-line code block within a switch expression, replacing the need for a break to return results.


Java 17 features
record
sealed classes/interfaces
Pattern Matching for instanceof
multiline text blocks(json,html,sql) using """    """
switch expression (arrow)
new RandomGenerator, previously Random


Java 21 features
Virtual Threads → “Java 21 introduced virtual threads, making it easy to run thousands of lightweight threads for scalable concurrency.”
Pattern Matching for Switch → “Switch statements can now match types directly, removing the need for manual casting.”
Record Patterns → “Record patterns let you unpack data from record classes directly in conditions, reducing boilerplate.”
Ex: if(obj instanceof Point(int x, int y)){..} i.e destructuring
String Templates (Preview) → “String templates simplify building strings with variables using placeholders, like STR."Hello, \{name}!".”
Sequenced Collections interface → used to get first and last elements.

In Java, we can create threads either by extending the Thread class or by implementing the Runnable interface. Extending Thread ties the task and thread together, but it restricts inheritance. Implementing Runnable is preferred because it separates the task from the thread execution and allows the class to extend other classes.

Platform independence in Java refers to its ability to run the same compiled code on any operating system or hardware architecture without modification. This is achieved through the use of bytecode and the Java Virtual Machine (JVM).

When a Java program is written, it is compiled by the javac compiler into an intermediate form called bytecode (stored in .class files). it is designed to be executed by the JVM, which acts as an interpreter. Hence Java supports Write Once, Run Anywhere (WORA).

JVM is platform dependent.

Feature 	wait()	sleep()
Class	Defined in java.lang.Object	Defined in java.lang.Thread
Lock Release	Releases the object lock (monitor)	Does not release any locks
Context	Must be called from a synchronized block/method	Can be called from any context
Waking Up	Wakes via notify(), notifyAll(), or timeout	Wakes automatically after the specified time
Method Type	Instance method	Static method (affects current thread)
Purpose	Inter-thread communication	Introducing a simple time delay


Annotations in the Spring Framework are a form of metadata that provide additional information about the program. They do not directly affect the execution of the code but are used to configure and manage the behavior of Spring applications. These annotations simplify development by reducing the need for extensive XML configuration.
They are used by compilers and development tools to process the code.

Key Categories of Spring Annotations
Dependency Injection (DI) Annotations
Annotations like @Autowired, @Qualifier, and @Value are used to inject dependencies into Spring beans. For example:
class Student {
@Autowired
private Address address;
}
@Autowired automatically injects the Address bean into the Student class.
Spring Web Annotations
These annotations, such as @Controller, @RequestMapping, and @RestController, are used in Spring MVC to handle web requests. For instance:
@Controller
public class DemoController {
@RequestMapping("/hello")
@ResponseBody
public String hello() {
return "Hello, Spring!";
}
}
This maps the /hello endpoint to the hello method.
Spring Boot Annotations
Annotations like @SpringBootApplication and @EnableAutoConfiguration are specific to Spring Boot. They simplify application setup by enabling auto-configuration and component scanning:
@SpringBootApplication =
 @Configuration - The @Configuration annotation in Spring marks a class as a source of bean definitions for the Spring IoC container 
@EnableAutoConfiguration - Spring Boot simplifies the configuration process primarily through its auto-configuration feature. This feature automatically configures your application based on the dependencies present in the classpath, eliminating the need for extensive manual setup.
 @ComponentScan - The @ComponentScan annotation in Spring is used to specify the packages that should be scanned for Spring components like service, repository, controller, etc. This annotation is typically used alongside the @Configuration annotation to define the configuration class for a Spring application.
@SpringBootApplication
public class DemoApplication {
public static void main(String\[] args) {
SpringApplication.run(DemoApplication.class, args);
}
}
Scheduling and Asynchronous Processing
Annotations such as @EnableScheduling and @Scheduled allow scheduling tasks, while @Async enables asynchronous method execution.
Data Access Annotations
Annotations like @Transactional, @Id, and @Query are used for database operations. For example:
@Transactional
public void performTransaction() {
// Transactional logic
}
Bean and Component Annotations
Annotations like @Component, @Service, and @Repository define Spring-managed beans. For example:
@Service
public class UserService {
// Business logic
}
Practical Benefits
Spring annotations reduce boilerplate code, improve readability, and make applications easier to configure and maintain. They are widely used across Spring Core, Spring MVC, Spring Boot, and Spring Data modules to streamline development.

API documentation is essential because it helps API consumers understand how to use the endpoints — what requests they can make, what responses to expect, and what rules or validations apply. Without clear documentation, consumers struggle to integrate, leading to errors and wasted time. In my project, we used Swagger/OpenAPI to generate interactive documentation so that consumers could easily test the endpoints.

Problem: Monolithic applications become hard to scale, maintain, and deploy independently.
Solution: Microservices break the application into smaller, independently deployable services, each handling a specific business capability.
Project Use: In my project, we separated modules like User Service, Order Service, and Inventory Service to scale independently and reduce deployment risks.

Problem: Managing distributed microservices (communication, configuration, discovery) is complex.
Solution: Spring Cloud provides tools for service discovery, configuration management, load balancing, and resilience.
Project Use: We used Spring Cloud Config for centralized configuration and Spring Cloud Netflix (Eureka, Ribbon, Hystrix) for service discovery and fault tolerance.

Problem: Without validation, invalid data can enter the system, causing errors or inconsistent states.
Solution: Bean Validation (JSR 380, Hibernate Validator) ensures data integrity by applying annotations like @NotNull, @Size, @Email.
Project Use: We validated user input in DTOs before persisting to the database, preventing bad data from propagating.

Problem: Microservices need a way to discover each other dynamically without hardcoding IPs.
Solution: Eureka Server acts as a service registry where services register themselves and discover others.
Project Use: We deployed Eureka Server so our Order Service could dynamically locate the Inventory Service without manual configuration.

Problem: Monitoring and managing microservices in production is difficult without built-in endpoints.
Solution: Actuator provides endpoints for health checks, metrics, and application info.
Project Use: We exposed /actuator/health and /actuator/metrics.

Generics allow you to write classes, interfaces, and methods that work with different data types, without having to specify the exact type in advance.
This makes your code more flexible, reusable, and type-safe.
Instead of writing separate code for each type, you can use type parameters like <T> to make your code reusable and avoid runtime ClassCastException errors.
if a non-generic method matches exactly, it will be chosen over a generic method.
Cannot overload by return type alone — parameter list differences are required.
Type promotion applies if no exact match exists (e.g., byte → int).

DBMS and SQL
Database normalization is a systematic process of structuring data in relational databases to reduce redundancy, eliminate anomalies, and ensure data integrity. It involves decomposing large, unorganized tables into smaller, well-structured ones while maintaining relationships between them.

types of queries:
ddl(create,alter table, drop,truncate,add column),dml(insert,update,delete),dcl(grant,revoke),tcl(set transaction, commit,rollback,savepoint),dql(select)
constraints: A set of conditions defining the type of data that can be input into each column of a table - default, unique, not null, primary key, foreign key

Spring
DI is a design pattern where dependencies are injected externally rather than created within the class, promoting loosely coupled code.

IoC is a design pattern where the control of object creation and management is delegated to a container. Spring’s IoC container manages beans and their dependencies.
IoC Containers:
BeanFactory: Basic container for managing beans.
ApplicationContext: Advanced container with additional features like event propagation.

Logging- Slf4j vs logback vs log4j vs java.util.logging
SLF4J is a logging facade — it provides a common API so applications aren’t tied to one logging framework. Logback is the default implementation for SLF4J, offering fast performance and rich features like rolling logs and flexible configuration. Log4j is another popular logging framework, older than Logback, but still widely used with similar capabilities. Java’s built‑in `java.util.logging` is the standard library option, but it’s less flexible and less powerful compared to SLF4J with Logback or Log4j. In practice, most modern projects use SLF4J with Logback for flexibility and performance.

How service discovery works in Eureka
Each microservice registers itself with Eureka Server.
Eureka maintains a registry of available services and their instances.
Clients (via Feign) query Eureka to find the service location dynamically.
This avoids hardcoding IPs/ports.

Spring DAO simplifies database access by providing a consistent framework for data operations.
Spring DAO using JDBC and Hibernate

Spring Cloud
It is a framework for building cloud applications, simplify the implementation of microservices, Centralized configuration.
Tools: service discovery, API Gateway, and load balancing
Resilience and Fault Tolerance: Implements advanced fault tolerance patterns (e.g., circuit breakers, retries) to ensure high availability in microservices. 
Spring Cloud Components: 
Spring Cloud Config 
Provides centralized external configuration for distributed systems, supporting dynamic updates without restarting applications. 
Spring Cloud Netflix 
Integrates Netflix OSS tools like Eureka (service discovery), Ribbon (load balancing), Hystrix (circuit breaker), and Zuul (API gateway). 
Spring Cloud Gateway 
A modern API gateway for routing, security, and monitoring of microservices, replacing Zuul for better performance and scalability. 
Spring Cloud Sleuth 
Adds distributed tracing to microservices, enabling request tracking across services in combination with tools like Zipkin or Jaeger. 
Spring Cloud Stream 
Supports building event-driven microservices by abstracting messaging systems like Kafka and RabbitMQ. 
Spring Cloud Kubernetes 
Provides integration with Kubernetes for service discovery, configuration, and seamless deployment in containerized environments. 

Load balancing is handled client-side using Spring Cloud LoadBalancer integrated with Eureka. The API Gateway uses the lb:// URI scheme to resolve service names, and requests are distributed across instances using a Round Robin strategy by default.

Spring security
Authentication verifies identity using credentials like a Username and Password to establish who a user is.
Authorization determines what resources a verified user can access based on their Roles and permissions.
Security error codes associated with these processes are 401 Unauthorized for failed authentication and 403 Forbidden for failed authorization.

Spring REST
REST (Representational State Transfer) is an architectural style used for building web-based APIs. It relies on stateless communication and standard HTTP methods like GET, POST, PUT, and DELETE to interact with resources. Data is usually exchanged in JSON or XML.
Rest principles
Client–Server: Separation of concerns: client handles UI, server handles data. Makes systems more flexible and scalable.
Stateless: Each request must contain all the info needed. Server doesn’t store client session state.
Cacheable - Responses should define if they can be cached. Improves performance and scalability.
Uniform Interface - Consistent way to interact with resources (URIs, HTTP methods, representations).
Layered System - Clients don’t need to know if they’re talking to the actual server or an intermediate (like a proxy or gateway). Improves scalability and security.

Spring Boot
Auto‑configuration → Spring Boot configures beans automatically based on classpath.
Starters → Pre‑packaged dependencies (e.g., spring-boot-starter-web).
Profiles → Different configs for environments (dev, test, prod).
Spring (Boot) Starters 
Spring Web: 
The stater is used to build web application 
Spring Stater Parent: 
Used in maven project to simplify dependency management and configuration of spring boot applications 
It acts as project object model(POM) that manages the versions of dependencies and plugins to support the applications 
Spring Stater actuator: 
This stater provides production ready features for monitoring managing your application (Wx: Health Check) 
Spring Stater Test: 
This stater provides Set of testing tools to test spring boot application 
Junit 
Spring Stater Thymeleaf: 
This stater that  integrates Thymeleaf engine with spring boot allowing you to create dynamic web application 
Spring Stater Dev Tools: 
It is a stater That enhances the development experiences in spring boot applications that providing features like 
Automatic restart 
Livereload 
Debubbing etc… 
Spring Stater Security: 
This Is a stater which provides security to your spring boot application providing authentication and authorization as the key features 
Spring Stater JPA: 
This is a starter in spring boot which provides database access 
Spring Boot MVC: 
MVC is standard design pattern which will be used by many of the developers to build a web application 
SpringBoot Security: 
It is a starter in springboot framework which provides security to the application 
By using this starter it provides basic authentication and authorization to spring boot appliocation 


Spring Data JPA
Spring Data JPA uses Hibernate as its default JPA provider. All the JPA annotations are processed by Hibernate at runtime.
Entities → Classes mapped to database tables.
Repositories → Interfaces for CRUD operations.
Relationships → @OneToMany, @ManyToMany, @ManyToOne.
N+1 problem:

derived methods: findByUsername, etc.

Hibernate
Hibernate is a powerful Java framework designed to simplify database interactions in Java applications. It is an open-source, lightweight Object-Relational Mapping (ORM) tool that facilitates the conversion of data between Java objects and relational database tables.
Hibernate uses POJOs to map Java objects to database tables. It supports multiple databases.
(only for console applications)
Lazy Loading → Data fetched only when needed.
Eager Loading → Data fetched immediately.
Caching → First‑level (session) and second‑level (shared) cache.

Query Interface: Used to execute HQL queries. Obtained via session.createQuery().
Key Methods:
executeUpdate(): For DML operations (INSERT, UPDATE, DELETE).
list(): Retrieves all records.
setFirstResult(): Sets the starting record for pagination.
setMaxResults(): Limits the number of records retrieved.
setParameter(): Binds parameters to queries.

JPA vs Hibernate
JPA is a specification, while Hibernate is a framework that implements JPA.
JPA uses EntityManager and EntityManagerFactory for persistence operations, while Hibernate uses Session and SessionFactory.
JPA queries are written in JPQL, whereas Hibernate uses HQL, which extends JPQL with additional features.

REST APIs
@RestController → Defines REST endpoints.
@RequestMapping → Maps URLs.
@GetMapping, @PostMapping → Handle specific HTTP methods.

Microservices
Service Discovery (Eureka) → Services register and find each other.
API Gateway → Single entry point for routing, auth, logging.
Config Server → Centralized configuration management.
Resilience (Circuit Breaker) → Prevents cascading failures (Resilience4j).

Testing
JUnit → Unit testing framework.
Mockito → Mock dependencies for isolated testing.