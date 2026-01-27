# Types of Processor Scheduling
**Long-term Scheduling** The Decision to add to the pool of processes to be executed
**Medium-term Scheduling** - The decision to add to the number of processes that are partially of fully in main memory 
**I/O Scheduling** - The decision as to which process's pending I/O request shall be handled by an available I/O Device.

# Processor Scheduling
Aim is to assign processes to be executed by the processor in a way that meets system objectives, such as response time, throughput, and processor efficiency.
Broken down into three separate functions:
- Long term scheduling 
- Medium term scheduling
- Short term scheduling
![[Pasted image 20251031132714.png]]
![[Pasted image 20251031132724.png]]
![[Pasted image 20251031132731.png]]
# Scheduling Algorithms
## Long-term Scheduling
Determines which programs are admitted to the system for processing

Controls the degree of multiprogramming
- The more processes that are created, the smaller the percentage of time that each process can be executed
- May limit to provide satisfactory service to the current set of processes
Creates processes from the queue when it can, but must decide:
- When the operating system can take on one or more additional processes
- Which jobs to accept and turn into processes
	- First Come, first served
	- Priority, expected execution time, I/O requirements
## Medium-term Scheduling
Part of the swapping function

Swapping-in decision are based on the need to manage the degree of multiprogramming
- Considers the memory requirements of the swapped-out processes
## Short-term Scheduling
Known as the **dispatcher**
Executes most frequently
Makes the fine-grained decision of which process to execute next
Invoked when an event occurs that may lead to the blocking of the current process or that may provide an opportunity to pre-empt a currently running process in favour of another

Examples:
- Clock interrupts
- I/O interrupts
- Operating System Calls
- Signals (eg. semaphores)
### Short-Term Scheduling Criteria
Main Objective is to allocate processor time to optimize certain aspects of system behavior
A set of criteria is needed to evaluate the scheduling policy
#### User-oriented Criteria
- Relate to the behavior of the system as perceived by the individual user or process (such as response time in an interactive system)
- Important on virtually all systems
#### System-oriented Criteria
- Focus is on effective and efficient utilization of processor (rate at which processes are completed)
- Generally of minor importance on single-user systems.
### Short-Term Scheduling Criteria: Performance:
Another dimension along which criteria can be classified is those that are performance related and those that are not directly performance related.
Criteria can be classified into:
#### Performance-related
- Quantitative
- Easily measured
Examples: Response time and throughput
#### Non-performance related
- Qualitative
- Hard to measure
Examples: Predictability
# Scheduling Criteria
## User Oriented, Performance Related
### Turnaround time
This is the interval of time between the submission of a process and its completion. Includes actual execution time plus time spent waiting for resources, including the processors. This is an appropriate measure for a batch job.
### Response Time
For an interactive process, this is the time from the submission of request until the response begins to be received. Often a process can begin producing some output to the user while continuing to process the request. Thus, this is a better measure than turnaround time from the user's point of view. The scheduling discipline should attempt to achieve low response time and to maximize the number of interactive users receiving acceptable response time.
### Deadlines
When a process completion deadlines can be specified, the scheduling discipline should subordinate other goals to that maximizing the percentage of deadlines met.
## User Oriented, Other
### Predictability
A given job should run in about the same amount of time and at about the same cost regardless of the load on the system. A wide variation in response time or turnaround time is distracting to users. It may signal a wide swing in system workloads or the need for system tuning to cure instabilities.
## System Oriented, Performance Related
### Throughput
The scheduling policy should attempt to maximize the number of processes completed per unit of time. This is a measure of how much work is being performed. This clearly depends on the average length of a process, but is also influenced by the scheduling policy, which may affect utilization
### Processor Utilization
This is the percentage of time that the processor is busy. For an expensive shared system, this is a significant criterion. In single-user systems and in some other systems, such as real-time systems, this criterion is less important than some of the others.
## System Oriented, Other
### Fairness
In the absence of guidance from the user or other system-supplied guidance, processes should be treated the same, and no process should suffer starvation
### Enforcing priorities
When process are assigned priorities, the scheduling policy should favour higher--priority processes
### Balancing Resources
The scheduling policy should keep the resources of the system busy. Processes that will underutilize stressed resources should be favoured. This criterion also involves medium-term and long-term scheduling.

![[Pasted image 20251031134413.png]]
## Characteristics of Various Scheduling Policies
![[Pasted image 20251031134446.png]]
## Selection Function
Determines which process, among ready processes, is selected next for execution
May be based on priority, resource requirements, or the execution characteristics of the process
If based on execution characteristics, then important quantities are:
- $w$ = time spent in system so far, waiting
- $e$ = time spent in execution so far
- $s$ = total service time required by the process, including e; generally, this quantity must be estimated or supplied by the user
## Decision Mode
Specifies the instants in time at which the selection function is exercised
### Non-pre-emptive
Once  a process is in the running state, it will continue until it terminates or blocks itself for I/O
### Pre-emptive
Currently running process may be interrupted and moved to ready state by the OS
Decision to pre-empt may be performed when a new process arrives when an interrupt occurs that places a blocked process in the Ready state, or periodically, based on a clock interrupt.
#### Example
![[Pasted image 20251031134857.png]]
Arrival Time = When it arrives to the CPU
Service time = How long it takes
![[Pasted image 20251031134906.png]]

![[Pasted image 20251031135042.png]]
## FCFS (Non Premptive)

| Process | Arrival | Service | Start | End | Turnaround (End - Arrival) | $\frac{\text{Turn}}{\text{Serv}}$ | Wait (Turnaround - Service) | Response (Start - Arrival) |
| ------- | ------- | ------- | ----- | --- | -------------------------- | --------------------------------- | --------------------------- | -------------------------- |
| A       | 0       | 3       | 0     | 3   | 3                          | 1.00                              | 0                           | 0                          |
| B       | 2       | 6       | 3     | 9   | 7                          | 1.17                              | 1                           | 1                          |
| C       | 4       | 4       | 9     | 13  | 9                          | 2.25                              | 5                           | 5                          |
| D       | 6       | 5       | 13    | 18  | 12                         | 2.40                              | 7                           | 7                          |
| E       | 8       | 2       | 18    | 20  | 12                         | 6.00                              | 10                          | 10                         |

## Shortest Process Next (SPN) (Non-Premptive)

| Process | Arrival | Service | Start | End | Turnaround | $\frac{\text{Turn}}{\text{Serv}}$ | Wait | Response |
| ------- | ------- | ------- | ----- | --- | ---------- | --------------------------------- | ---- | -------- |
| A       | 0       | 3       | 0     | 3   | 3          | 1.00                              | 0    | 0        |
| B       | 2       | 6       | 3     | 9   | 7          | 1.17                              | 1    | 1        |
| E       | 8       | 2       | 9     | 11  | 3          | 1.50                              | 1    | 1        |
| C       | 4       | 4       | 11    | 15  | 11         | 2.75                              | 7    | 7        |
| D       | 6       | 5       | 15    | 20  | 14         | 2.80                              | 9    | 9        |

|---A---|------B------|--E--|----C----|-----D-----|
0       3             9    11        15          20
## Shortest Remaining Time (SRT) (Premptive)

| Process | Arrival | Service | Start | End | Turnaround | $\frac{\text{Turn}}{\text{Serv}}$ | Wait | Response |
|---------|---------|---------|-------|-----|------------|----------------------------------|------|----------|
| A       | 0       | 3       | 0     | 3   | 3          | 1.00                             | 0    | 0        |
| B       | 2       | 6       | 3     | 15  | 13         | 2.17                             | 7    | 1        |
| C       | 4       | 4       | 4     | 8   | 4          | 1.00                             | 0    | 0        |
| D       | 6       | 5       | 15    | 20  | 14         | 2.80                             | 9    | 9        |
| E       | 8       | 2       | 8     | 10  | 2          | 1.00                             | 0    | 0        |

|---A---|B|------C------|--E--|-----B-----|-----D-----|
0       3 4            8    10          15          20
## Highest Response Ratio Next (HRRN)

| Process | Arrival | Service | Start | End | Turnaround | $\frac{\text{Turn}}{\text{Serv}}$ | Wait | Response |
| ------- | ------- | ------- | ----- | --- | ---------- | --------------------------------- | ---- | -------- |
| A       | 0       | 3       | 0     | 3   | 3          | 1.00                              | 0    | 0        |
| B       | 2       | 6       | 3     | 9   | 7          | 1.17                              | 1    | 1        |
| C       | 4       | 4       | 9     | 13  | 9          | 2.25                              | 5    | 5        |
| E       | 8       | 2       | 13    | 15  | 7          | 3.50                              | 5    | 5        |
| D       | 6       | 5       | 15    | 20  | 14         | 2.80                              | 9    | 9        |

|---A---|------B------|----C----|--E--|-----D-----|
0       3             9        13    15          20

## Round Robin
#### Formulas
- **Start** = max(previous End, Arrival)
- **End** = Start + Service
- **Turnaround** = End − Arrival
- **Wait** = Turnaround - Service
- **Response** = Start - Arrival
- **Turn/Serv** = Turnaround ÷ Service

## First-Come-First-Served (FCFS)
Simplest scheduling policy
Also known as first-in-first-out (FIFO) or a strict queuing scheme

As each process becomes ready, it joins the ready queue

When the currently running process ceases to execute, the process that has been in the ready queue the longest is selected for running.

Performs much better for long processes than short ones
Tends to favour processor-bound process over I/O-bound processes
## Round Robin
Uses preemption based on a clock
Also known as time slicing because each process is given a slice of time before being preempted
Principal design issue is the length of the time quantum, or slice, to be used
Particularly effective in a general-purpose timesharing system or transaction processing system
One drawback is its relative treatment of processor-bound and I/O-bound processes

![[Pasted image 20251031135422.png]]
![[Pasted image 20251031135440.png]]
## Shortest Processes Next (SPN)
Non-pre-emptive policy in which the process with the shortest expected processing time is selected next
A short process will jump to the head of the queue
Possibility of starvation for longer processes
One difficulty is the need to know, or at least estimate, the required processing time of each process
If the programmer's estimate is substantially under the actual running time, the system may abort the job
## Shortest Remaining Time (SRT)
Pre-emptive version of SPN
Scheduler always chooses the process that has the shortest expected remaining processing time
Risk of starvation of longer processes
Should give superior turnaround time performance to SPN because a short job is given immediate preference to a running longer job
## Highest Response Ratio Next (HRRN)
Chooses next process with the greatest ratio
Attractive because it accounts for the age of the process
While shorter jobs are favored, aging without service increases the ratio so that a longer process will eventually get past competing shorter jobs.
$\text{Ratio}=\frac{\text{TimeSpentWaiting}+\text{ExpectedServiceTime}}{\text{ExpectedServiceTime}}$
### Performance Comparison
Any scheduling discipline that chooses the next item to be served independent of service time obeys the relationship
$\frac{T_{t}}{T_{s}}=\frac{1}{1-p}$
Where
$T_{t}$ turnaround time or residence time; total time in system, waiting plus execution
$T_{s}$ Average service time; average time spent in Running state
$p$ Processor Utilization
## Feedback Scheduling
this approach is known as **multilevel feedback**, meaning the OS allocates the processor to a process and , when the process blocks or is preempted, feeds it back into one of several priority queues.
![[Pasted image 20251031140553.png]]
## Fair-Share Scheduling
Scheduling Decisions based on the process sets
Each user is assigned a share of the processor
Objective is to monitor usage to give fewer resources to users who have had more than their fair share and more to those who have had less than their fair share
#### Example of a Fair Share Scheduler-Three Processes and Two Groups
![[Pasted image 20251031140553.png]]
## Traditional UNIX Scheduling
- Used in both SVR3 and 4.3 BSD UNIX
	- these systems are primarily targeted at the time-sharing interactive environment
- Designed to provide good response time for interactive users while ensuring that low-priority background jobs do not starve
- Employs multilevel feedback using round robin within each of the priority queues
### Example of Traditional UNIX Process Scheduling
![[Pasted image 20251031140908.png]]
## Band
Used to optimize access to block devices and to allow the 
- Makes use of one-second preemption
- priority is based on process type and execution history
In decreasing order of priority, the bands are:
- Swapper
- Block I/O device control
- File Manipulation
- Character I/O device control
- User process
