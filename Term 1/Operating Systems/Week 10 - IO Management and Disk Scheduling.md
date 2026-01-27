# Categories of I/O Devices
## Human Readable
- Suitable for communicating with the computer use
- Printers, Terminals, Video Display, Keyboard, Mouse
## Machine Readable
- Suitable for communicating with electronic equipment
- Disk drives, USB keys, sensors, controllers
## Communication
- Suitable for communicating with remote devices
- Modems, digital line drivers
# Differences in I/O Devices
## Data Rate
There may be differences of magnitude between the data transfer rates
## Application
	The use to which a device is put has an influence on the software
## Complexity of Control
The effect on the operating system is filtered by the complexity of the I/O module that controls the device
## Unit of Transfer
Data may be transferred as a stream of bytes or characters or in larger blocks
## Data Representation
Different data encoding schemes are used by different devices
## Error Condition
The nature of errors, the way in which they are reported, their consequences, and the available range of responses differs from one device to another.
# Typical I/O Device Data Rates
![[Pasted image 20251107133622.png]]
# Organization of the I/O Function
## Programmed I/O
The processor issues an I/O Command on behalf of a process to an I/O module; that process then busy waits for the operation to be completed before proceeding.
## Interrupt-drive I/O
The processor issues an I/O command on behalf of a process
### Non-Blocking
Process continues to execute instructions from the process that issued the I/O Command
### Blocking
The next instruction the processor executes is from the OS, which will put the current process in a blocked state and schedule another process
## Direct Memory Access (DMA)
A DMA module controls the exchange of data between main memory and an I/O module

## I/O techniques
![[Pasted image 20251107133836.png]]
# Evolution of the I/O Function
1. Process directly controls a peripheral device
2. A controller or I/O module is added
3. Same configuration as step 2, but now interrupts are employed
4. The I/O module is given direct control of memory via DMA
5. The I/O module is enhanced to become a separate processor, with a specialized instruction set tailored for I/O
6. The I/O module has a local memory of its own and is, in fact ,a computer in its own right
## Alternative DMA Configuration
![[Pasted image 20251107133955.png]]
# Design Objectives Buffering
## Efficiency
- Major effort in I/O Design
- Important because I/O operations often form a bottle neck
- Most I/O Devices are extremely slow compared with main memory and the processor
- The area that has receive the most attention is disk I/O
## Generality
- Desirable to handle all devices in a uniform manner
- Applies to the way process view I/O devices and the way the operating system manages I/O Devices and operations
- Diversity of devices makes it difficult to achieve true generality
- Use a a hierarchical, modular approach to the design of the I/O function
# Buffering
To avoid overheads and inefficiencies, it sometimes convenient to perform input transfer in advance of requests being made, and to perform output transfer some time after the request is made. This technique is known as buffering
## Block-oriented device
- Stores information in blocks that are usually of fixed size
- Transfers are made one block at a time
- Possible to reference data by its block number
- - Disks and USB keys are examples
## Stream-oriented device
- Transfer data in and out as a stream of bytes
- No block structure
- - Terminals, printers, communication ports, mouse and other pointing devices, and most other devices that are not secondary storage are examples.
## No Buffer
![[Pasted image 20251107134450.png]]
Without a buffer, the OS directly access the device when it needs
## Single Buffer
The simplest type of support that the OS can provide
When a user process issues an I/O request, the OS assigns a buffer in the system portion of the main memory to the operation
![[Pasted image 20251107134551.png]]

Input transfers are made to the system buffer
Reading ahead/ anticipated input
- Is done in the expectation that block will eventually be needed
- When the transfer is complete, the process moves the block into user space and immediately requests another block.
### Advantage
Approach generally provides a speedup compared to the lack of system buffering
- The user process can be processing one block of data while the next block is being read in
- The OS is able to swap the process out because the input operation is taking place in system memory rather than user process memory.
### Disadvantage
- Complicates the logic in the operating system
- Swapping logic is also affected
## Single Buffering for Stream-Oriented I/O
Can be used in a line-at-a-time fashion or a byte-at-a-time fashion:
### Line-at-a-time operation
Is appropriate for scroll-mode terminals (dumb terminals)
- With this form of terminal, user input is one line at a time, with a carriage return signaling the end of a line
- Output to the terminal is similarly one line at a time
### Byte-at-a-time operation
Is used on forms-mode terminals, when each keystroke is significant and for many other peripherals, such as sensors and controllers
## Double Buffer
- Assigning two system buffers to the operation
- A process now transfer data to or from one buffer while the operating system empties or fills the other buffer 
- Also known as buffer swapping
![[Pasted image 20251107135104.png]]
## Circular Buffer
- When more than two buffers are used the collection of buffers is itself referred to as a circular buffer
- Each individual buffer is one unit in the circular buffer
![[Pasted image 20251107135146.png]]
## I/O Buffer Schemes (Input)
![[Pasted image 20251107135158.png]]
# Disk Performance Parameters
The actual details of disk I/O operation depend on the :
- Computer system
- Operating system
- Nature of the I/O Channel and disk controller hardware
## Timing of a Disk I/O Transfer
![[Pasted image 20251107135327.png]]
When the disk drive is operating, the disk is rotating at a constant speed
To read or write the head must be positioned at the desired track and at the beginning of the desired sector on that track
Track selection involves either
- Moving the head in a movable-head system or
- Electronically selecting one head on a fixed-head system.
## Seek Time Disk Performance
**Seek time** - On a moveable-head system, the time it takes to position the head at the track is known as seek time.

Consists of two key components:
1. Initial Startup time
2. The time taken to traverse the tracks once the access arm is up to speed
### Settling time
Time after positioning the head over the target track until track identification is confirmed

- Much improvment comes from smaller and lighter disk components
- A typical average seek time on contemporary hard disks is under 10 ms

## Disk Performance
### Rotational Delay
- The time required for the addressed area of the disk to rotatte into position
- Disks rotate at speeds ranging from 3,600 RPM to 15,000 RPM
### Access time
The sum of seek time and rotational delay equals the access time, which is the time it takes to get into position or to read or write
### Transfer time
Once the head is in position, the read or write operation is then performed as the sector moves under the head; this is the data transfer portion of the operation
The time required for the transfer is the transfer time.
# Disk Scheduling Algorithms
![[Pasted image 20251107135837.png]]
![[Pasted image 20251107135844.png]]
![[Pasted image 20251107135857.png]]
## First-In, First-Out (FIFO)
Processes in sequential order
Fair to all processes
Approximates random scheduling in performances if many processes compete for the disk
## Priority (PRI)
- Control of scheduling is outside the control of disk management software
- Goal is not to optimize disk utilization but to meet other objectives
- Short batch jobs and interactivev jobs are given higher priority
- Provides good interactive response time
- Longer jobs may wait excessively
- A poor policy for database system
## Shortest Service Time First (SSTF)
Selects the disk I/O request requiring the least movement of the disk arm
Always chooses the minimum seek time
## SCAN
- Also known as elevator algorithm
- Arm moves in one direction only
	- Satisfies all outstanding requests until reaching the last track in that direction
	- Then, the direction is reversed
- Favors jobs requesting tracks near the innermost and outermost tracks and the latest-arriving jobs
## C-SCAN (Circular SCAN)
- Restricts scanning to one direction only
- When the last track has been visited in one direction, the arm is returned to the opposite end of the disk and the scan begins again
## N-Step-SCAN
Segments the disk request queue into the sub queues of length N
Sub queues are processed one at a time, using SCAN
While a queue is being processed new request must be added to some other queue
If fewer than N request are available at the end of a scan, all of them are processed with the next scan
## FSCAN
- Uses two subqueues
- When a scan begins, all of hte request are in one of the queues, with the other empty
- During scan, all new requests are put into the other queue
- Service of new requests is deferred until all of the old requests have been processed
# Raid
**Redundant Array of Disks**
- Consists of 7 levels, zero through 6
- Strategy employs multiple disk drives and distributes data in such a way as to enable simultaneous access to data from multiple drives
	- Imrpoves I/O performance and allows easier incremental increases in capacity
## Design architectures share 3 characteristics:

- RAID is a set of physical disk drives viewed by the operating system as a single logical drive
- Data is distributed across the physical drives of array in a scheme known as striping
- Redundant disk capacity is used to store parity information, which guarantees data recoverability in the case of a disk failure.
## Raid Levels
![[Pasted image 20251107141258.png]]
## Raid Level 0
- Not a true RAID because it does not include redundancy to improve performance or provide data protection
- User and system data are distributed across all of the disks in the array
- Logical disk is divided into strips
## Raid Level 1
- Redundancy is achieved by the simple expedient of duplicating all the data
- There is no "write penalty"
- When a drive fails the data may still be accessed from the second drive
- Principal disadvantage is the cost
## Raid Level 2
- Makes use of parallel access techniques
- Data striping is used
- Typically a Hamming code is used
- Effective choice in a environment in which many disk errors occurs
## Raid Level 3 (Raid 5)
- Requires only a single redundant disk, no matter how large the disk array
- Employs Parallel access, with data distributed in small strips
- Can achieve very high data transfer rates
## Raid Level 4
- Makes use of an independent access technique
- A bit-by-bit parity strip is calculated across corresponding strips on each data disk, and the parity bits are stored in the corresponding strip on the parity disk
- Involves a write penalty when a I/O write request of small size is performed
## Raid Level 5
Similar to RAID-4 but distributes the parity bits across all disks
typical allocation is round-robin scheme
Has the characteristic that the loss of any one disk does not result in data loss
## Raid Level 6
Two different parity calculations are carried out and stored in separate blocks on different disks
Provides extremely high data availability
Incurs a substantial write penalty because each write affects two parity blocks
# Disk Cache
## Cache Memory
Is used to apply to a memory that is smaller and faster than main memory and that is interposed between main memory and the processor
- Reduces average memory access time by exploiting the principle of locality
## Disk cache
Is a buffer in main memory for disk sectors
- Contains a copy of some of the sectors on the disk
When an I/O request is made for a particular sector, a check is made to determine if the sector is in the disk cache
- If YES: The request is satisfied via the cache
- If NO: The requested sector is read into the disk cache from the disk
## Least Recently Used (LRU)
Most commonly used algorithm that deals with the design issue of replacement strategy
The block that as been in the cache the longest with no reference to it is replaced
A stack of pointers references the cache
- Most recently referenced block is on the top of the stack
- When a block is referenced or brought into the cache, it is placed on the top of the stack
## Least Frequently Used (LFU)
The block htat has experience the fewest references is replaced
A counter is associated with each block
Counter is incremented each time a block is accessed
When a replacement is required, the block with the smallest count is selected
## Frequently-Based Replacement
![[Pasted image 20251107142445.png]]
## UNIX I/O Structure
![[Pasted image 20251107142511.png]]
# UNIX Buffer Cache
- Is essentially a disk cache
- I/O operations with disk are handled through buffer cache
## Characteristics
The data transfer between the buffer cache and the user process space always occurs using DMA
- Does not use any processor cycles
- Does not consume bus cycles
3 Lists are maintain:
### Free List
List of all slots in the cache that are available for allocation
### Device List
List of all buffers currently associated with each disk
### Driver I/O queue
List of buffers that are actually undergoing or waiting for I/O on a particular device
## Character Queue
Used by character oriented devices
- Terminals and printers
Either written by the I/O device and read by the process or vice versa
- Producer/consumer model is used
Character queues may only be read once
- As each character is read, it is effectively destroyed
## Unbuffered I/O
Is simply DMA between device and process space
Is always the fastest method for a process to perform I/O 
Process is locked in main memory and cannot be swapped out
I/O device is tied up with the process for the duration of the transfer making it unavailable for other processes

Unbuffered vs Buffered
