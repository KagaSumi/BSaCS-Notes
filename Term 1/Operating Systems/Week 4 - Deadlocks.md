# Principles of deadlock
The **permanent** blocking of a set process that either compete for system resources or communicate with each other

A set of processes is deadlocked when each process in the set is blocked awaiting an event hat can only be triggered by another blocked process in the set
Permanent because none of the events is ever triggered
No efficient solution in the general
## Resource Categories
Resources can be categorized as
### Reusable 
Can be safely used by only one process at a time and is not depleted by that use 
	Processors, I/O Channels, main and secondary memory, devices, and data structures such as files, databases, and semaphores
### Consumable
One that can be created (produced) and destroyed (consumed)
	Interrupts, signals, messages, and information in I/O Buffers
## Deadlock Approaches
There is no single effective strategy that a can deal with all types of deadlock
3 Common approaches
### Deadlock Prevention
Disallow one of the three necessary conditions for deadlock occurrence, or prevent circular wait condition from happening
### Deadlock Avoidance
Do not grant a resource request if this allocation might lead to deadlock
### Deadlock Detection
Grant resources requests when possible, but periodically check for the presence of deadlock and take action to recover
## Conditions for Deadlock
### Mutual Exclusion
- Only one process may use a resources at a time
- No process may access a resource until that has been allocated to another process
### Hold-and-Wait
- A process may hold allocated resources while awaiting assignment of other resources
### No Pre-emption
- No resources can be forcibly removed from a process holding it
### Circular Wait
- A closed chain of processes exists, such that each process holds at least one resource needed by the next process in the chain
# Deadlock prevention
There are two ways to prevent Deadlocks
## Indirect 
Prevent the occurrence of one of the three necessary conditions
## Direct
Prevent the occurrence of a circular wait
## Condition Prevention
### Mutual Exclusion
- If access to a resources requires mutual exclusion, then mutual exclusion must be supported by the OS
- Some resources, such as files, may allow multiple accesses for reads but only exclusive access for writes
- Even in this case, deadlock can occur if more than one process requires write permissions
### Hold-and-Wait
Can be prevented by requiring a process request all its required resources at once and blocking the process until all request can be granted simultaneously
### No Pre-emption
If a process holding a certain resources is denied a further request, that process must release its original resources and request them again

OS may preempt the second process and require it to release its resources
### Circular Wait
 The circular wait condition can be prevented by defining a linear order foo resources types
# Deadlock Avoidance
Allows the 3 necessary conditions but makes judicious choices to assure that deadlock point is never reached

A decision is made dynamically whether the current resource allocation request will if granted, potentially lead to a deadlock

Allows the three necessary conditions but makes judicious choices to assure that deadlock point is never reached
Requires knowledge of future process request
## Approaches
### Process Initiation Denial
Do not start a process if its demands might lead to deadlock

A process is only started if the maximum claim of al current processes plus those of the new process can be met.

This strategy is hardly optimal because it assumes the worst that all process will make their maximum claims together.
### Resource Allocation Denial
Do not grant incremental resource request to a process if this allocation might lead to deadlock

This strategy of resource allocation denial, is also known as **banker's algorithm**

**State** of the system reflects the current allocation of resources to processes

**Safe State** is one in which there is at least one sequence of resources allocations to processes that does not result in a deadlock
**Unsafe State** is a state that is not safe
![[Pasted image 20250926140146.png]]
## Deadlock Avoidance Advantages & Restrictions
### Pros
It is not necessary to pre-empt and rollback processes, as in deadlock detection
It is less restrictive than deadlock prevention
### Cons
Maximum resource requirement for each process must be stated in advance
Processes under consideration must be independent with no synchronization requirements
There must be a fixed number of resources to allocate
No process may exit while holding resources

# Deadlock Detection
**Prevention** Strategies are very conservative
	Solutions by limiting access to resources and by imposing restrictions on process

**Detection** strategies do the opposite
	They don't limit resource access or restrict process actions
	Resource request are granted to processes whenever possible
	Periodically the OS performs an algorithm that allows it to detect the circular wait condition.
## Deadlock Detection Algorithm
### Pros
Leads to early detection and is relatively simple

### Cons
Frequent Checks consume processor time

## Recovery Strategies
Once a deadlock has been detected, some strategy is needed for recovery
- Abort all deadlocked processes
- Back up each deadlocked process to some previously defined checkpoint and restart all processes
- Successively abort deadlocked processes until deadlock no longer exists
- Successively pre-empt resources until deadlock no longer exists
# Integrated Deadlock Strategy
Rather than attempting to design an OS facility that employs only one of these strategies, it might be more efficient to use different strategies in different situations

Group resources into a number of resouce classes

Use linear ordering strategy defined previously for the prevention of circular wait to prevent deadlocks between resource classes

Within a Resource Class use the algorithm that is most appropriate for that classes
## Classes of resources
### Swappable Space
Blocks of memory on secondary storage for use in swapping processes
### Process Resources
Assignable devices, such as tape drives, and files
### Main Memory
Assignable to processes in pages or segments
### Internal Resources
Such as I/O Channels
## Class Strategies
### Swappable Space
- Prevention of deadlocks by requiring that all of the required resources that may be used by allocated at onetime, as in the hold-and-wait prevention strategy

This strategy is reasonable if the maximum storage requirements are known

### Process Resources
- Avoidance will often be effective in this category, because its reasonable to expect process to declare ahead of time the resources that they will require in the class
### Main Memory
- Prevention by preemption appears to be the most appropriate strategy for main memory
- When a process is preempted, it is swapped to secondary memory freeing space to resolve dead lock
### Internal Resources
- Prevention by means of resource ordering can be used
# Dining Philosophers Problem
![[Pasted image 20250926144601.png]]
No two philosophers can use the same fork at the same time (**mutual exclusion**)
No philosopher must starve to death (**avoid deadlock and starvation**)

# UNIX concurrency mechanisms
Unix provides a variety of mechanisms for interprocessor communication and synchronization including
- Pipes
- Messages
- Shared memory
- Semaphores
- Signals
**Pipes, essages, and Shared memory**  can be used to <u>communicate data</u> between processes, whereas **semaphores and signals** are used to <u>trigger actions</u> by other processes.
## Pipes
A Circular Buffers allowing two processes to communicate on the producer-consumer model
	- FIFO queue, written by one process and read by another

## Messages
A Block of bytes with an accompanying type
	- UNIX provides `msgsnd` and `msgrcv` system calls for processes to engage in message passing
	- Associated with each process is a message queue, which functions like a mailbox
## Shared Memory
Common block of virtual memory shared by multiple processes
	- Fastest form of interprocess communication
	- Permission is read-only or read-write for a process
	- Mutual exclusion constraints are not part of the shared-memory facility but must be provided by the processes using the shared memory
## Semaphores
[[Week 3 - Concurrency]]
## Signals
A software mechanism that informs a process of the occurrence of asynchronous events
	- A signal is delivered by updating a field in the proces table for the process to which the signal is being sent
	- Signals are similar to hardware interrupts, but do not employ priorities

### A process may respond to a signal by:
- Performing some default action
- Executing a signal-handler function
- Ignoring the signal
# Linux kernel concurrency mechanisms
## Real-time (RT) Signals
Linux includes all of the concurrency mechanisms found in other UNI systems
	- Including pipes, messages, shared memory, and signals
Linux also supports a special type of signaling knowing as real-time (RT) signals

RT signals differ from standard UNIX signals in 3 primary ways:
1. Signal delivery in priority order is supported
2. Multiple signals can be queued
3. With standard signals, no value or message can be sent to the target process - it is only a notification.
With RT signals it is possible to send a value along with the signal
## Linux Kernel Concurrency Mechanisms
Linux also includes a rich set of concurrency mechanisms specifically intended for use when a thread is executing in kernel mode.

## Linux Kernel Concurrency Mechanisms
- Atomic Operations
- Spinlocks
- Semaphores
- Barriers
- The RCU (Read-Copy-Update)
### Atomic Operations
- Linux provides a set of operations that guarantee atomic operations on a variable
- These operations can be used to avoid simple race conditions
- Atomic operations execute without interruption and without interference
- Simplest of the approaches to kernel synchronization
#### Two types of atomic operations
##### Integer Operation
- Operates on a integer variable
-  Typically used to implement counters
##### Bitmap Operation
- Operate on one of a sequence of bits at an arbitrary memory location indicated by a pointer variable

### Spinlocks
- Most common technique for protecting a critical section in Linux
- Can only be acquired by one thread at a time
	- Any other thread will keep trying (spinning) until it can acquire the lock
- Built on a integer location in memory that is checked by each thread before it enters its critical section
	- If the value is 0, then it will set to 1 and enter Critical Section.
	- If not 0 then it will wait until integer is 0
- Effective in situations where the wait time for acquiring a lock is expected to be very short.

#### Disadvantages
- Locked-out threads continue to execute in a busy-waiting mode
### Semaphores
At the User Level:
	Linux provides a semaphore interface corresponding to that in UNIX SVR4
Internally:
	Linux provides and implementation of semaphores for its own use. That is, code that is part of the kernel can invoke kernel semaphores.
	These kernel semaphores cannot be accessed directly by the user program via system calls.
	They are implemented as functions within the kernel and are more efficient than user-visible semaphores

#### Types of Semaphore Linux Provides
- Binary Semaphore
- Counting Semaphores
- Reader-Writer Semaphores
### Barriers
To enforce the order in which instructions are executed, Linux provides the memory barrier facility
Some operation are defined for this facility e.g. the `rmb()` operation ensures that no reads occur across the barrier defined by the place of the `rmb()` in the code
### The RCU (Read-Copy-Update)
The RCU mechanism provides access for multiple readers and writers to a shared reasource

The shared resources that the RCU mechanism protects must be accessed via a pointer
# Solaris thread synchronization
In addition to the concurrency mechanism of UNIX SVR4, Solaris supports 4 thread synchronization primitives
- Mutual exclusions (mutex) locks
- Semaphores
- Readers/writer locks
- Condition variables
## Mutual exclusions (mutex) locks
Used to ensure only one thread at a time can access the resource protected by the mutex

The thread that locked the mutex must be the one to unlock it

A thread attempts to acquire a mutex lock by executing the `mutex_enter primitivbe`

Default blocking policy is a spinlock

### Mutex operations
`mutex_enter()` Acquires the lock, potentially blocking if it is already held
`mutex_exit()` Releases the lock, potentially unblocking a waiter
`mutex_tryenter()` Acquires the lock if it is not already help

`mutex_tryenter()` permits the programmer to use a busy-wait approach for user-level threads, which avoids blocking the entire process because one thread is blocked
## Semaphores
`sema_p()` Decrements the semaphore, potentially blocking a thread
`sema_v()` Increments the semaphore, potentially unblocking a thread
`sema_tryp()`Decrements the semaphore if blocking is not required
## Readers/writer locks
Allows multiple threads to have simultaneous read-only access to an object protected by the lock

Allows a single thread to access the object for writing one time, while excluding all readers
	- When lock is acquired for writing it takes on the status of a write lock
	- If one or more readers have acquired the lock its status is read lock
The primitives are as follows:
`rw_enter()` Attempts to acquire a lock as a reader or writer
`rw_exit()` Release a lock as a reader or writer
`rw_tryenter()`Acquires the lock if blocking is not required
`rw_downgrade()` A thread that has acquired a write lock converts it to a read lock. Any waiting writers writer remain until this thread release the lock. If there are no waiting writers, the primitive wakes up any pending readers.
`rw_tryupgrade()` Attempt to convert a reader lock to a writer lock
## Condition variables
A conditional variable is used to wait until a particular condition is true

Condition variables must be used in the conjunction with am mutex lock
![[Pasted image 20250926151420.png]]