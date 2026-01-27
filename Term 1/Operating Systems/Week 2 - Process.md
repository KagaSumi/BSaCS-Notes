# Process
Two elements that are **essential** to a process are 
1. Program Code
	1. Which may be shared with other processes that are executing the same program
2. A set of data associated with that code
	When the processor begins to execute the program code, we refer to this executing entity as a process

While a process is executing the following characteristics can be used to identify it
- Identifier
- State
- Priority
- Program Counter
- Memory Pointers
- Context Data
- I/O Status information
- Accounting Information
![[Pasted image 20250912133936.png]]o
### Process States
#### Trace
The behavior of an individual process by listing the sequence of instructions that execute for that process

The behavior of the processor can be characterized by showing how the tracs of the various processes are interleaved
#### Dispatcher
Small program that switches the processor from one process to another
![[Pasted image 20250912133753.png]]
#### Example
![[Pasted image 20250912133900.png]]
>Let us view these traces from the processor's point of view.
The figure on the next slide shows the interleaved traces resulting from the first 52 instruction cycles (for convenience, the instruction cycles are numbered).
The shaded areas represent code executed by the dispatcher.
The same sequence of instructions is executed by the dispatcher in each[]() instance because the same functionality of the dispatcher is being executed.
We assume that the OS only allows a process to continue execution for a maximum of six instruction cycles, after which it is interrupted; this prevents any single process from monopolizing processor time.
# Process States
## Two-State Process Model
In this model, a process may be in one of two states: **Running** or **Not Running**
![[Pasted image 20250912134221.png]]
### Reasons for process creation
- New Batch Job
	The OS is provided with a batch job control stream, usually on tape or disk. When the OS is prepared to take on new work, it will read the next sequence of job control commands.
- Interactive Log-on
	A user at a terminal logos on to the system
- Created by OS to provide a service 
	The OS can create a process to perform a function on behalf of a user program without the user having to wait (e.g. Process for printing)
- Spawned by existing process
	For purpose of modularity or to to exploit parallelism, a user program can dictate the creation of a number of processes.
### Process Creation
Process Spawning
	When the OS creates a process as the explicit request of another process
Parent Process
	 Is the Original, creating process
Child Process
	Is the new process

## Process Termination
There must be a means for a process to indicate its completion
A batch job should include a **HALT** instruction or an explicit OS service call for termination

For an interactive application, the action of the user will indicate when the process is completed 
#### Process Termination Reasons
- Normal Completion
	The process executes a OS service call to indicate it is finished
- Time Limit Exceeded
	The process has run longer than the **specified** total time limit
		Time is measured in the following:
			- Time spent executing 
			- Time Elapsed
			- Time spent inactive
			- Time since user input
- Memory Unavailable
	Process is unable to get more memory
- Bounds Violation
	The process attempts to access a memory location that it isn't allowed
- Protection Error
	The process attempts to use a resource it doesn't have permissions or in a improper fashion (writing on read only)
- Arithmetic Error
	The process tries a prohibited computation (divide by zero) or attempts to store a number larger than datatype
- Time overrun
	Time limit exceed waiting for an **event**
- I/O Failure
	An error occurred during Input or Output, 
	Example
		File not found
		Failure to read
		Failure to Write
		Invalid Operation
- Invalid instruction
	The process attempts to execute a nonexistent instruction
- Privileged Instruction
	The process attempts to use an instruction reserved for the **operating system**
- Data Misuse
	A piece of data is the wrong type or uninitialized
- Operator or OS intervention
	For some reason the operator or the operating system has terminated the process
		Used for Deadlocks
- Parent termination
	When the parent process is terminated, it will terminate all the children
- Parent Request
	A parent process is able to terminate its offspring
## Five-State Model
![[Pasted image 20250912135857.png]]
A more natural way to handle this situation is to split the Not Running state into two states: **Ready** and **Blocked**

If more all processes were ready to execute, then queuing is employed
![[Pasted image 20250912140413.png]]
Queue is FIFO, and the processor operates in round-robin fashion on the available process

However with simple example described this implementation is inadequate, some process are not running when they are ready to execute. While others are blocked waiting on I/O to complete

Meaning using a single queue, the dispatcher could not just select the process at the oldest end of the queue

### Reasons for Process Suspension
- Swapping
	The OS needs to release sufficient main memory to bring in a process that is ready to execute
- Other OS Reason
	The OS may suspend a background or utility process or o a process that is suspected of causing a problem
- Interactive User request
	A user may wish to suspend execution of a program for debugging 
- Timing
	A process may be executed periodically and may be suspending while waiting for the next time interval
- Parent Process Request
	A parent process may wish to suspend execution of a descendant to examine or modify the suspended process or to coordinate activity of various descendants
## Suspending Process
**Swapping**
Involves moving all of a process from main memory to disk
When none of the process in main memory is in the Ready State the OS swaps one of the blocked process out on to disk into a **suspend queue**
	This is a queue of existing process that have been temporarily kicked out of main memory, or suspend queue or it honors a new-process request

*Note* Swapping is I/O task, there for it can be make the problem worse due to disk I/O is dependant on disk speed
![[Pasted image 20250912141745.png]]
#### Characteristics of a suspended Processes
- Not immediately available for execution
- The process was placed in a suspended state by an agent
- process may or may not be waiting on an event
- The process may not be removed from this state until the agent explicitly orders the removal
# Process Description
![[Pasted image 20250912141957.png]]
![[Pasted image 20250912142011.png]] 
## Memory Tables
Memory Tables are used to keep track of both **main** (real) and **secondary** (virtual) memory

Process are maintained on secondary memory using some sort of virtual memory or simple swapping mechanism
![[Pasted image 20250912142258.png]]
## I/O Tables
Used by the OS to manage the I/O devices and channels of the computer system

At any given time, an I/O device may be available or assigned to a particular process
If an I/O operation is in progress, the OS needs to know
	The **status** of the I/O operation
	The **location** in main memory being used as the source or destination of I/O transfer
## File Tables
The file table provide information abou
	1. Existence of files
	2. Location of secondary memory
	3. Current Status
	4. Other attributes
Information may be maintained and used by a file management system
	In which case the OS has little or no knowledge of files
In other operating systems, much of the detail of file management is managed by the OS itself
## Process Tables
Must be maintained to manage processes
There must be some reference to memory, I/O, and files, directly or indirectly
The tables themselves must be accessible by the OS and therefore are subject to memory management

## Process Control Structures
To manage and control a process the OS must know **two** things
### Process Location
- Must include a program or set of programs to be executed
- Consist of **least sufficient memory** to hold the programs and data of that process
- The execution of program typically involves a stack that is used to track procedure calls and parameter passing between procedures
### Process Attributes
- Process has an associated with it a number of attributes that are used by OS for process control
- Collection of program, data, stack, and attributes is referred as the **process image**
- Process image location will depend on the memory management scheme being used
#### Elements of a Process Image
1. User Data
	1. The modifiable part of the user space
2. User Program
	1. The program to be executed
3. Stack
	1. Each process has one or more LIFO stacks associated. The stack is used to store parameters and calling address for procedure and system calls
4. Process Control Block
	1. Data needed by OS to control the process
###### Elements of a Process Control Block
1. Process Identification (using identifiers)
	1. Numeric identifiers that may be stored with the PCB
		1. Identifier of this process
		2. Identifier of Parent process
		3. User Identifier
2. Process State information
	1. User-Visible Registers (8-32)
3. Control and Status Registers
	1. Program Counter
	2. Condition Codes
	3. Status Information
4. Stack Pointers
	1. Each process has a stack this is the pointer to the **top** of the stack
5. Process Control Information
	1. Scheduling and state information that is needed by the operating system to perform its scheduling function
		- Process State
		- Priority
		- Scheduling-related information
		- Event
6. Data Structuring
	- A process may be linked to another process (queue, ring or some other structure)
	- Or Link to parent or child process
	- Point to another process that support these structures
7. Inter-process Communication
	- Various flags, signals, and messages may be associated with communication between two independent processes
	- Some or all of this information may be maintained in the process control block
8. Process Privileges
	- The granted privileges in terms of the memory that may be access and the types of instructions that may be executed
9. Memory Management
	- This section may include pointers to segment and/or page tables that describe the virtual memory assigned to the process
10. Resource Ownership and Utilization
	- Resources controlled by the process may be indicated such as opened files
	- A history of utilization of the processor or other resources may also be included

## Process Identification
Each process is assigned **UNI** (Unique Numeric Identifier)
	Otherwise there must be a mapping that allows the OS to locate appropriate tables based on the process identifier

Many of the table controlled by the OS may use process identifiers to cross-reference process tables

Memory tables may be organized to provide a map of main memory with indication of which process is assigned to each region

When processes communicate with one another, the process identifier informs the OS of the destination of a particular communication

When processes are allowed to create other process, identifiers indicated the parent and descendant of each process

## Processor State Information
Consists of the contents of processor registers
- User-visible registers
- Control and Status registers
- Stack Pointers

All processor designs includes registers/set of registers, often known as **program status word (PSW)**
	These contain condition codes plus other status information
	EFLAGS register is an example of a PSW used by any OS running on an  x86 processor
#### x86 EFLAGS Register
![[Pasted image 20250912144802.png]]
## Process Control Information
 The additional information needed by the OS to control and coordinate the various active process
 ![[Pasted image 20250912144903.png]]
![[Pasted image 20250912144913.png]]

## Role of the Process Control Block
This is the **most important data structure** of a OS
- Contain all information about a process that is needed by the OS
- Blocks are read / modified by virtually every module of the OS
- Defines the state of the OS
##### Difficulty is not access, but protection
- A bug in a single routine could damage process control blocks, which could destroy the system's ability to manage the affected processes
- A design change in the structure or semantics of the process control block could affect a number of modules in the OS
# Process Control
## Modes of Execution
### User Mode
- Less privileged mode
- User programs typically execute in this mode
### System Mode
- More-privileged mode
- Also referred to as control mode or kernel mode
- Kernel of the Operating System
## Typical Functions of A OS Kernel
1. Process Management
	- Process Creation and termination
	- Process Scheduling and dispatching
	- Process Switching
	- Process Synchronization and support for interproces communication
2. Memory Management
	- Allocation of address space to processes
	- Swapping
	- Page and segment management
3. I/O Management
	- Buffer management
	- Allocation of I/O channels and devices to processes
4. Support Functions
	- Interrupt handling
	- Accounting
	- Monitoring

## Process Creation
Once a OS decide create a new process it will
1. Assign a unique ID for the process
2. Allocate space for the process
3. Initialize the Process Control Block
4. Set the appropriate linages
5. Create or expand other data structures
## Mechanism for Interrupting the Execution of a Process
### Interrupt
Cause : External to the execution of the current instruction
Use: Reaction to an asynchronous external event
### Trap
Cause: Associated with the execution of the current instruction
Use: Handling of an error or an exception condition
### Supervisor Call
Cause: Explicit request
Use: Call to an OS function

## System Interrupts
1. Interrupt
	1. Clock Interrupt
		The OS determines that a process has been running for too long
			**Time slice**
	2. I/O Interrupt
	The OS determines that I/O action has occurred. If I/O action constitutes an event where one or more process are waiting for. The OS will move all corresponding block process to the Ready state. 
	The OS must then decide whether to resume execution of the process currently in the Running State or to pre-empt that process for a higher-priority Ready process
	3. Memory Fault (Need to wait for I/O)
		The processor Encounters a virtual memory address reference for a work that isn't in main memory. The OS must bring the block of memory containing the reference from secondary memory to main memory. 
2. Trap
	An error or exception condition generated within the currently running process
	OS determine if the conditional is fatal
	 - Moved to the Exit state and a process switch occurs
	 - Action will depend on the nature of the error and the design of the OS
## Mode Switching
### No Interrupt Pending
	Proceeds to fetch stage and fetches the next instruction of the current program in the current process
### Interrupt Pending
	Sets the PC to the starting address of the interrupt handler program
	Switches from user mode to kernel mode so that the interrupt proces code may include privileged instructions
## Changing a Process State
1. Save the context of the processor
2. Update the PCB of the process currently in the Running State
3. Move the PCB of the process to the appropriate queue
4. Select another process for Execution
5. Update the PCB of the process Selected
6. Update Memory Management Data structures 
7. Restore the context of the processor to that which existed at the time the select process was last switched out
# Execution of the Operating System
Read 3.5 of the book CINEMA

# UNIX SVR 4 Process Management
Uses the model where most of the OS executes within the environment of a user process
System Process run in kernel mode
	House keeping function or OS code
User Processes
 - Operate in user mode to execute user programs and utilities
 - Operate in kernel mode to execute instructions that belong to the kernel
 - Enter kernel mode by issuing a system call, when a exception is generated or when an interrupt occurs
## UNIX Process States
- User Running
	-  Executing in user mode
- Kernel Running
	- Executing in kernel mode
- Ready to Run in Memory
	- Ready to run as soon as kernel schedules it
- Asleep in Memory
	- Unable to execute until an event occurs; process is in main meomry ( ablocked state)
- Ready to Run, Swapped
	- Process is ready to run but the swapper must swap teh process into main meomryt memory before kernel can schedule
- Sleeping, Swapped
	- The process is awaiting an event and has been swapped to secondary storage
- Preempted
	- Process is returning from kernel to user mode, but kernel preempts it and does a process switch to schedule anotehr process
- Created
	- Process is newly created and not yet ready to run
- Zombie
	- Process no longer exists, but it left a reord for a parent process to collect

# Process Control
Process creation is means of the kernel system call, `fork()`
When a process issues a fork() request, the OS perform the following:

1. Allocates a slot in the process table for the new process
2. Assigns a unique process ID to the child process
3. Makes a copy of the process image of the parent, with the exception of any shared memory
4. Increments counters for any files owned by the parent, to reflect that an additional process now also owns those files
5. Assigns the child process to the Ready to Run state
6. Returns the ID number of the child to the parent process, and a 0 value to the child process


After creating the process the Kernel can do one of the following, as part  
of the dispatcher routine:  
• Stay in the parent process. Control returns to user mode at the point  
of the fork() call of the parent.  
• Transfer control to the child process. The child process begins  
executing at the same point in the code as the parent, namely at the  
return from the fork() call.  
• Transfer control to another process. Both parent and child are left in  
the Ready to Run state

# Processes
# Processes and Threads
Two characteristics 
![[Pasted image 20250912160614.png]]
### Resource Ownership
- Process includes a virtual address space to hold the process image
- Time to time a process may be allocated control or ownership of resources (I/O, main memory, I/O devices and files)
### Scheduling/Execution
- Execution of process follows a executino path (trace) through one or more programs
- This execution may be interleaved with other proceses

A unit of dispatching is referred to as a **thread** or a lightweight process
The unit of resource ownership is reffered to as a **process or task**

**Multithreading** The ability for a OS to support multiple, concurrent paths of execution within a single process


### Single threaded approaches
A single thread of execution per process, in a which the concept of a thread is not recognized

Example MS-DOS is an OS that supports a single user process and a single thread

### Multi Threaded Approach
The right half of hte figure depicts multithreaded approaches
the JRE (Java run-time environment) is a nexample of a system of a one process with multiple threads 

## Process
Defined in a multithreaded environment as the "unit of resource allocation" and a unit of protection
- Virtual Address space that holdsd the process image
- Protected access to 
	- Processors
	- Other processes
	- Files 
	- I/o Reosurces
### One or more threads in a process
Each thread has 
- An executable state
- A saved thread context when not running
- an execution stack 
- some per-thread static storage for local variables
- Access to the' memory and resources of its process, shared with all other threads in that process
## Key Benefits of threads
- Takes less time to create a new thread than a process
- Less time to terminate a thread rather than a process
-  Switching between two threads takes less times than switching between process
- Threads enhance efficiency in communications between programs

## Thread use in a single-user system
1. Foreground and background work
	1 thread rendering, 1 back up

2. Asynchronous processing
	protect against power failure as a thread for periodic backup
	
3. Speed of execution 
	Multi-threaded for better work

4. Modular Program Structure
	programs with variety of activities maybe easier to use threads over multiple programs


### Thread Execution States
Running
Ready 
Blocked

Spawn - Thread is made (spawned)
Block - Waiting for a event
Unblock - Move to Ready Queue
Finish - Thread is finished a n ca be deallocated by 


## Thread Synchronization
All threads of a process share the same address space and resources

Any alteration of a resource by one thread **affect all other threads** int he same process
Therefore it is necessary to synchronize the activates of the various threads

# Types of Threads
### User Level Thread (ULT)
![[Pasted image 20250912160821.png]]
All thread management is done by the application 
The kernel is not aware of the existence of threads

#### Pros
- Thread Switching does not require kernel mode privileges
- Scheduling can be application specific
- ULTs can run on any OS
#### Cons
- When a ULT executes a system call, not only is that thread blocked, but all of the threads within the process are blocked as well
- In a pure ULT strategy, a multithreaded application cannot take advantage of multiprocessing
### Kernel Level Thread (KLT)
![[Pasted image 20250912161102.png]]
Thread is managed by the kernel
- There is no thread managemtn code in the application level, simply an application programming interface (API) to the kernel thread facility
- Windows is an example of this approach
#### Pros
- The kernel can simultaneously schedule multiple threads from the same process on multiple processors
- IF one thread in a process is blocked, the kernel can schedule another thread of the same process
- Kernel routines themselves can be multithreaded
#### Cons
- The transfer of control from one thread to another within the same process requires a mode switch to the kernel
## Combined Approaches
![[Pasted image 20250912161400.png]]
Thread creation is done completely ini the user space, as is the bulk of the scheudling and synchronization of threads within an application

The multiple ULT from a single application are mapped onto some (smaller or equal) number of KLT

Solaris is a good example

### Relationship between Threads and Processes
![[Pasted image 20250912161416.png]]
1:1 
## Performance Effect of Multiple Cores
![[Pasted image 20250912161511.png]]
### Applications That Benefit from Multicore
Multithreaded native Applications
	Characterized by having a small number of highly threaded processes
Multi-process Application
	Characterized by the presence of many single-threaded processes
Java Application
	All applications using Java can immediately benefit from multicore Technology
Multi-instance applications
	Multiple instances of the application in parallel
Game Engines
	

# Multicore and multithreading
# Windows process and thread management
# Solaris thread and SMP management
# Linux process and thread management
# Android process and Thread management
# Mac OS X grand central dispatcher