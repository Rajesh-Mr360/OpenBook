# Introduction

**Spring Boot** is an open-source framework built on top of the **Spring Framework** that simplifies the development of Java-based applications by eliminating complex configuration. Unlike the traditional Spring Framework, which requires extensive XML configuration, Spring Boot follows a **convention-over-configuration** approach and provides **auto-configuration**, eliminating the need for most XML files. This allows developers to focus more on business logic rather than application setup.

# Features of Spring Boot
The key features of Spring Boot are:
1. Auto Configuration
2. Embedded Servers
3. Starter Dependencies
4. Actuator

## 1. Auto Configuration
Auto-configuration in Spring Boot is a process through which Spring Boot automatically configures your application based on the dependencies present in your classpath. To enable autoconfiguration, we have to add one of the following annotations to the configuration class : `@SpringBootApplication` or `@EnableAutoConfiguration`.

*Imagine you add the `spring-boot-starter-web` dependency to your project. This dependency includes various libraries like Spring MVC, Tomcat, and Jackson. Spring Boot automatically configures a web application context, sets up a Tomcat server, and configures Jackson for JSON serialization - all without you writing a single line of configuration code.*

### 1.1. Internal Working of Autoconfiguration

Behind the scene Spring boot application leverages the **Spring factories loader mechanism** to locate and load configurations. Here's a breakdown of the internal workings of Spring Boot auto-configuration:

The `@EnableAutoConfiguration` annotation, typically placed on top of main class of your application, and is the entry point for auto-configuration. It tells Spring Boot to scan the classpath for auto-configuration classes located in `META-INF/spring.factories` files within your project's dependencies.

The Spring Factories Loader mechanism loads the `spring.factories` files from all the jars on the classpath. These files contain lists of auto-configuration classes that Spring Boot should consider for configuration. Not all auto-configuration classes are applied by default. Spring Boot uses conditional annotations to determine which configurations should be activated.

Some commonly used conditional annotations include:
    - `@ConditionalOnClass`: Applies the configuration only if the specified class is present on the classpath.
    - `@ConditionalOnMissingBean`: Applies the configuration only if a bean of the specified type does not already exist in the application context.
    - `@ConditionalOnProperty`: Applies the configuration based on the value of a specific property in your application configuration files.
  
When Spring Boot finds an auto-configuration class that meets all the specified conditions, it creates and configures the beans defined within that class. These beans are then registered in the Spring application context, making them available for use throughout your application.

### 1.2. Customization and Overriding Auto-Configurations

Spring Boot’s auto-configuration is not a rigid process. You can customize or override these auto-configurations in several ways:

- **Custom `@Configuration` Classes:** You can define your own configuration classes to specify or override beans.
- **Application Properties:** Using `application.properties` or `application.yml`, you can customize various aspects of the auto-configurations, such as server port, database URLs, etc.
- **Excluding Auto-Configurations:** You can exclude specific auto-configuration classes using the `@EnableAutoConfiguration` annotation with the `exclude` attribute.

### 1.3. Disabling Auto-Configuration

In some cases, you may want to completely disable a specific auto-configuration. To do this, add the following property to your `application.properties` or `application.yml` file:

```properties
spring.autoconfigure.exclude=org.springframework.boot.autoconfigure.security.SecurityAutoConfiguration
```

Alternatively, use the `@EnableAutoConfiguration` annotation in your main application class and exclude specific auto-configuration classes:

```Java ln:false
@SpringBootApplication  
@EnableAutoConfiguration(exclude = {SecurityAutoConfiguration.class})  
public class MyApplication {  
	public static void main(String[] args) {  
		SpringApplication.run(MyApplication.class, args);  
	}  
}
```


---


## Spring Boot Starters 

> [!NOTE]
> _The primary purpose of a **Spring Boot Starters** is to provide all the necessary dependencies in one place so that you don’t have to hunt down and specify each one individually._

Before **Spring Boot Starters** was introduced, Developers used to spend a lot of time on Dependency management. Spring Boot Starters were introduced to solve this problem so that the developers can spend more time on actual code than Dependencies.

**Spring Boot Starters are pre-configured sets of dependencies that simplify the process of adding commonly used libraries to your Spring Boot application.** There are around 50+ Spring Boot Starters for different Spring and related technologies. These starters give all the dependencies under a single name.

For example, to get started using Spring and JPA for database access, you can include the `spring-boot-starter-data-jpa` dependency in your project. This will automatically add all the required dependencies, such as Spring Data JPA, Hibernate, and a database driver, to your project.
### Key benefits

- **Reduced Boilerplate Code:** Spring Boot starters eliminate the need to write lengthy XML configuration files or manually add individual dependency libraries. They streamline the process by providing pre-configured beans and configurations.
- **Compatibility and Version Management:** Starters ensure compatibility between different libraries within the package and manage their versions effectively, reducing potential conflicts.
- **Faster Development:** By using starters, you can quickly set up core functionalities like database access, web development, security, and more, allowing you to focus on building the unique features of your application.
- **Simplified Dependency Management:** Spring Boot Starters simplify managing dependencies by providing a single entry point for a group of related libraries. This eliminates the need to manually manage individual versions and potential conflicts.

---

## Spring Boot Actuator

### Introduction  
Spring Boot Actuator provides production ready features to monitor and manage their Spring Boot applications. It provides a set of built-in endpoints, these endpoints provide a wide range of useful information about the application’s health, performance, and behavior. Actuator endpoints can be accessed via **HTTP GET** requests, which return information in JSON format.

**Here are some commonly used ones:**
- **/health:** This endpoint provides basic health information about your application, indicating if it's functioning properly.
- **/info:** This endpoint exposes general information about your application, including build details, dependencies, and Git commit information.
- **/metrics:** This endpoint provides detailed metrics about your application's performance, including memory usage, garbage collection, and HTTP requests.
- **/env:** This endpoint displays all the environment variables your application is using.
- **/loggers:** This endpoint allows you to view and modify the logging levels for different parts of your application.
- **/shutdown:** This endpoint can be used to gracefully shut down your application.

To enable Spring Boot Actuator in the application, we need to add the `spring-boot-starter-actuator` dependency to your project. Once you’ve added the dependency, Spring Boot Actuator’s features will automatically become available in a standard Spring Boot application. For instance, you can navigate to `http://localhost:8080/actuator/health` to view your application’s health information.

By default, only the ‘`/health`’ and ‘`/info`’ endpoints are enabled. If you want to enable all endpoints, you can add the following property to your `application.properties` file:

``` ln:false
management.endpoints.web.exposure.include=*
```

If you want to expose only specific endpoints, you can list them:

``` ln:false
management.endpoints.web.exposure.include=health,info,beans
```

---

## Spring Boot CLI

Spring Boot CLI (Command Line Interface) is a command line tool that allows developers to run Spring Boot applications from the command line. This tool is particularly useful for developers who prefer to work in a command-line environment, as it allows them to quickly create and run Spring Boot applications without the need for an IDE.

One of the key advantages of using the Spring Boot CLI is that it makes it easy to create new Spring Boot projects. The CLI provides a command called `spring init` which can be used to generate a new Spring Boot project with a specified set of dependencies. This command also allows developers to specify the build tool (Maven or Gradle) and the packaging format (JAR or WAR) for the project.

Another advantage of using the Spring Boot CLI is that it allows developers to quickly run their Spring Boot applications from the command line. The CLI provides a command called `spring run` which can be used to run a Spring Boot application. This command also allows developers to specify command-line arguments and properties for the application.

The Spring Boot CLI also provides a command called `spring shell` which starts a shell session where developers can run various Spring Boot commands. This shell session provides an interactive environment where developers can quickly test and experiment with different Spring Boot features.

In addition to these features, the Spring Boot CLI also provides a number of other useful commands such as `spring test` to run tests, `spring jar` to package application as a jar, `spring war` to package application as a war and many more.

Overall, the Spring Boot CLI is a powerful tool that allows developers to easily create, run and test Spring Boot applications from the command line. It is a great option for developers who prefer a command-line environment or for developers who want to automate the process of building and running Spring Boot applications.
