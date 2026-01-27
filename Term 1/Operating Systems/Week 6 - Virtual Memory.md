# Locality and Virtual Memory
## Virtual Memory Terminology
![[Pasted image 20251010133609.png]]
### Hardware and Control Structures
Two Characteristics fundamental to memory management
1. All memory references are logical addresses that are dynamically translated into physical addresses at run time
2. A process may be broken up into a number of pieces that don't need to be contiguously located in main memory during execution
If these two characteristics are present, it is not necessary that all of the pages are segments of a process be in main memory during execution
## Execution of a Process
1. Operating System brings into main memory a few pieces of the  program
	Resident Set
		Portion of process that is in main memory
2. An interrupt is generated when an address is needed that is not in main memory
		OS places the process in a blocking state
3. Piece of process that contains the logical address is brought into main memory
	- OS issues a disk I/O Read request
	- Another process is dispatched to run while the disk I/O takes place
	- An interrupt is issued when disk I/O is complete, which causes the operating system to place the affected process in the Ready state
#### Implications
- More processes may be maintained in main memory
- A process may be larger than all of main memory
#### Definitions
**Real memory** - Main memory, the actual RAM
**Virtual memory** - Memory on disk
>Allows for effective multiprogramming and relieves the user of tight constraints of main memory
# Paging
![[Pasted image 20251010134214.png]]
> Characteristics of Paging and Segmentation

**Thrashing** - A state in which the system spends most of its time swapping processes pieces rather than executing instructions

> The OS avoids this by guessing based on  history which pieces are least likely to be used in the near future
###  Principle of Locality
- Program and data references within a process tend to cluster
- Only a few pieces of a process will be needed over a short period of time 
- Therefore it is possible to make intelligent guesses about which pieces will be needed in the future
- Avoids thrashing
##### Support Needed for Virtual memory
For Virtual Memory to be **practical** and **effective**
1. Hardware must support paging and segmentation
2. Operating System must include software for managing the movement of pages and/or segments between secondary memory and main memory
## Paging
The term virtual memory is usually associated with systems that employ paging
Use of paging to achieve virtual memory was first reported for the **Atlas** computer

Each process has its own page table
	Each page table entry (PTE) contains the **frame number** of the corresponding page in main memory
	A page table is also needed for virtual memory scheme based on paging
![[Pasted image 20251010134722.png]] 
>Typical Memory Management Formats 

![[Pasted image 20251010135119.png]]
>Address Translation in a paging System
### Two-Level Paging System
![[Pasted image 20251010134854.png]]
![[Pasted image 20251010134914.png]]
> Root page table is a table that contains a Root page pointer to another table that used for another page table lookup

### Translation Lookaside Buffer (TLB)
Each Virtual memory reference can cause two physical memory access
- One to Fetch the page table entry
- One to fetch the data
To overcome the effect doubling the memory access time, most virtual memory schemes make use of a special high-speed cache called a translation lookaside buffer (TLB)
- This cache functions in the same way as a memory cache and contains those page table entities that have been most recently used
![[Pasted image 20251010135415.png]]
>"Caching Recent Pages we looked at"
>If not in Main Memory it is a Page Fault


![[Pasted image 20251010135752.png]]
## Associative Mapping
The TLB only contains some of the page tables so we can't just index into the TLB based on page number
The processor is equipped with hardware that allows it to interrogate simultaneously a number of TLB entries to determine if there is a match on page number
![[Pasted image 20251010140117.png]]
![[Pasted image 20251010140250.png]]
## Page Size
The smaller the page size, the lesser the amount of internal fragmentation

However, more pages are required for per process. More pages per process means larger page tables

For large programs in heavily multiprogram med environment some portion of the page tables of active processes must be in virtual memory instead of main memory

The physical characteristics of most secondary-memory devices favor a larger page size for more efficient block transfer of data

Contemporary programming techniques used in large programs tend to decrease the locality of references within a process.

The design issue of page size is related to the size of physical main memory and program size

Main memory is getting larger and address space used by applications is also growing

Most obvious on personal computers where applications are becoming increasingly complex
# Segmentation
Segmentation allows the programmer to view memory as consisting of multiple address spaces or segments

Pros:
- Simplifies handling of growing data structures
- Allows programs to be altered and recompiled independently
- Lends itself to sharing data among processes
- Lends itself to protection

## Segment Organization
Each segment table entry contains the starting address of the corresponding segment in main memory and the length of the segment
A bit is needed to determine if the segment is already in main memory
Another bit is needed to determine if the segment has been modified since it was loaded in main memory.

![[Pasted image 20251010140950.png]]
# Combined paging and segmentation
In a combined paging/segmentation system a user's address space is broken up into a number of segments. Each segment is broken up into a number of fixed-sized pages which are equal in length to a main memory frame
- **Segmentation** - is visible to the programmer
- **Paging** - is transparent to the programmer
![[Pasted image 20251010141114.png]]
# Protection and sharing
Segmentation lends itself to implementation of protection and sharing policies

Each entry has a base address and length so inadvertent memory access can be controlled 

Sharing can be achieved segments referencing multiple processes
![[Pasted image 20251010141235.png]]
# Fetch, Placement, and Replacement policies
The design of memory management portion of an operating system depends on three fundamental areas of choice:
1. Whether or not to use Virtual memory techniques
2. The use of paging or segmentation or both
3. The algorithms employed for various aspects of memory management
## Fetch Policy
Determines when a page should be brought into memory
### Demand Paging
Only brings pages into main memory when a references is made to a location on the page

Many page faults when process is first started

Principle of locality suggests that as more and more pages are brought in, most future references will be to pages that have recently been brought in, and page faults should drop to a very low level.
### Pre-paging
Pages other than the one demanded by a page fault are brought in

Exploits the characteristics of most secondary memory devices

If pages of a process are stored contiguously in secondary memory it is more efficient to bring in a number of pages at once time 

Ineffective if extra pages are not referenced

Should not be confused with **swapping**
## Placement Policy
Determines where in real memory a process piece is to reside
Important design issue in a segmentation system
Paging or combined paging with segmentation placing is irrelevant because hardware performs functions with equal efficiency

For **NUMA** systems an automatic placement strategy is desirable
## Replacement Policy
Deals with the selection of a page in main memory to be replaced when a new page must be brought in
	Objective is that the page that is removed by the page least likely to be referenced in the near future
	
The more elaborate the replacement policy the greater the hardware and software overhead to implement it
### Frame locking
When a frame is locked the page currently stored in that frame may not be replaced
- Kernel of the OS as well as key control structures are held in locked frames
- I/O buffers and time-critical areas may be locked into main memory frames
- Locking is achieved by associating a lock bit with each frame
### Basic Algorithms
![[Pasted image 20251010143619.png]]
#### Optimal
Is **clairvoyant** and can tell that if a page address is needed in the future or not and selects based on that.

#### Least recently used (LRU)
Replaces the page that has not been referenced for the longest time
by the principle of locality, this should be the page least likely to be referenced in the near future

Difficult to implement 
	One approach is to tag each page with the time of last reference
			This requires a great deal of overhead
#### First-in-first-out (FIFO)
Treats page frames allocated to a process as a circular buffer
pages are removed in a round-robin style
	Simple replacement policy to implement
	
Page that has been in memory the longest is replaced
#### Clock
Requires the association of an additional bit with each frame
	Referred to as the use bit

When a page is first loaded in memory or referenced, the use bit is set to 1
The set of frames is considered to be circular buffer
Any frame with a use bit of 1 is passed over by the algorithm
Page frames visualized as laid out in a circle
![[Pasted image 20251010143924.png]]
### Page Buffering
Improves paging performance and allows the use of a simpler page replacement policy

A replaced page is not lost, but rather assigned to one of two lists:
1. Free page list
	List of page frames available for reading in pages
2. Modified page list
	Pages are written out in clusters

## Replacement Policy and Cache Size
With large caches, replacement of pages can have a performance impact
	If the page frame selected for replacement is in the cache, that cache block is lost as well as the page that it holds
	In systems using page buffering, cache performance can be improved with a policy for page placement in the pagebuffering
	Most operating systems place pages by selecting an arbitrary page frame from the page buffer
## Resident Set Management
The OS must decide how many pages to bring into main memory
	The smaller the amount of memory allocated to each process, the more processes can reside in memory
	Small number of pages loaded increases page faults
	Beyond a certain size, further allocations of pages will not affect page fault rate
### Resident set size
#### Fixed-allocation
Gives a process a fixed number of frames in main memory within which to execute
	When a page fault occurs one of hte pages of that process must be replaced
#### Variable
Allows the number of page frames allocated to a process to be varied over the lifetime of the process
### Replacement Scope
The scope of a replacement strategy can be categorized of a global or local
#### Global
Considers all unlocked pages in main memory
#### Local
Chooses only among the resident pages of the process that generated the page fault 
![[Pasted image 20251017133839.png]]
### Fixed Allocation, Local Scope
Necessary to decide ahead of time the amount of allocation to give a process
If allocation is too small, there will be a high page fault rate
If allocation is too large, there will be too few programs in main memory
	This increases processor idle time and time spent swapping
### Variable Allocation Global Scope
Easiest to implement
OS maintains a list of free frames
Free frame is added to resident set of process when a page fault occurs
If no frames are available the OS must choose a page currently in memory
One way to counter potential problems is to use page buffering
### Variable Allocation Local Scope
When a new process is loaded into main memory, allocate to it a certain number of page frames as it resident set
When a page fault occurs, select the page to replace from among the resident set of the process that suffers the fault
Re-evaluate the allocation provided to the process and increase or decrease it to improve overall performance
Decision to increase or decrease a resident set size based on the assessment of the likely future demands of active processes
## Page Fault Frequency (PFF)
Requires a use bit to be associated with each page in memory
Bit is set to 1 when the page is accessed
When a page fault occurs, the OS notes the virtual time since the last page fault for the process
Does not perform well during transient periods when there is a shift to a new locality
## Cleaning Policy
Concerned with determining when a modified page should be written out to secondary memory
### Demand
A page is written out to secondary memory only when it has been selected for replacement
### Precleaning
Allows the writing of pages in batch

## Load Control
Determines hte number of processes that will be resdient in main memory
Critical in effective memory management 
Too feww processes, many occasions when all processes will be blocked 
To many will lead ot thrashing
### Degree of multiprogramming