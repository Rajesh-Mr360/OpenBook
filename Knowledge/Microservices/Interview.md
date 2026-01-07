## Blue – Green deployment in Microservices

Blue-green deployment in microservices involves running two identical environments – one serves production traffic (blue), while the other hosts a new version (green). Traffic is gradually switched from blue to green, allowing for seamless updates with minimal downtime. If issues arise, traffic can be rerouted back to the stable blue environment, ensuring reliability and enabling quick rollback if necessary.

## RestTemplate

`RestTemplate` is a synchronous client library included in the Spring Framework that simplifies making HTTP requests to RESTful web services. `RestTemplate` is commonly used in Spring Boot applications for making HTTP requests to external APIs. 

`RestTemplate` supports all standard HTTP methods (GET, POST, PUT, DELETE, etc.), allowing you to interact with APIs that require different request types.

In microservice architectures, `RestTemplate` facilitates communication between services. Services can call each other's APIs using HTTP requests made with `RestTemplate`.

## Authentication and Authorization in Microservices
In the context of microservices, authentication and authorization are two crucial components for ensuring the security of the system. Here’s a breakdown of each:

**Authentication**
- Authentication is the process of verifying the identity of a user or service. In a microservices architecture, each service might need to authenticate itself to other services or authenticate users who are accessing the system.
- This process typically involves presenting credentials, such as usernames and passwords, API keys, or tokens, to prove identity.
- Common authentication mechanisms in microservices include JSON Web Tokens (JWT), OAuth, and OpenID Connect.

**Authorization**
- Authorization, on the other hand, is the process of determining what actions an authenticated user or service is allowed to perform. Once a user or service is authenticated, authorization mechanisms enforce access control policies to ensure that only authorized actions are permitted.
- This often involves defining roles and permissions, which are then used to make access control decisions.
- Authorization mechanisms can range from simple role-based access control (RBAC) to more fine-grained access control strategies like attribute-based access control (ABAC) or policy-based access control (PBAC).
## How to Register Microservices Using Netflix Eureka
- Spring Cloud provides a convenient way to integrate with Eureka.
- Include the `spring-cloud-starter-netflix-eureka-client` dependency in your `pom.xml` or `build.gradle` file.
- Annotate your main class with `@EnableEurekaClient`.
- Configure properties like `eureka.client.serviceUrl.defaultZone` to point to your Eureka server instance.
- Your microservice will automatically register itself with Eureka on start-up.

---
How does microservices architecture promote continuous integration and continuous deployment (CI/CD)?

Microservices architecture promotes CI/CD by **facilitating the independent development and deployment of each service**. Since microservices are loosely coupled, teams can work on them independently.

https://arjunks1991.medium.com/service-registry-service-discovery-and-load-balancing-in-microservices-applications-83c937c16d48


