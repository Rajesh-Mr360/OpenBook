**Spring Cloud** is a collection of tools and frameworks built on top of **Spring Boot** that helps you easily develop **distributed systems and microservices**.  
It provides solutions to common challenges that appear when you break an application into many small services.

## Why do we need Spring Cloud ?

When you have multiple microservices, you face issues like:
- How will services find each other? (**Service Discovery**)
- How do I load balance requests? (**Client-side/Gateway load balancing**)
- What if one service is down? (**Circuit Breaker / Resilience**)
- How do I hide internal services from outside traffic? (**API Gateway**)
- Where do I store configuration for all services? (**Centralized Config**)
- How do I trace a request across multiple services? (**Distributed Tracing**)

Spring Cloud provides ready-made solutions for these problems so you don’t have to build them from scratch.

## What Spring Cloud includes

| Feature                 | Tool                                      | Purpose                                           |
| ----------------------- | ----------------------------------------- | ------------------------------------------------- |
| **Service registry**    | _Eureka_                                  | Services register themselves and discover others  |
| **API Gateway**         | _Spring Cloud Gateway / Zuul_             | Route external requests to internal services      |
| **Config management**   | _Spring Cloud Config_                     | Store config in Git/central store                 |
| **Load balancing**      | _Spring Cloud LoadBalancer / Ribbon(old)_ | Distribute calls among multiple service instances |
| **Fault tolerance**     | _Resilience4J (Hystrix old)_              | Retry, fallback, circuit breaker                  |
| **Distributed tracing** | _Sleuth + Zipkin_                         | Trace calls across services                       |
### 💬 **In short**

> **Spring Boot = creates microservices**  
> **Spring Cloud = helps microservices work together**

