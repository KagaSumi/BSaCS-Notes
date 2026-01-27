![[Pasted image 20251007083520.png]]
Issues that influence architectural decision

## Issues
### Non-functional product characteristics
security and performance
if you get these wrong, your product is unlikely to be a commercial success

### Product lifetime
If you anticipate long product lifetime, you need to create regular product revisions. you therefore need na architecture that can evolve
### Software reuse
You can save a lot of time and effort if you can reuse large compoonents from other products, open-source software
### Number of user
### Software compatibilitiy

# Architectural Complexity
Complexity in a system architecture arises because of the number of and nature of the relationships between components in that system.

*Localise relationships* If there are relationships between components A and B, these are easier to understand if A and B are defined in the same module.

When decomposing a system into components, you should try to avoid unnecessary software complexity

*Reduce shared dependencies*
Where components A and B depend on some other component or data, complexity increases because changes to the shared component mean you have to understand how these changes affect both A and B

![[Pasted image 20251007083857.png]]
# Technology Choices
## Database
If you use relational or unstructured
![[Pasted image 20251007084152.png]]
## Platform
What platform are developing for mobile or web?
o![[Pasted image 20251007084201.png]]
![[Pasted image 20251007084223.png]]
## Server
Are we using in-house servers or run it on public cloud like AWS or GCP or azure
![[Pasted image 20251007084231.png]]
## Open Source
Are there open-source components that we can use to help us implement our product
![[Pasted image 20251007084243.png]]
## Development Tools
Do our developer tools make any assumptions about the software being developed that limit your architectural choices?

# Architectural Patterns
## Layered Patterns
Most Common
Separation of concerns among component 
Each layer in the architecture forms an abstraction around the work that needs to be done to satisfy a particular business request

### Key Concepts
- Separation of concerns
- Closed layers
- Layers of isolations
![[Pasted image 20251007085905.png]]
### Cross Cutting Concerns
Cross-cutting concerns are concerns that are systemic, that is , they affect the whole system.

In a **layered architecture**, cross-cutting concerns affect all layers in the system as well as the way in which people use the system.

Cross-cutting concerns are completely different from the functional concerns represented by layers in a software architecture

Every layer has to take them into account and there are inevitably interactions between the layers because of these concerns.
### Aspect-Oriented Programming (AOP)
**Aspect** - A module that encapsulate the desired behaviour
**Join Point** - A point in the program where an aspect can eb applied, such as method execution, object instantiation
**Advice** - The code that is executed at a join point.
- Before
- After
- Around
**Pointcut** - a set of join points where an advice should be applied.
### Consideration
Architecture anti pattern sinkhole
Every layered architecture will have at least some scenarios that fall into 
### Pros and Cons
#### Pros
- Allows the replacement of entire layers as long as the interface is maintained
#### Cons
- In practice providing a clean separation between layer is difficult and a high level layer may have to interact directly with a lower level layers rather than through the layer immediately below it.
- Performance can be a problem because of multiple levels of interpretation of a service request as it is processed at each layer.
## Client Server
Client-server architectures are a type of distribution architecture that is suited to applications where clients access a shared database and business logic operations on that data
In this architecture, the user interface is implemented on the user's own computer or mobile device.
- Functionality is distributed between the client and one or more server computer

**Client** - A piece of software or application that takes the input and sends request to the servers.
**Server** - a piece of software that recieves and processes requests from clients
**Load Balancing** - Responsible for distributing incoming network traffic across a group of backend servers to optimize resource usage
![[Pasted image 20251007090820.png]]
![[Pasted image 20251007090827.png]]
### Client-server Communication
Client-server communication normally uses the **HTTP** protocol

HTTP is text-only so we send structured data ie XML or JSON
![[Pasted image 20251007090935.png]]
### Pros and Cons
#### Pros
- Separation or abstractions between client and servers
	- High interoperability
- Needs separation of functionality
	- Request validation or sanitization in client side
	- Business logic and storage on storage side.
		- Sharding, load balancing, partitioning
#### Cons
- Centralized Control
	- If the servers go down the entire service goes down
- Vulnerable to cyber attacks (e.g. DDOS)
	- number of servers is considerably smaller than the number of client
- Expensive to install and manage
## MVC (Model, View, Controller)
![[Pasted image 20251007091231.png]]
![[Pasted image 20251007091358.png]]
![[Pasted image 20251007091406.png]]
### Pros and Cons
#### Pros
- Separation of Concerns
- Parallel Development
- Reusability
- Testability
#### Cons
- Tight coupling between controller and view
- Difficulty in managing many views
## Event Driven Architecture
Distributed asynchronous architecture pattern
- Highly scalable
- Made of highly decoupled single purpose event processing components
Two common topologies:

### Mediator
![[Pasted image 20251007091524.png]]
Architecture Components
- Event Queues
- Event mediator
- Event channels
- Event processors
### Broker
![[Pasted image 20251007091532.png]]
#### Pros and Cons
##### Pros
- Scalability
- Extensibility and Flexibility
- Asynchronous Processing
- Loose Coupling
- Resilience
##### Cons
- Complexity
- Latency issues
- Event Storming
- Event Duplication

## Repository Pattern
A sharing data pattern
Sub-systems must exchange data. This may be done in two ways
	1. Shared data is held in a central database or repository and may be accessed by all sub-systems;
	2. Each sub-system maintains its own database and passes data explicitly to other sub-systems
When large amounts of data are to be shared, the repository model of sharing is most commonly used as this is efficient data sharing mechanisms
![[Pasted image 20251014083124.png]]
### Pros and Cons
#### Pros
Components can be independent
All data can be managed consistently, eg backup at the same time
#### Cons
Single point of failure
Inefficiencies in organizing all communication through the repository
	Can cause performance bottlenecks if not optimized for large scale systems.
## Pipe and Filter Pattern
### Definition
The Pipe and Filter pattern organizes data processing tasks into a series of filters, where each filter transforms the data in some way. These filters are connected by pipes, which transport data from one filter to the next.
### Purpose
To divide a complex data processing task into smaller, reusable, and independently executing components (filters_), improving modularity and flexibility.
### Key Concept
Each filter performs a discrete step in the transformation of the data, and pipes allows for the flexible connection of filters to form complex processing

### Filters
-Each filter performs a specific task on the input data and sends the result to the next filter.
Filters are designed to be independent and reusable
### Pipes
- Pipes at as conduits for data flow between filters.
- They ensure data is passed along the chain in a consistent format.
![[Pasted image 20251014083552.png]]
#### Pros and Cons
##### Pros
- Easy to scale by adding or removing filters.
- Highly reusable filters that can be applied in different pipelines.
- Clear separation of concerns with each filter focusing on a specific task
##### Cons
- Potential performance overhead due to the movement of data between filters.
- Complexity may increase with deeply nested or overly complex pipelines
- Debugging can become difficult in complex pipelines.
## Service Oriented Architecture (SOA)
### Definition
SOA is an architectural pattern where software components (services) communicate over a network to provide functionalities. Each service is contained and performs a specific business task.
### Purpose
To enable different services, often across different systems, to communicate and work together while remaining independent.
### Key Concepts
SOA emphasizes reusability, interoperability, and loose coupling between services.
### Services
- Self-contained units of functionality that expose an interface to clients.
- Services can be built using different programming languages and technologies
### Looses Coupling
- Services interact through well-defined interfaces (often using protocols likes HTTP,SOAP, or REST)
- Without depending on the internal workings of other services
### Interoperability
![[Pasted image 20251014084207.png]]
#### Pros & Cons
##### Pros
- High degree of scalability and flexibility
- Services can be reused across different applcatinos
- Independent development, deployment, and scaling of services
##### Cons
- Overhead from service communication, especially in high-latency networks
- Potential complexity when integrating multiple services.
- Requires strong governance to maintain service boundaries and avoid duplication.