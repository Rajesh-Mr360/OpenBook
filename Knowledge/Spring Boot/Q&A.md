## Core / Basic Spring Boot Questions

1. **What is Spring Boot ?**    
	- **Spring Boot** is an open-source framework built on top of the **Spring Framework** that simplifies the development of Java-based applications by eliminating complex configuration. Unlike the traditional Spring Framework, which requires extensive XML configuration, Spring Boot follows a **convention-over-configuration** approach and provides **auto-configuration**, eliminating the need for most XML files. This allows developers to focus more on business logic rather than application setup.
	- Additionally, Spring boot provides embedded servers, starter dependencies, and actuators.
2. **What are the key features of Spring Boot ?**
	- The key features of spring boot includes:
		- Auto configuration
		- Embedded Servers
		- Spring Boot Starter Dependencies
		- Actuators
3. **Why use Spring Boot over Spring Framework ?**
    - Developing applications using traditional Spring framework required lot of XML configuration but in spring boot this can be automated by using Spring Boot Auto-configuration feature, reducing the time developers need to spend on configuration and allows them to focus on core business logic. Additionally, Spring Boot provides **Spring Boot Starters** to manage dependencies and supports embedded servers.
4. **What is `@SpringBootApplication` and what annotations does it combine ?**
	- The `@SpringBootApplication` annotation is used on top of main class to mark it as initial point for bootstrap. This annotation is combination of `@Configuration`, `@EnableAutoConfiguration`, and `@ComponentScan` annotations.
5. **Explain auto-configuration in Spring Boot.**
    - Auto-configuration in Spring Boot is a process through which Spring Boot automatically configures your application based on the dependencies present in your classpath. To enable autoconfiguration, we have to add one of the following annotations to the configuration class : `@SpringBootApplication` or `@EnableAutoConfiguration`.
	- *Imagine you add the `spring-boot-starter-web` dependency to your project. This dependency includes various libraries like Spring MVC, Tomcat, and Jackson. Spring Boot automatically configures a web application context, sets up a Tomcat server, and configures Jackson for JSON serialization - all without you writing a single line of configuration code.*
	- Behind the scene Spring boot application leverages the spring factories loader mechanism to locate and load initial configuration. The `@EnableAutoConfiguration` annotation is added on top of the main class, which is entry point for auto configuration. It tells Spring Boot to scan classpath and load all the `spring.factories` files. These files consists of classes that spring boot must consider for auto configuration. Upon loading, the beans are created for eligible classes and will be registered in application context making them available for use throughout the application. 
6. **What are Spring Boot starters ?**
    - **Spring Boot Starters** are **pre-configured bundles** that consists of commonly used libraries as single dependency, removing the need for manually searching for and managing individual dependencies. Instead of adding multiple related dependencies one by one, you just add **one starter**, and it automatically brings all required libraries with compatible versions.

---
## Intermediate / Practical Questions

8. **What’s the difference between `@Controller` and `@RestController`?** 
	- The `@Controller` and `@RestController` annotations are used to mark controller classes in a Spring Boot application. Even though they are used for similar functionalities, the main difference is **how they return data to the client**.
	- With `@Controller`, methods usually return a **view name**, which is resolved to a template. If you want to return JSON, you must add `@ResponseBody`. The `@Controller` annotation is typically used when building web pages.
	- `@RestController` is a combination of `@Controller` and `@ResponseBody`. **All methods return data directly**, so there is no need to annotate each method with `@ResponseBody`. The `@RestController` annotation is used when building REST APIs.
9. **Explain the use of Spring Boot Actuator and its endpoints.**
    - Spring Boot Actuator is a powerful tool that provides production-ready features to monitor and manage Spring Boot applications. It simplifies application management by exposing operational information through HTTP endpoints or JMX beans. These endpoints allow developers to monitor application health, metrics, configurations, and more.
    - Spring Boot Actuator provides a variety of built-in endpoints. Some of the most commonly used ones are:
	    - **/actuator/health**: Displays the health status of the application.  
		- **/actuator/info**: Displays arbitrary application information.  
		- **/actuator/metrics**: Shows ‘metrics’ information for the current application.  
		- **/actuator/env**: Displays properties from the `Environment`.  
		- **/actuator/beans**: Displays a complete list of all Spring beans in your application.
10. **How to change the default Tomcat port?**
    - Using `server.port` in properties.
11. **What is dependency injection in Spring Boot?**
	- **Dependency Injection (DI)** in Spring Boot is a design pattern where the **framework provides (injects) the required objects** to a class instead of the class creating them itself. This makes the code **loosely coupled, easier to test, and more maintainable**. 
	- Spring manages objects marked with annotations like: `@Component`, `@Service`, `@Repository`, `@Controller`, `@RestController`
	- Spring injects them using: `@Autowired`
12. **How do you handle exception handling in Spring Boot ?**
    - Instead of repeating `try-catch` blocks across your controllers and services, **Spring Boot provides a clean way to handle exceptions globally** using `@ControllerAdvice` and `@ExceptionHandler`. This allow you to centralize error handling and return meaningful responses instead of default errors.
13. **Difference between `@Component`, `@Service`, and `@Repository`**.
	- In Spring, `@Component` is a **class-level stereotype annotation** used to mark a class as a **Spring-managed bean**. When Spring performs **component scanning**, it automatically detects such classes, instantiates them, and registers them in the **ApplicationContext** for dependency injection.
	- `@Service` and `@Repository` are specialized forms of the `@Component` annotation, used to identify classes as Spring-managed beans. The `@Service` annotation marks classes that contain core business logic and may interact with the database through other components, while the `@Repository` annotation is applied to classes responsible for database access and persistence operations.
## 🔹 **Advanced / Senior Level Questions**

16. **How to optimize Spring Boot application startup?**
    - Spring Boot applications can experience slow startup times due to factors like excessive bean creation, classpath scanning, and dependency injection. Optimizing startup time is crucial for improving development efficiency and deployment speed.
    - To make the startup faster, you can delay bean creation using **lazy initialization**, which means beans are created only when they are actually needed. You can also improve startup time by **turning off auto-configurations you don’t use**, so Spring doesn’t waste time setting them up. Another helpful step is to **limit component scanning** to only the packages your application really needs, instead of scanning the entire project. And if you want an even bigger boost, Spring Boot supports **AOT compilation with GraalVM**, which turns your application into a native image and helps it start much faster than usual.
17. **Explain asynchronous processing with `@Async`.**
18. **How to implement JWT-based authentication?**
19. **Service Discovery & Microservices integration**
    - Using Spring Cloud Eureka or Consul.
20. **Handling configuration management in distributed systems.**
    - Spring Cloud Config Server & profiles.
21. **How do you containerize a Spring Boot app?**
    - Using Docker file & containers.
22. **Explain transaction management with `@Transactional`.**
	- The transaction management feature in the Spring framework helps you ensure that when you're making changes to your database, either all those changes are saved successfully, or none of them are. This prevents situations where only some changes are saved, leaving your data in an inconsistent state.
	- In Spring, **`@Transactional`** is used to manage database operations as a **single unit of work**, meaning _all the changes inside a method succeed together or fail together_. If something goes wrong, the transaction can be **rolled back**, preventing partial updates and keeping data consistent.
	- When you mark a method with `@Transactional`, Spring:
		- **Opens a database transaction** when the method starts.
		- **Executes all queries inside the method.**
		- If everything is successful → **commits** the changes.
		- If an exception occurs → **Rollback** the changes.
23. **Difference between `RestTemplate` and `WebClient`.** 
	- `RestTemplate` and `WebClient` are both used to call external HTTP services in Spring, but they work differently in terms of style, performance, and usage. `RestTemplate` waits until it gets a response and blocks the thread, while  `WebClient` works asynchronously, letting the app serve more requests without waiting.
24. **How to build microservices with Spring Boot & Spring Cloud?**
    - Microservices communication, circuit breakers, load balancing.

---
## 🔹 **Design & Scenario-Based / Coding Questions**
 
28. **Implement file upload/download endpoints.**
29. **Performance tuning & logging strategy for production.**
