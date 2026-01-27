# Concurrency
OS Design is concerned with the management of process and threads
## MultiProgramming 
- The management of multiple processes within a **uniprocessor** system
## MultiProcessing
- The management of multiple processes within a multiprocessor
## Distributed Process
- The management of multiple processes executing on multiple distributed computer system

## Concurrency Design Issues
- Communication among processes
- Sharing of and competing for resources
- Synchronization of the activities of multiple processes, and allocation of processor time  to processes
## Concurrency Arises in Three Different Contexts
1. Multiple Applications
2. Structured Applications
3. Operating System Structure
## Definitions
![[Pasted image 20250919133743.png]]
# Mutual Exclusion Software Approaches
Software approaches can be implemented for concurrent processes that execute on a single-processor or a multiprocessor machine with shared main memory

These approaches usually assume elementary **mutual exclusion** at the memory access level
- Simultaneous access to the same location in main memory are managed b a memory arbiter, although th eorder of access granting is not specified ahead of time

## Attempt 1
![[Pasted image 20250919134341.png]]
Flip flop between Process 0 and Process 1
### Drawback
- Process must **strictly alternate** in their use of their critical section,
- If one process fails, the other process is permanently blocked
### Flaw
the flaw is they store the name of the process that may enter its critical section
## Attempt 2
![[Pasted image 20250919134350.png]]
We change to each process to handle their own state P0 affect flag 0 (for P0)

### Drawbacks
- If a process fails inside is critical section or after setting its flag to true. The other process will become stuck
- Doesn't guarantee mutual exclusion
	- If Critical is long, since we flip the flag0 before we enter our critical, it process 1 can access critical before we finish
## Attempt 3
![[Pasted image 20250919135408.png]]
Block Process 1 , check if blocked (if process 1 is in Critical secition) if not go work and remove block
### Drawbacks
- If both processes set their flags to true before either executes the while statements, each will think the other is working on critical section causing a **deadlock**
## Attempt 4
![[Pasted image 20250919135436.png]]
Show desire to enter Critical Section
If Process 1 is in Critical we add a delay to pulse a intent to access the critical Process 1 finishes up and clears the block we proceed and continue
### Drawbacks
- This blocking can continue indefinitely causing a **livelock**, not a deadlock because it alternates between process. Eventually the delay offset will clear the lock
## Dekker's Algorithm
![[Pasted image 20250919135925.png]]
Block Other process,
If not my turn then we don't block and wait until our turn
If it is our turn we keep blocking and enter critical.

## Peterson Algorithm for Two Process
Dekker's Algorithm Solves the mutual exclusion problem, but it was confusing
Peterson set up a simple global array as a flag
![[Pasted image 20250919140415.png]]
Bundle Flag and Turn together Same flip flop and blocking as Dekker's
### Exhaustive case
P1 has no interest in critical section,
P1 is waiting for critical section
P1 is using its critical section repeatedly and therefore monopolizing access to it

# Race Conditions
## Difficulties of Concurrency
1. Sharing glboal Resources
2. Difficult for OS to manage the allocation of resources optimally
3. Difficult to locato programming erros as results are not deterministic and reproducible
## Race condition
Occurs when multiple process or threads read and write data items.
The **loser** is the <u>one who updates last</u> will determine the final value of the variable
##  Process Interaction
![[Pasted image 20250919141426.png]]

# Illustration of Mutual Exclusion
Mutual Exclusion is used when there is competition for the same resource
> I/O Device, Memory, Processor time, clock

### 3 control problems 
1. The need for mutual exclusion
2. Deadlock
3. Starvation
![[Pasted image 20250919141724.png]]
Have a function (arbiter) to handle critical resources

## Cooperation
**Sharing** process aren't **explicitly** aware of other processes using the same data

**Communication** all process are communicating to each other to synchronize or coordinate the cooperation
# Requirements of Mutual Exclusion
1. Mutual Exclusion must be enforced: only one process at a time is allowed into its critical section
2. A process that halts must do so without interfering with other processes
3. It must not be possible for a process requiring access to critical section to be delayed indefinitely: no deadlock or starvation
4. When no process is in a critical section, any process requesting entry must be permitted without delay.
5. No assumptions are made about relative process speeds or number of processes. 
6. A process remains inside its critical section for a finite time only
# Hardware Approaches to support mutual exclusions


1. Interrupt Disabling
	1. A process will continute to run until it invokes an OS services or until it is interrupted
	Disadvantages
		The efficiency of execution could be noticeable degraded becasue the process is limited in its ability to interleave processes
		This won't work for a multiprocessor architecture
	
2. Comapre & Swap Instruction
	1. In this case, there is not a master/slave relationship; rather the processor behave independently in a peer relationship
	2. A compare ism ade ebetween a memory value and a test value
		1. if the values are the same, a swap occurs between teh (old) memory value and a new wvalue
		2. Otherwise if they are **not** the same we don't change the old memory value
		3. Carried out atomically
3. Exchange Instruction
	1. Similar concept to compare & swap
	2. The instruction exchanges the contents of a register with that of a memory location

![[Pasted image 20250919143906.png]]
## Special Machine Instructions
### Advantages
- Applicable to any number of processes on neither a single proessor or multiple processors sharing main memory
- simple and easy to verify
- Can be used to support critical seections; each critical section can be define by its own variable
### Disadvantages
- Busy-waiting is employed
	- While a process is waiting for access it continues to consume processor time
- Starvation is possible
- Deadlock is possible
# Semaphore
![[Pasted image 20250919144144.png]]
A Semaphore is a integer used for signaling processes
that can only be 
- Incremented
	- semSignal
- Decremented
	- semWait
- Initialized
	- Non-negative
There is no way to inspect or manipulate a semaphore other than these 3 operations
![[Pasted image 20250919144605.png]]

Semaphore are used to *count processes slots*
-ve block process
+ve place it in queue


## Strong and Weak Semaphores
### Strong Semaphore
A semaphore whose defiinition includes the poliy that the process that hsa been blocked the longest is released from the queue first (FIFO)
### Weak Semaphore
A semaphore whose definition does not specify the order in which process are removed from the queue
![[Pasted image 20250919145134.png]]
## Mutual Exclusions Using Semaphores
![[Pasted image 20250919145315.png]]
![[Pasted image 20250919145328.png]]
## Producer/Consumers Problem
Consumer (Takes out data from buffer)
Producer (Putting data into buffer)
Only 1 producer or consumer may access the buffer at one time

Ensure the producer won't try to add data into the buffer if it's full and the consumer won't try to remove data from an empty buffer
### Using Binary Semaphore to solve
#### Incorrect
![[Pasted image 20250919145511.png]]
Use 2 binary semaphore represent buffer state & lock.
#### Correct
![[Pasted image 20250919145737.png]]
#### Correct using regular sempahores
![[Pasted image 20250919145737.png]]


Two Implementation of Semaphores
![[Pasted image 20250919145954.png]]
# Monitors
![[Pasted image 20250919150128.png]]
Programming language construct that provides equivalent functionality to that of semaphores and is easier to control

## Characteristics
- Local data variables are accessible only by the monitor's procedures and not by any external procedures
- Process enters monitor by invoking one of its procedures
- Only one process may be executing in the monitor at a time.
## Synchronization
A monitor <u>supports</u> by th e use of **condition vairables**

These are contained in the monitor and only accessible within the monitor

They have two functions
cwait(c): suspend execution of calling process on condition c
csignal(c): resume execution of some process blocked after a cwait on the same condition

Monitor wait and signal operations are different from those from the semaphore. If a process in a monitor signals and no tasks is waiting on the condition variable, the signal is lost.
![[Pasted image 20250919150338.png]]
# Message Passing
When <u>process interact</u> with one another two funamental <u>requirements</u> must be satisfied
1. Synchronization
	- To enforce mutual exclusion
2. Communication
	- To exchange information

One approach to providing both of these functions is

**Message passing**
The actual function is normally provided in the form of a pair of primitives

send(destination, message)
receive(source, message)

![[Pasted image 20250919150553.png]]


Communication of a message between two process implies synchronization between the two
	The receive cannot receive a message until it has been sent by another process


When Send is executed there is 2 possibilities
1. Sending is blocked until Message is received
2. or not

When a receive is executed there is two possibilities
- If a message has been sent, the message is received and execution continues
- If no messages are have been sent it will either be blocked, **or** continue to execute and abandon the attempt to receive

## Blocking Send, Blockign Receive
- Both sender and receiver are blocked until the message is delivered
- Sometimes referred to as rendezvous
- Allows for tight synchronization between process
## Nonblocking Send, Blocking Receive
- Sender continues on but receiver is blocked until the requested message arrives
- Most useful combination
- Sends one or more messages toa variety of destinations as quickly as possible
## Nonblocking Send, Nonblocking Recieve
- neither party is required to rwait
# Addressing
## Direct
- Send includes a specific identifier of the destination
- Receive can be handles one of two ways
	1. Require that the process explicitly designate a sending process
		- Effective for cooperating concurrent processes
	2. Implicit Addressing
		- Source parameter of the receive primitive possess a value returned when the receive operation has been performed
## Indirect
- Messages are sent to a shared data structure consisting of queues that can temporarily hold messages
	- Queues are referred to as mailboxes
- One process sends a message to the mailbox and the other picks it up from the mailbox
	- Allows for greater flexibility in the use of messages

### Indirect Addressing Relation Ship
![[Pasted image 20250919151358.png]]
#### One-to-One
- Insulates their interaction from erroneous interference from other processes
#### Many-to-One
- client/server interactions 
- mailbox is known as a port
#### One-to-Many
Useful for applications where a message or some information is meant to be a broadcast to a set of processes
#### Many-to-Many
- multiple server processes to provide concurrent service to multiple clients
## Queueing Discipline
The simplest queuing discipline is FIFO
	May not be sufficient for message with varying priority

Other Alternatives
	Priority based, or Destination
	To allow the receiver to inspect the message queue and select which to receive