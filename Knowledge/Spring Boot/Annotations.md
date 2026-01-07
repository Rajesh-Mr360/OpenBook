
# Annotations

## Core Annotations

- **@SpringBootApplication :** The `@SpringBootApplication` annotation is combination of `@Configuration`, `@EnableAutoConfiguration` & `@ComponentScan` annotations. It is typically used on top of the main class of spring boot application to mark it as starting point for bootstrap.

- **@EnableAutoConfiguration :** The `@EnableAutoConfiguration` annotation is used to enable Spring Boot's auto-configuration feature. This feature allows Spring Boot to automatically configure your Spring application based on the jar dependencies that you have added to your project.

- **@ComponentScan :** The `@ComponentScan` annotation in Spring is used along with the `@Configuration` annotation for auto detecting component classes to be managed by Spring Container. When you use `@ComponentScan`, Spring will scan the specified packages for classes annotated with `@Component` (or any of its specialisations, such as `@Controller`, `@Service`, or `@Repository`) and automatically create instances of these classes as beans in the Spring container. The `@ComponentScan` without arguments tells Spring to scan the current package and all of its sub-packages.

- **@Configuration :** The `@Configuration` annotation is a class level annotation which is used to mark a class as a source of bean definition. This annotation is typically used in conjunction with the `@Bean` annotation to define beans that will be managed by the Spring container. The `@Configuration` annotation is typically used on classes that are dedicated to providing configuration for the application. These classes are often referred to as *configuration classes*.

## Web

- **@RestController :** The `@RestController` annotation is combination of `@Controller` & `@ResponseBody` annotations. The return values of methods within an `@RestController` are automatically serialized into the HTTP response body using HTTP message converters (like Jackson for JSON). This eliminates the need to manually add the `@ResponseBody` annotation to every method.

- **@Controller :** Used to mark a class as Spring MVC controller. It indicates that the class is responsible for **handling incoming HTTP requests**, processing them, and returning a **view (UI page)** as a response.

- **@RequestMapping :** The **`@RequestMapping`** annotation in Spring Boot is used to map web requests to specific handler classes or methods that process those requests. It tells Spring Boot **which controller method should be invoked for a particular URI and HTTP request**, enabling proper routing of client requests to the appropriate handler.

- **@GetMapping :** The `@GetMapping` annotation in Spring Boot is used to map HTTP `GET` requests to specific handler methods in a controller class. This annotation is primarily used to mark methods responsible for fetching data from the server.

- **@PostMapping :** The **`@PostMapping`** annotation in Spring Boot is used to handle **HTTP POST requests**. It is mainly used to **send or submit data to the server**, usually to **create new resources**. It tells Spring Boot **which controller method should be invoked when a POST request is made to a specific URI**.

- **@PutMapping :** The **`@PutMapping`** annotation in Spring Boot is used to handle **HTTP PUT requests**. It is mainly used to **update existing data** on the server. It tells Spring Boot **which controller method should be invoked when a PUT request is made to a specific URI**.

- **@PathVariable :** The `@PathVariable` annotation in Spring Boot is used to extract dynamic values from a URL path and bind them to method parameters in a controller.

- **@RequestParam :** The `@RequestParam` annotation in Spring Boot is ==used to **extract query parameters** from a URL or form data in an HTTP request and bind them to method parameters in a controller==. This is commonly used for GET requests, searching, filtering, and managing user inputs.

- **@RequestBody :** The `@RequestBody` annotation in Spring Boot is ==used to **bind the body of an HTTP request to a method parameter** in a controller==. It enables the automatic deserialization of the incoming request body (typically JSON or XML) into a Java object.

- **@ResponseBody :** The `@ResponseBody` annotation in Spring Boot ==indicates that a method's return value should be bound directly to the **HTTP response body** and automatically serialized into the appropriate format== (e.g., JSON or XML). It is primarily used when building RESTful web services or handling AJAX requests, where the direct return of data (rather than a view template) is required.

## Dependency Injection

- **@Component :** In Spring, the `@Component` annotation is a stereotype annotation used to mark a class as a component. This allows Spring to automatically detect it during configuration, create a bean instance, and manage its lifecycle within the Spring container.

- **@Service :** We mark class with `@Service` annotation to indicate that they’re holding the business logic. Besides being used in the service layer, there isn’t any other special use for this annotation.

- **@Repository :** The `@Repository` annotation is used to indicate that the class provides the mechanism for storage, retrieval, update, delete and search operation on objects. It's job is to catch persistence-specific exceptions and re-throw them as one of Spring’s unified unchecked exceptions.

- **@Autowired :** The **`@Autowired`** annotation is used in **Spring Boot** to enable **dependency injection**. It tells Spring to **automatically inject** the required bean into a class, so you don’t need to create objects manually using `new`.

- **@Qualifier :** The **`@Qualifier`** annotation is used **along with `@Autowired`** to **resolve ambiguity** issue when **multiple beans of the same type** exist in the Spring container. It tells Spring **exactly which bean to inject**.

- **@Primary :** The **`@Primary`** annotation is used in **Spring Boot** to mark a bean as the **default choice** when **multiple beans of the same type** are available for dependency injection.

- **@Value :** The **`@Value`** annotation is used to **inject values into fields, constructors, or methods** from **property files**, **environment variables**, or **inline expressions**.

## JPA & Database Annotations
@Entity
@Table
@Id
@GeneratedValue
@Column
@OneToOne
@OneToMany
@ManyToOne
@ManyToMany
@JoinColumn
@Transactional

## Configuration & Properties
@ConfigurationProperties
@EnableConfigurationProperties
@PropertySource
@Profile
@Bean

## Security Annotations
@EnableWebSecurity
@EnableMethodSecurity
@PreAuthorize
@PostAuthorize
@Secured
@RolesAllowed

## Test Annotations
@SpringBootTest
@WebMvcTest
@DataJpaTest
@MockBean
@AutoConfigureMockMvc
@TestConfiguration


## Actuator Annotations
@Endpoint
@ReadOperation
@WriteOperation
