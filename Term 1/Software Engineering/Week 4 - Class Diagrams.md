# Class Diagram
![[Pasted image 20250923084112.png]]
- `-` private
- `+` public
- `#` protected (can be  used by same class or subclass)
- `~` package (any other class as long as in the same package)
# Multiplicity
In UML show relationships
## Aggregation
Represent: Part-whole relationships
The 'whole' side is often called the assembly or the aggregate

(Aggregate common attributes to order class)
## Composition
A composition is a strong kind of aggregation
- If a building object is destroyed the rooms are destroyed
- Rooms cannot exist independently
## Generalization
Allows you to create a hierarchy where subclasses share common behaviors and attributes from a parent class, but each subclass can implement its specific behavior
![[Pasted image 20250923084523.png]]
# Sequence Diagrams
![[Pasted image 20250923084716.png]]
A **sequence diagram** is a type of diagram that illustrates how objects or classes within a system interact over time:
	- Document processes
	- Understand the requirement of a new program
Shows interaction in the order they take place, hence sequence
## Creating a Sequence Diagram
![[Pasted image 20250923085015.png]]
1. Identify Actors and Objects
2. Lifelines
	- Life lines are vertical dashed line that represent the existence of actors and object
3. Messages and Interaction
	- Show interaction between objects and message
	- return messages
4. Alternative frames for conditional logic
	- Show different potential outcome
5. Activation Boxes
	- Represents when an object is actively processing
# State Diagram
A state diagram is a technique used to describe how a system behaves and responds to events

It is based on assumption that a system has a finite number of states and the events (stimuli) may cause a transition from one state to another.

A State Diagram has 3 key components
![[Pasted image 20250923085653.png]]
- State Name
- State Variables
- State Activates

![[Pasted image 20250923085821.png]]

# Software Architectures
To create a reliable, secure and efficient product, you need to pay attention to architectural design which includes
- Its overall organization
- how  the software is decomposed into components
- The technologies that you use to build the software
The architecture of a software product affects its performance usability, security, reliability and maintainability

## Definition of Software Architecture
IEEE
Architecture is the fundamental organization of a software system embodied in its components, their relationships to each other and to the environment
Ralph Johnson
	Architecture is about important stuff

## Software Architecture and Components
A component is an element that implements a coherent set of functionality or features

Software component can be considered as a collection of one or more services that may be used by other components
When designing software architecture, you don't have to decide how an architectural element or component is to be implemented
Rather you design the component or interface and leave the implementation of that interface to a later stage of development process.

Why is architecture important
- Mimizing complexity should be an important goal for architectural designers
![[Pasted image 20250923092814.png]]
## Restrictions
Definition 
Restrictions are the **non-negotiable boundaries** within which the system must be designed. These come from various sources:
**Technical**
	The system must run on specific hardware or use certain techonologies
**Business** 
	The system must meet a budget or deliver within a tight deadline.
**Regulatory**
	The system must comply with industry standards or government regulations