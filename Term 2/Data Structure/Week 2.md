# Data Structure
> A way of organizing, sorting, and managing data so it can be accessed and modified efficiently.
> It defines the relationships between data elements and the operations that can be performed on them.

Often, if we choose the right data structure, our algorithms can become far more efficient.
## Implementing Data Structures
In this course, we'll be studying and implementing many different data structures. The Java collections API gives us some guidelines on the methods we should include in our data structures.

Java includes a implementation of common data structures in **Collections Framework**. The collections framework implements a number of very useful data structures which we will study and use throughout this course. For now you just need to be aware of its existence.

# Java Collection Framework
Java Collections Framework (JCF)
- Provides a unified architecture for storing and manipulating groups of objects.
- Includes interfaces, implementations (classes), and algorithms.
- Supports operations such as searching, sorting, and iteration.

## Core Interfaces
- **Collection**: The root interface representing a group of objects.
- **List**: Ordered collection (e.g., ArrayList, LinkedList).
- **Set** - Unordered collection of unique elements (e.g., HashSet, TreeSet)
- **Queue**: Collection designed for holding elements prior to processing (e.g., PriorityQueue)
- **Map** Key-value pairs (e.g., HashMap, TreeMap)

Key Points
- Interfaces define the functionality; implementations provide concrete behavior.
- Algorithms are defined in terms of these interfaces.
- We will be implementing some of these interfaces ourselves.

# Collection Interface
## Iterators
An interface that provides methods for traversing collections.
### Key Methods:
- `hasNext()`: Checks if there are more elements
- `next()`: Return the next element.
- `remove()`: Removes the last returned element( optional).
### Enhanced for Loop:
Simplifies iteration over collections implementing `Iterable`
	Example : For (String s : list) {System.out.println(s)}
## List Iterators
An interface that extends `Iterator` with additioanol methods for bidirectional traversal.

### Key Methods:
- `hasPrevious()`: Checks if there are elements before the current position.
- `previous()`: Returns the previous element.
- `add(E e)` : Inserts the specified elements
- `set(E e)`: Replaces the last returned element
### Use Case:
Ideal for traversing and modifying `List` Collections (e.g., `ArrayList, LinkedList`)

# Why Study Data Structures
Data structures are the foundation of efficient algorithms.
They allow us to model and solve real-world problems effectively.
Understanding their use cases help us choose the right tool for the job
# Lists
An list is an ordered collection of elements, where duplicates are allowed. 
Elements are indexed, typically starting from 0.
## Operations
- Access: `get(index) (list[2])`
- Insertion: Add elements at a specific position
- Deletion: Remove elements by value or index.
- Traversal: Iterate through al elements.
# Array Lists
## Use Case
1. Random Access
	If you need fast access to elements by index($O(1)$ lookup), ArrayList is better as it provides direct access to any elements.
2. Memory Efficiency
	ArrayLists have lower memory overhead compared to linked lists.
3. Stable Size
	If list is relatively static or has a known size or growth pattern, an ArrayList can be more efficient due to its simple and contiguous memory structure
## Run Time
If we don't need to resize:
Access: $O(1)$
Insertion (at end): $O(1)$
Insertion (at arbitrary index) $O(n)$
Deletion (at end): $O(1)$
Deletion (at arbitrary index): $O(n)$
Traversal: $O(n)$

If we do need to resize, then we have an $O(n)$ operation to copy over all existing elements
# Linked Lists
![[Pasted image 20260113134800.png]]
Linked lists maintain a set of nodes, each of which hold data and a reference to the next node.

How memory is allocated in Linked vs ArrayList
![[Pasted image 20260113134903.png]]
## Time Complexity
Access: $O(n)$
Insertion (at end): $O(1)$
Deletion (at end): $O(1)$
Deletion (at arbitrary index): $O(n)$
Traversal: $O(n)$
## Usecase
1. Frequent Insertion/Deletions: If you application requires frequent insertion/deletion. Linked list is more efficient 
2. Memory Allocation
	Linked List used dynamic memory allocation and doesn't require a contiguous block of memory. If you are dealing with a situation where memory is fragmented or grow linked list is better

# Doubly Linked Lists
![[Pasted image 20260113135220.png]]
## Runtime


![[Pasted image 20260113135229.png]]
# Stacks
![[Pasted image 20260113135528.png]]
A stack is a collection of elements with LIFO (Last-In, First-Out) Behavior
Elements are added and removed from the same end, called the *top*

## Core Operations
- `push(x)`: Add elements x to the top.
- `pop()`: Remove and return the top element.
- `peek()`: Return the top element without removing it.
- `isEmpty()`: Check if the stack is empty. 
## Applications
- Expression evaluation and conversion (e.g., infix to postfix)
- Backtracking (e.g., browser history, recursion). 
- Undo Operations in text editors.
- Depth-First Search
## Time Complexity of Stacks
### Array-based Implementation (assuming we don't resize)
- `push`:$O(1)$
- `pop`: $O(1)$
- `peek`: $O(1)$
### Linked List Implementation
- `push`:$O(1)$
- `pop`: $O(1)$
- `peek`: $O(1)$
# Queues
![[Pasted image 20260113135929.png]]
A queue is a collection of elements with FIFO (First-In, First-Out) behavior
Elements are added at the *rear* and removed from the *front*.
## Core Operations
- `enqueue(x)`: Add element *x* to the rear.
- `dequeue()`: Remove and return the front element.
- `peek()`: Return the front element without removing it.
- `isEmpty()`: Check if the queue is empty.
## Applications
- Task scheduling (e.g., CPU scheduling, printer queues).
- Breadth-first search (BFS) in graph
- Handling asynchronous data (e.g., message queues).

## Circular Queue
![[Pasted image 20260113140054.png]]
## Time Complexity of Queues
### Circular Queue Implementation
- enqueue: $O(1)$
- dequeue: $O(1)$
### Linked List Implementation
- enqueue: $O(1)$
- dequeue: $O(1)$
## Why Choose one over the other?
# Comparison of Lists, Stacks, and Queues
## Key Differences:
**Lists**: Flexible insertion and access at any index.
**Stacks**: LIFO behavior; suitable for backtracking and nested operations.
**Queues**: FIFO behavior; ideal for scheduling and sequential processing.
## Use Cases
**Lists**: General-purpose storage.
**Stacks**: Expression Parsing, undo operations
**Queues**:Tasks Scheduling