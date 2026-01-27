# Microservices
Small-scale, stateless
Single responsibility
Independent with their own database and UI management code
# Characteristics
### Self-containedo 
Microservices do not have external dependencies. They manage their own data and implement their own user interface
### Lightweight
Microservices communicate using weight protocols, so that service communication overheads are low.
### Implementation independent
Microservices may be implemented using different programming languages and may use different technologies (e.g., different types of database in their implmentation)
### Independently Deployable
Each microservice runs in its own process and is independently deployable, using automated systems.
### Business-oriented
Microservices should implement business capabilities and needs, rather than simply provide a technical service.

# Microservices Architecture
It addresses two problems with monolithic applications:
1. Rebuilding the whole system for a change
2. As the demand increase the whole system has to be scaled
## Benefits of Microservices
Microservices are self-contained and run in a separate process
	In cloud based system each cna be stopped and restarted independently
If the demand on a service increase, service replicas can be quickly created and deployed

# API Gateway
API gateway acts as a **single point of entry** for client into a system of microservices
Handling the routing, request composition, and response aggregation
This offers **security, authentication, rate limiting**
## Decomposition guidelines
Balance fine-grain functionality and system performance
Follow the common closure principle
Associate services with business capabilities
Design services so that they only have access to the data they need.

## Microservice Communication
Microservices communicate by exchanging messages.
A message that is sent between services includes some administrative information, a service request and the data required to deliver the requested service.
Services return a response to a service request messages
	An authentication service may send a message to a login service that includes the name input by the user.
	The response may be a token associated with a valid user name or might be an error saying that there is no registered user. 
# Apache Kafka
![[Pasted image 20251028082733.png]]
**Event streaming platform** for real-time data pipelines
Kafka Decouples producers and consumers of messages, enabling asynchronous communication

This enables services to communicate **via event-driven** architectures.

## Service Discovery
Services in a microservices architecture need to find each other dynamically.
Tools like **consul, eureka, and Kubernetes service discovery** can be used
Use of **registries** to map service names to instance

## Microservice Data Design
You should isolate data within each system service with as little data sharing as possible.
If data sharing is unavoidable, you should design microservices so that most sharing is read-only, with a minimal number of services responsible for data updates.

If services are replicated in your system, you must include a mechanism that can keep the database copies used by replica services consistent.


# Inconsistency management
An ACID transaction bundles a set of data updates into a single unit so that
either all updates are completed or none of them are. ACID transactions are
impractical in a microservices architecture.
The databases used by different microservices or microservice replicas need
not be completely consistent all of the time.
Dependent data inconsistency
• The actions or failures of one service can cause the data managed by
another service to become inconsistent.
Replica inconsistency
• There are several replicas of the same service that are executing
concurrently. These all have their own database copy and each updates its
own copy of the service data. You need a way of making these databases
eventually consistent' so that all replicas are working on the same data.
## Eventual Consistency
Eventual consistency is a situation where the system guarantees that the databases will eventually become consistent
You can implement eventual consistency by maintaining a transaction log.
When a database change is made, this is recoded on a pending updates log.
Other service instance look at this log, update their own database and indicate that they have made the change.
# Service Coordination
Most user session involve a series of interactions in which operations have to be carried out in a specific order

This is called a workflow


# Failure types in a Microservice
![[Pasted image 20251028083620.png]]
# Timeouts and circuit breakers
A timeout is a counter that this associated with the service requests and starts running when the request is made.
Once the counter reaches some predefined value, such as 10 seconds, the calling service assumes that the service request has failed and acts accordingly.
The problem with the timeout approach is that every service call to a failed service is delayed by the timeout value so the whole system slows down.

Instead of using timeouts explicitly when a service call is made, we suggest using a circuit breaker. Like an electrical circuit breaker, this immediately denies access to a failed service without the delays associated with timeouts. 