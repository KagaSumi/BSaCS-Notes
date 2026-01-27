# Software Quality
Creating a successful software product does not simply mean providing useful features for users.
You need to create a high-quality product that people want to use.
Customers have to be confident that your product will not crash or lose information, and users have to be able to learn to use the software quickly and without mistakes.
# Product quality Attributes
![[Pasted image 20251104082109.png]]
## Programming for reliability
There are 3 simple techniques for reliability imrpovemnt that can be applied in any software company.
### Fault Avoidance
You should avoid introducing faults into your program.
### Input validation
You should define the expected format for user inputs and validate that all inputs conform to that format.
### Failure Management
You should implement your software so that program failures have minimal impact on product users.
# Fault avoidance
## Underlying causes of program errors
![[Pasted image 20251104082254.png]]
## Software complexity
![[Pasted image 20251104082307.png]]
## Program complexity
Complexity is related to the number of relationships between elements in a program and the type and nature of these relation ships

The number of relationships between entities is **coupling**. The higher the **coupling** the more complex the system is.

A **static** relationship is one that is stable and **does not depend** on program execution.
	Whether or not one component is part of another component is a static relation
A **Dynamic relation**, which change over time, are more complex than static relationships.
	An example of a dynamic relationship is 'calls' relationship between functions.
## Types of complexity
### Reading Complexity
This reflects how hard it is to read and understand the program
### Structural Complexity
This reflects the number of relationship between the structures (classes, objects, methods or functions) in your program.
### Data Complexity
This reflects the representation of data used and relationships between the data elements in your program.
### Decision Complexity
This reflects the complexity of the decisions in your program.
## Code Complexity
[Slide Link](https://colab.research.google.com/drive/1I9cVUiAhKxrn56zwI_WOfvYSnSnk6uDB#scrollTo=YPxzEBVccMSX)
# Complexity Reduction guidelines
## Structural complexity
- Functions should only do 1 thing and 1 thing only
- Functions should never have side effects
- Every class should have a single responsibility
- Minimize the depth of inheritance hierarchies 
- Avoid multiple inheritance
- Avoid threads (parallelism) unless necessary
## Data Complexity
- define interfaces for all abstractions.
- Define abstract data types.
- Avoid using floating-point numbers.
- Avoid using data aliases.
## Decision Complexity
- Avoid deeply nested conditional statements.
- Avoid complex conditional expressions.
## Ensure that every class has a single responsibility
- Design classes so that there is only a **single reason** to change a class
	- If you adopt this, classes will be smaller and more cohesive
	- They will therefore be less complex and easier to understand change
- Gather together things that change for the same reason
- Separate those things that change for different reasons.
# Separation of Concerns
- This means abstraction in the program should adress a separate concern and that all aspects sohuld be covered tehre.
- If a program component provides a particular service, you should make available only the information that is required to use that service (the 'what'). The implementation of the service ('the how') should be no interest to service users.
# Avoid deeply nested Conditional Statement
- Deeply nested conditional (if) statements are used when you need to identify which of a possible set of choices is to be made.
[Code Example](https://colab.research.google.com/drive/1I9cVUiAhKxrn56zwI_WOfvYSnSnk6uDB#scrollTo=Ytddss_qqthx)
# Avoid Deep Inheritance hierarchies
- Inheritance allows attributes and methods of a class be inherited by sub-classes.
- Inheritance appears to be an effective and efficient way of reusing code and making changes that affect all subclasses
- However inheritance increases the structural complexity of the code.
The main problem with deep inheritance is that you have to look through all the classes and super classes to see where it would be best to make changes. As well as other classes to see if they have any unintended interactions.
# Open-Closed Principle
Software entities (such as classes, modules, functions) should be open for extension but closed for modification.
**Open for extension**
A class or module should allow its behavior to be extended. This means that you should be able to add new functionality to a system
**Closed for modification**
Once a class or module is written and tested, you should not have to modify its existing code. Modifying existing code can introduce bugs or affect the stability of the system.
## Why OCP is important
- Reducing the risk of breaking existing code
- Making Code easier to maintain and scale
## How to apply the OPC
- Use faces or abstract classes
- Use inheritance or composition
- Avoid hard-coding logic
# Design Pattern definition
A general reusable solution to a commonly-occurring problem with a given context in software design.
## Common Types of design Patterns
### Creational Patterns
These are concerned with class and object creation. They define ways of instantiating and initializing objects and classes that are more abstract than the basic class and object creation mechanisms defined in a programming language.
### Structural Patterns
these are concerned with class and object composition. Structural design patterns are a description of how classes and objects may be combined to create larger structures.
### Behavioral Patterns
These are concerned with class and object communication. They show how objects interact by exchanging messages, the activities in a process and how these are distributed amongst the participating objects.

## Example of Creational, Structural, and Behavioral Patterns

| Pattern Name |    Type     |                                                                                                    Description                                                                                                    |
| :----------: | :---------: | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
|   Factory    | Creational  |                                                               Used to create objects when slightly-different variants of the object may be created.                                                               |
|  Prototype   | Creational  |                                              Used to create an object clone-that is, a new object with exactly the same attribute values as the object being cloned.                                              |
|    Facade    | Structural  | Used to provide a single interface to a group of classes in which each class implements some functionality accessed through the interface. Used to match semantically compatible interfaces of different classes. |
|   Mediator   | Behavioural |                                           Used to reduce the number of direct interactions between objects. All object communications are handled through the mediator                                            |
|    State     | Behavioural |                                                    Used to implement a state machine in which an object changes its behavior when its internal state changes.                                                     |
## The Observer Pattern
# The Observer Pattern

| **Element**         | **Description** |
|----------------------|-----------------|
| **Name**             | **Observer** |
| **Description**      | This pattern separates the display of an object from the object itself. There may be multiple displays associated with the object. When one display is changed, all others are notified and take action to update themselves. |
| **Problem**          | Many applications present multiple views (displays) of the same data with the requirement that all views must be updated when any one view is changed. You may also wish to add new views without the object whose state is being displayed knowing about the new view or how the information is presented. |
| **Solution**         | The state to be displayed (sometimes called the Model) is maintained in a Subject class that includes methods to add and remove observers and to get and set the state of the Model. An observer is created for each display and registers with the Subject. When an observer uses the set method to change the state, the Subject notifies all other Observers. They then use the Subject’s `getState()` method to update their local copy of the state and so change their display. Adding a new display simply involves notifying the Subject that a new display has been created. |
| **Implementation**   | This pattern is implemented using abstract and concrete classes. The abstract Subject class includes methods to register and deregister observers and to notify all observers that a change has been made. The abstract Observer class includes a method to update the local state of each observer. Each Observer subclass implements these methods and is responsible for managing its own display. When notifications of a change are received, the Observer subclasses access the model using the `getState()` method to retrieve the changed information. |
| **Things to consider** | The Subject does not know how the Model is displayed so cannot organize its data to optimize the display performance. If a display update fails, the Subject does not know that the update failed. |
# Refactoring
Changing a program to reduce its complexity without changing external behavior of the program.
- Make it more readable and more understandable

It is easier to make changes

The reality of programming is that as you make changes and additions to existing code, you inevitably increase its complexity.

# Code Smells
Indicators in code that can lead to deeper problems

| Code Smell             | Refactoring Action                                                                                                                                                                      |
| :--------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Large Classes          | Large classes may mean that the single responsibility principle is being violated. Break down large classes into easier-to-understand, smaller classes.                                 |
| Long methods/functions | Long methods or functions may indicate that the function is doing more than one thing. Split into smaller, more specific functions or methods.                                          |
| Duplicated Code        | Duplicated code may mean that when changes are needed, these have to be made everywhere the code is duplicated.                                                                         |
| Meaningless Names      | Meaningless names are a sign of programmer haste. They make the code harder to understand.                                                                                              |
| Unused Code            | This simply increases the reading complexity of the code. Delete it even if it has been commented out.                                                                                  |
| Primitive Obessession  | occurs when primitive data types (such as strings, integers, and booleans) are used excessively to represent complex concepts, rather than creating custom types or classes.            |
| Feature envy           | occurs when a method in one class is overly interested in the data or functionality of another class, leading it to frequently access or manipulate the other class’s fields or methods |