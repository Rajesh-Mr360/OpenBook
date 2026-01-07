**Your microservice-based e-commerce platform integrates with an external payment gateway. Occasionally, the payment service is down, causing failures. How do you ensure system resilience while providing the best user experience ?**

- Use **Circuit Breaker Pattern** (Resilience4j or Hystrix).
- Implement **fallback mechanisms** (retry with exponential backoff or return cached responses).
- Store failed payments and **retry asynchronously** via an event-driven mechanism.

---

**Your Order Service receives the same request multiple times due to network issues. How do you prevent duplicate order processing ?**

- Use an **Idempotency Key** sent by the client.
- Store processed requests in Redis or a database to **reject duplicates**.
---

**Your Spring Boot application is experiencing performance issues under high load. What steps would you take to diagnose and resolve the problem?**


---
**How would you scale a Spring Boot application to handle increased traffic, and what Spring Boot features can assist with this?**

---
**How do you manage transactions in a Spring Boot application, and what code is running internally when using the @Transactional annotation?**

---
**In a Spring Boot application, you need to ensure that all service methods annotated with @Transactional are logged with the execution time taken by each method. How would you implement this in Spring Boot?**

---

**How would you configure your application to ensure that access to API endpoints is restricted based on user roles, and that the role checks are applied to method-level security in your controllers or services?**

For role-based security, use Spring Security. First, enable method-level security:
```
@EnableGlobalMethodSecurity(prePostEnabled = true)
public class SecurityConfig extends WebSecurityConfigurerAdapter {
    // Security configuration
}
```

Then, in your controller or service, use @PreAuthorize or @Secured:

```
@PreAuthorize("hasRole('ADMIN')")
@GetMapping("/admin")
public String adminOnly() {
    return "Admin content";
}
```











---
---


---


**One microservice is taking an extended time to respond, causing your calling service to hang.**

Use the **Circuit Breaker** pattern (e.g., via Resilience4j). This prevents cascading failures by "tripping" the circuit if failure thresholds are met, allowing the system to fail fast and provide a fallback response.

---

**You need to handle high traffic and scale a specific service without impacting the rest of the application.**

Leverage **Kubernetes** for container orchestration to scale service instances horizontally. Use Spring Cloud Load Balancer to distribute traffic across these instances.

---

**Leverage Kubernetes for container orchestration to scale service instances horizontally. Use Spring Cloud LoadBalancer to distribute traffic across these instances.**

Implement the **Saga Pattern**. Use **Choreography** (services react to each other's events via a message broker like Kafka) or **Orchestration** (a central coordinator tells each service what to do) to manage distributed transactions and execute compensating actions if a step fails.

---

**You need to maintain data consistency in an eventually consistent system**

Use event-driven communication with RabbitMQ or Apache Kafka to propagate updates across services.

---
**Clients need to interact with multiple services but you want to expose only a single entry point.**

Use an **API Gateway** (e.g., Spring Cloud Gateway). It handles request routing, authentication, and rate limiting centrally.

---
**Microservice instances change IP addresses dynamically in a cloud environment.**
Implement **Service Discovery** using Netflix Eureka. Services register themselves at startup, and others find them by name instead of hardcoded IPs.

---

**How to secure service-to-service communication?**

Use **Spring Security** with **JWT** tokens. The API Gateway validates the user's token, and services can exchange internal tokens or use mTLS for mutual authentication.






