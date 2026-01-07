
## What is Spring framework?

Spring is a light weight, loosely couples, integrated framework used for developing web applications. Spring helps in reducing the complexity of developing Enterprise level application. Spring is also called as ‘**Framework of Frameworks**’ because it provides support for multiple other frameworks such as **Hibernate**, **Struts**, **EJB**, etc...,

Spring architecture follows a principle of Modularity that contains multiple modules. This Modular architecture allows the developers to select only the required modules according to their needs and leave the rest. This makes our application lightweight and focused. _(Example: if we want to only use the Spring Web module, we don't have to add a Data access module to our project)._ 

## What are features of Spring framework?

The features of spring framework are...
1. Inversion of control
2. Dependency Injection
3. Aspect oriented programming
4. Spring MVC
5. Transaction management

## What are spring Beans?
According to the official documentation in spring.io,
> In Spring, the objects that form the backbone of your application and that are managed by the Spring IoC container are called beans. A bean is an object that is instantiated, assembled, and managed by a **Spring IoC container**. Otherwise, a bean is simply one of many objects in your application.

A **_Spring bean_** is an instance of a Java class which is created and managed by a Spring container. Once a Java class is marked as a Spring bean, the container takes over the following operations:  
- Loading the class.
- Creating an object of the class.  
- Managing the object.
- Destroying the object when no longer needed.

## What is Spring bean lifecycle?

The bean life cycle refers to when & how the bean is instantiated, what action it performs until it lives, and when & how it is destroyed.

**Bean life cycle is managed by the Spring container.** 
1. When we run the program then, first of all, the spring container gets started.
2. The Spring container creates an instance of the bean. This typically involves using the bean's no-argument constructor.
3. Spring injects any dependencies the bean has into its properties. This is achieved through Dependency Injection.
4. The bean is now ready and can be used by your application.
5. Ultimately, the bean is destroyed with the closure of the spring container.

## Spring bean scopes

The Spring Framework has five scope supports. They are:

- **Singleton:** The scope of bean definition while using this would be a single instance per IoC container.
- **Prototype:** Here, the scope for a single bean definition can be any number of object instances.
- **Request:** The scope of the bean definition is an HTTP request.
- **Session:** Here, the scope of the bean definition is HTTP-session.
- **Global-session:** The scope of the bean definition here is a Global HTTP session.

Note: The last three scopes are available only if the users use web-aware ApplicationContext containers.

## What is the default bean scope in spring framework?

The default bean scope in Spring is singleton. This means that only one instance of a bean will be created and managed by the Spring container, regardless of how many times it is requested. This scope is useful for beans that are stateless, meaning that they do not maintain any internal state and can be safely shared across different parts of the application.

## What is IOC?
**Inversion of Control (IoC)** is a design principle in which a software component is designed to receive its dependencies from an external source, rather than creating them itself. In Spring, this is achieved through the use of **Dependency injection (DI)**.

The container is responsible for creating the objects, wire them together, configure them, and manage their complete life cycle from creation till destruction. The Spring container uses DI to manage the components that make up an application. These objects are called Spring Beans.

## What is Dependency Injection?

Dependency injection is a fundamental aspect of spring framework, through which the spring container injects one object into other objects. Simply put, this allows for loose coupling of components and move the responsibility of managing the components onto the container.

In Dependency Injection, you do not have to create your objects but have to describe how they should be created. You don’t connect your components and services together in the code directly, but describe which services are needed by which components in the configuration file. The IoC container will wire them up together.

**Dependency injection can be achieved in two ways:**
1. **Constructor dependency injection**
	In this method, dependencies are passed as a parameter to the class’s constructor. This ensures that all the dependencies are injected upon the instantiation of an object. We utilise the `@Autowired` Annotation on top of the constructors to achieve this.
2. **Setter dependency injection**
	This is another way to inject dependencies and its done by using a `setter()` or `getter()` methods to do so. We can do so by annotating a `setter()` method with `@Autowired` and it’ll do the work. A key point here is that, dependencies will only be injecting when the setter/getter methods are called.


## Spring configuration file

A Spring configuration file is an xml file that contains configuration information for a Spring application. This information can include bean definitions, property values, and other settings. 

## BeanFactory and ApplicationContext

Spring framework provides two IOC container for configuring, managing, and manipulating beans. One is **BeanFactory** and the other is **Application Context**.

| BeanFactory                                                                     | ApplicationContext                                                                                             |
| ------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| BeanFactory is the root interface for accessing spring container.               | The Spring Application Context is an extension of the BeanFactory, offering advanced integration capabilities. |
| BeanFactory loads beans on demand when `getBean()` method is explicitly called. | Application context loads beans on start up of the spring application.                                         |
| BeanFactory doesn't provide support for annotation based dependency injection.  | Application context provides support for annotation based dependency injection.                                |
| BeanFactory doesn't support Internationalization.                               | Application context supports Internationalization.                                                             |
| BeanFactory doesn't provide support reading multiple configuration files.       | Application context provides support for reading multiple configuration files.                                 |

## What is Spring AOP?

Spring AOP (Aspect-Oriented Programming) offers a way to modularize cross-cutting concerns. Cross-cutting concerns are aspects of software that affect multiple modules or components. They're functionalities that are needed in various parts of your application, such as logging, security, and transaction management.  Spring AOP allows developers to separate the implementation of these cross-cutting concerns from the business logic of the application, making the code more modular and easier to understand.

## What is Spring Transaction management?

In simpler terms, the transaction management feature in the Spring framework helps you ensure that when you're making changes to your database, either all those changes are saved successfully, or none of them are. This prevents situations where only some changes are saved, leaving your data in an inconsistent state.

Imagine you're transferring money between two bank accounts. With transaction management, if something goes wrong during the transfer, like an error or a system crash, the entire transaction is rolled back, so neither account ends up with the wrong balance.

In the Spring framework, transaction management is achieved primarily through two approaches:

1. **Programmatic Transaction Management**: This involves explicitly coding transaction demarcation using Spring's `TransactionTemplate` or directly through the `PlatformTransactionManager` interface. Developers manually control transaction boundaries in their code by starting, committing, or rolling back transactions.

2. **Declarative Transaction Management**: This approach involves configuring transactions declaratively, usually via annotations like `@Transactional`. Developers annotate methods or classes to specify transactional behaviour. Spring AOP (Aspect-Oriented Programming) intercepts method calls and automatically starts, commits, or rolls back transactions based on the configuration.

Both approaches offer flexibility and ease of use, with declarative transaction management being more commonly used due to its simplicity and reduced boilerplate code.


## Constructor Dependency Injection or Setter Dependency Injection

Since you can mix constructor-based and setter-based DI, it is a good rule of thumb to use constructors for mandatory dependencies and setter methods or configuration methods for optional dependencies. Note that use of the `@Autowired` annotation on a setter method can be used to make the property be a required dependency; however, constructor injection with programmatic validation of arguments is preferable.

**The Spring team generally advocates constructor injection, as it lets you implement application components as immutable objects and ensures that required dependencies are not null**. Furthermore, constructor-injected components are always returned to the client (calling) code in a fully initialized state.

## Lazy loading vs Eager loading

In Spring, beans can be either **lazy-loaded or eager-loaded**. Lazy loading means that a bean is not created until it is first requested by the application. Eager loading means that a bean is created when the application starts up.

The default behaviour in Spring is to Eager-load beans. This can improve the performance of the application because it means that only the beans that are actually needed are created. However, lazy loading can also make the application more difficult to debug because it can be hard to track down which beans have been created and when.

**Eager loading can be useful for beans that are needed by the application as soon as it starts up**. For example, an application might need to connect to a database as soon as it starts up. In this case, it would make sense to eagerly load the bean that is responsible for connecting to the database.

## What is Autowiring
In Spring, Autowiring is a feature that allows the container to automatically resolve and inject dependencies into beans without the need for explicit configuration.

**How `@Autowire` annotation work?** 
The `@Autowired` annotation works by using reflection to find the appropriate dependency to inject. It will first look for a bean with the same type as the dependency. If it cannot find a bean of the same type, it will look for a bean with a qualifier that matches the name of the dependency. If it still cannot find a bean to inject, it will throw an exception.

**Limitations of Autowiring**
- Dependencies are specified using `<constructor-arg>` and `<property>`  settings can override Autowiring.
- Primitive data types, Strings, and Classes can’t be Autowired.


## How is the configuration meta data provided to the spring container?
There are 3 ways of providing the configuration metadata to Spring framework. They are as follows:

**XML-Based Configuration :** The bean configurations and their dependencies are specified in XML configuration files. This starts with a bean tag as shown below:
``` ln:false
<bean id="beanName" class="org.intervuewBit.firstSpring.InterviewBitBean">
	<property name="name" value="InterviewBit"></property> 
</bean>
```


**Annotation-Based Configuration :**  Instead of the XML approach, the beans can be configured into the component class itself by using annotations on the relevant class, method, or field declaration. Annotation wiring is not active in the Spring container by default. This has to be enabled in the Spring XML configuration file as shown below:
``` ln:false
<beans>
	<context:annotation-config/> <!-- bean definitions go here -->
</beans>
```

**Java-Based Configuration :** Spring Framework introduced key features as part of new Java configuration support. This makes use of the `@Configuration` annotated classes and `@Bean` annotated methods.
 - `@Bean` annotation has the same role as the `<bean/>` element. 
 - Classes annotated with `@Configuration` allow to define inter-bean dependencies by simply calling other `@Bean` methods in the same class.
