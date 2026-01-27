# COMP 7035 Operating Systems Final Study Guide 2025

The exam will cover the following questions, topics and problems:
# Scheduling
- [x] 1. Define I/O scheduling  
- [x] 2. Define and discuss processor scheduling  
- [x] 3. Define and discuss long-term, medium-term and short-term scheduling  
- [x] 4. Understand which scheduling type (short, medium or long) corresponds to which process state transitions  
- [x] 5. Define different scheduling criteria  
- [x] 6. Discuss the different criteria dimensions (e.g. user-oriented vs. system-oriented criteria or performance-related vs. non-performance-related) and provide examples  
- [x] 7. Compare and contrast scheduling algorithms across decision mode, selection function, throughput, response time, overhead, effect on processes, and starvation possibility  
- [x] 8. Define and discuss scheduling algorithms: FCFS, Round Robin, SPN, SRT, HRRN, and Feedback (advantages/disadvantages)  
- [ ] 9. Given process arrival and service times, and a scheduling algorithm:  
  - [ ] Draw a diagram showing process schedule (order & duration)  
  - [x] Calculate start, finish, turnaround, wait, and response times; normalized turnaround time and average wait time  
- [x] 10. Discuss static and dynamic priorities  
- [x] 11. Explain preemptive vs. non-preemptive scheduling  
- [x] 12. Discuss feedback scheduling with a diagram  
- [x] 13. Explain fair-share scheduling  
- [x] 14. Identify scheduling algorithm used in traditional UNIX Scheduling and its benefits  
- [x] 15. Know what bands are used for and their priority order  
# Management & Disk Scheduling
- [x] 16. Summarize the three key categories of I/O devices  
- [x] 17. Give and explain two examples of key differences between I/O devices  
- [x] 18. Explain the three techniques for performing I/O  
- [x] 19. Explain why efficiency and generality are important in I/O facility design  
- [x] 20. Define buffering and what it avoids  
- [x] 21. Compare block-oriented vs. stream-oriented devices (examples)  
- [x] 22. Explain how I/O device, OS, and user process interact under: no buffer, single buffer, double buffer, circular buffer  
- [x] 23. Discuss advantages and disadvantages of a single buffer  
- [x] 24. Define seek, settling, access, and transfer time, and rotational delay  
- [x] 25. Define and discuss disk scheduling algorithms: FIFO, PRI, SSTF, SCAN, C-SCAN, N-Step-SCAN, FSCAN (advantages/disadvantages)  
	- [ ] 26. Disk scheduling exercise (given 200-track drive, requests list, head start position): compute tracks traversed and average seek time for FIFO, SSTF, SCAN, and C-SCAN  
- [x] 27. Explain RAID concept and describe levels with advantages/disadvantages  
- [x] 28. Define cache memory and disk cache; explain I/O request handling  
- [x] 29. Explain LRU and LFU algorithms for cache blocks  
- [x] 30. Describe UNIX buffer cache, how data transfer occurs, and the three maintained lists  
## File Systems
- [x] 31. Describe desirable properties of files  
- [x] 32. Define file systems and list typical operations  
- [x] 33. Compare and contrast field, record, file, and database  
- [x] 34. List four objectives and four user requirements of file management systems  
- [x] 35. Describe elements of the File System Software Architecture  
- [x] 36. Identify criteria for choosing a file organization  
- [x] 37. Define and discuss the five common file organizations (advantages/disadvantages, typical usage)  
- [x] 38. Define a B-tree (or draw a B-tree node with k children), typical usage, and advantages  
- [x] 39. Compare two-level scheme vs. tree-structured directory  
- [x] 40. Define pathname and state the two ways to assign them  
- [x] 41. Explain the relationship between pathname and working directory  
- [x] 42. List and explain three typical file access rights  
- [x] 43. Explain record blocking (fixed-length, variable-length spanned/unspanned)  
- [x] 44. Explain file allocation and define the File Allocation Table (FAT)  
- [x] 45. Define preallocation and dynamic allocation policies  
- [x] 46. Discuss portion size trade-offs and variable portions vs. blocks  
- [x] 47. Compare contiguous, chained, and indexed (block vs. variable) file allocation methods  
- [x] 48. Describe bit tables, chained free portions, indexing, and free block lists (advantages/disadvantages)  
- [x] 49. Define an inode in UNIX and explain file allocation in UNIX  
## Virtualization
- [x] 50. Explain virtualization  
- [x] 51. List and explain three key reasons for using virtualization  
- [x] 52. Define virtual machine, hypervisor, and paravirtualization  
- [x] 53. Explain hypervisor functions  
- [x] 54. Describe Type 1 and Type 2 virtualization  
- [x] 55. Define container virtualization and list two noteworthy characteristics  
- [x] 56. Explain Docker and its principal components  
- [x] 57. Identify two main strategies for providing processor resources  
- [x] 58. Explain ring 0 and its relevance to hypervisors  
- [x] 59. Explain page sharing, ballooning, and memory overcommit in virtual machines  
- [x] 60. Explain advantages of virtualizing workload’s I/O path and trade-offs  
- [x] 61. State the goal of the Java VM  

### Cloud Section

- [x] 62. Define cloud computing  
- [x] 63. List and describe three essential characteristics of cloud computing  
- [x] 64. List and define the three cloud service models  
- [x] 65. List and define the four cloud deployment models  
- [x] 66. List and define five major actors (roles & responsibilities)  
- [x] 67. Define the cloud operating system  
	- [x] 68. List and define key components of a cloud OS: virtual computing, virtual storage, virtual network, data structure management, and management/orchestration  
- [x] 69. Define the Internet of Things (IoT)  
- [x] 70. List and define principal components of an IoT-enabled device  
- [x] 71. Define constrained device and compare the three classes  
- [x] 72. List requirements for an IoT OS  