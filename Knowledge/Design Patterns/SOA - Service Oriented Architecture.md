
**What is Service Oriented Architecture ?**
Service-oriented architecture (SOA) is a software development architectural style that makes services reusable and lets them communicate across different platforms and languages to form new applications.

**For Example,** multiple business processes in an organization require the user authentication functionality. Instead of rewriting the authentication code for all business processes, you can create a single authentication service and reuse it for all applications.

**There are four main components in service-oriented architecture -**
1. **Service :** Services are the basic building blocks of SOA. They can be private — available only to internal users of an organization — or public — accessible over the internet to all. Individually, each service has three main features.
	- **Service implementation:** The service implementation is the code that builds the logic for performing the specific service function, such as user authentication or bill calculation.
	- **Service contract:** The service contract defines the nature of the service and its associated terms and conditions, such as the prerequisites for using the service, service cost, and quality of service provided.
	- **Service interface:** In SOA, other services or systems communicate with a service through its service interface. The interface defines how you can invoke the service to perform activities or exchange data. It reduces dependencies between services and the service requester. For example, even users with little or no understanding of the underlying code logic can use a service through its interface.
2. **Service Provider :** The service provider creates, maintains, and provides one or more services that others can use. Organizations can create their own services or purchase them from third-party service vendors.
3. **Service Consumer :** The service consumer requests the service provider to run a specific service. It can be an entire system, application, or other service. The service contract specifies the rules that the service provider and consumer must follow when interacting with each other. Service providers and consumers can belong to different departments, organizations, and even industries.
4. **Service Registry :** A service registry, or service repository, is a network-accessible directory of available services. It stores service description documents from service providers. The description documents contain information about the service and how to communicate with it. Service consumers can easily discover the services they need by using the service registry.


**Some standard protocols to implement SOA include the following:**

· Simple Object Access Protocol (SOAP)
· RESTful HTTP
· Apache Thrift
· Apache ActiveMQ
· Java Message Service (JMS) and many more.


## Enterprise Service Bus(ESB):

Most SOAs are implanted using an enterprise service bus (ESB). ESBs are so frequently used with SOAs that the terms are sometimes used interchangeably. An ESB is an architectural pattern that lets centralized software components integrate between applications. ESBs transform data models, handle routing and messaging, convert communication protocols, and manage the writing of multiple requests.

An ESB makes each one of these integrations its own service interface that new applications can reuse. Without an ESB, every application would have to connect directly to each service and service interface to perform its necessary integration or transformation, which makes building new software less efficient.

An enterprise service bus (ESB) is software that you can use when communicating with a system that has multiple services. It establishes communication between services and service consumers no matter what the technology.

**Benefits of ESB**
An ESB provides communication and transformation capabilities through a reusable service interface. You can think of an ESB as a centralized service that routes service requests to the appropriate service. It also transforms the request into a format that is acceptable for the service’s underlying platform and programming language.