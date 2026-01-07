
# `SpringApplication.run( )`

When you invoke the `run` method of `SpringApplication`, it creates a `WebApplicationContext` for your web application. If you look at the implementation of the `run` method, you will see that its return type is `ConfigurableApplicationContext`. ==This interface is implemented directly or indirectly by all the Application Contexts==

The type of `WebApplicationContext` that is created depends on the type of your web application. For example, if your application is a Servlet-based web application, Spring Boot creates a `AnnotationConfigServletWebServerApplicationContext`. On the other hand, if your application is a Reactive web application, Spring Boot creates a `AnnotationConfigReactiveWebServerApplicationContext`. This way, Spring Boot determines the type of your web application and creates the appropriate `WebApplicationContext` accordingly.

I understand that you’re curious about how Spring Boot determines the type of web application. It’s a great question, and I’d be happy to explain it to you.

Let me explain this to you, Spring Boot internally classifies web applications into two categories: Reactive and Servlet applications using the `WebApplicationType` enumeration. In the constructor of the SpringApplication class you will find this line :

``` ln:false
this.webApplicationType = WebApplicationType.deduceFromClasspath();
```

spring-boot uses the `deduceFromClasspath()` method to determine the type of web application based on the presence of certain dependencies on the classpath. If it finds the `spring-boot-starter-web` dependency, it will assume that the application is a Servlet-based web application and set the `webApplicationType` attribute to `SERVLET`. Similarly, if it finds the `spring-boot-starter-reactive` dependency, it will assume that the application is a reactive web application and set the `webApplicationType` to `REACTIVE`. If none of these dependencies are found, they `webApplicationType` will be set to `NONE`.

**what’s happened after the context get created ?**
The `this.refreshContext(context)` method in the `run()` method of `SpringApplication` triggers a refresh of the application context. This means that the application context will be initialized and configured with all the necessary beans and components required to run the application.

During the refresh process, Spring will scan the application’s classpath for all components that have been annotated with `@Component` or other annotations, and will create and configure instances of those components as necessary. It will also load and configure any other beans that are defined in the application context, such as those defined in XML configuration files or through Java configuration classes.

Once the application context has been fully refreshed and initialized, the application can start handling requests or performing other tasks.
