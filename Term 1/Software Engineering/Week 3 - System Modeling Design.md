# Software Design
In the general sense, **design** can be views as a form of a problem solving process

### Basic Steps of the design Process
#### Architectural Design (HLD,TLD)
describes how software is organized into components
#### Detailed Design
describes the desired behavior of these components
## Low Coupling
Coupling is a measure of **interdependence** among components in a computer program
![[Pasted image 20250909093958.png]]
#### Before Decoupling
A change in one part of the system affects other parts, making the code harder to maintain and extend
#### After Decoupling
The code is more flexible, easier to maintain, and allows for changes in one part of the system without affecting others
## Cohesion
Cohesion is a measure of **strength** of **association** of the **elements within** a **component**
![[Pasted image 20250909095026.png]]
### Problem with Low Cohesion
- Difficult to reuse
- hard to maintain
### Benefits of High Cohesion
- Easier to maintain
- Single responsibility
- Reusability
- More testable
## Abstraction
**Abstraction** is generally defined as **a view** of an object that **focuses** on the **information relevant to a particular purpose** and **ignores** the **remainder of the information**

Hiding the implementation details and showing only the essential features of an object. It allows users to interact with the object without needing to know how it works internally
#### Problems
Too much details
#### Benefits
Simplified Interface
Easier to use
## Encapsulation
**Encapsulation** means **grouping** and **packaging** the **internal details** of an **abstraction** and **making** those details **inaccessible** to external entities.
Bundling of data (attributes) and the methods (functions) that operate on that data into a single unit (class) and restricting access to some of the object's components
#### Problems
- No Control
- Exposure of internal state
#### Benefits
- Controlled Access
- No unwanted access to internal states.
# Software Modeling
## Structured Modeling
### Class Diagram
# Behavioral Modeling
## Sequence Diagram
## State Diagram