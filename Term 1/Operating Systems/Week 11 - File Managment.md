# Files
**Files** - Data Collections created by users
The File System is one of the most important parts of the OS to a user
## Desirable properties of files
### Long-term Existence
Files are stored on disk or other secondary storage and do not disappears when a user logs off
### Sharable between processes
Files have names and can have associated access permissions that permit controlled sharing
### Structure
Files can be organized into hierarchical or more complex structures to reflect the relationships among files
## File System
File Systems - Provide a means to store data organized as files as well as a collection of functions that can be performed on files
Maintian a set of attributes associated with the file

Typical operations include:
- Create
- Delete
- Open
- Close
- Read
- Write
## File Structure
Four terms are commonly used when discussing files:
- Field
- Record
- File
- Database
### Field
- Basic element of data
- Contains a single value
- Fixed or variable length
### Record
- Collection of related fields that can be treated as a unit by some application program
- Fixed or variable length
### File
- Collection of similar records
- Treated as a single entity
- May be referenced by name
- Access control restrictions usually apply at the file level
### Database
- Collection of related data
- Relationships among elements of data are explicit
- Designed for use by a number of different applications
- Consists of one or more types of files
# File Management System
Objectives for a file management system
- Meet the data management needs of the user
- Guarantee that the data in the file are valid
- Optimize performance
- Provide I/O support for a variety of storage device types
- Minimize the potential for lost or destroyed data
- Provide a standardized set of I/O interface routines to user processes
- Provide I/O support for multiple users in the case of multiple-user systems
# Minimal User Requirements
Each user:
- Should be able to create, delete read, write and modify files
- May have controlled access to other users' files
- May control what type of accesses are allowed to the uses' files 
- Should be able to move data between files
- Should be able to move data between files
- Should be able to back up and recover files in case of damage
- Should be able to access his or her files by name rather than by numeric identifier
## File system Software Architecture
![[Pasted image 20251114134137.png]]
## Device Drivers
- Communicates directly with peripheral devices
- Responsible for starting I/O operations on device
- Processes the completion of an I/O Request
## Basic File System
- Primary interface with the environment outside the computer system
- Deals with
	- Block of data that are exchanged with disk or tape systems
	- the placement of blocks on the secondary storage device
	- buffering blocks in main memory
- Does not understand the content of the data or the structure of the files involved
## Basic I/O Supervisor
- Responsible for all file I/O initiation and termination
- At this level, control structures are maintained that deal with device I/O scheduling and files status
	- selects the device on which I/O is to be performed
	- concerned with scheduling disk and tape accesses to optimize performance
	- I/O buffers are assigned and secondary memory is allocated at this level
## Logical I/O
- Enables users and applications to access records
- provides general-purpose record I/O capability
- Maintains basic data about file
## Access Method
- Provides a standard interface between applications and the files systems and devices that hold the data
- Different access methods reflect different file structures and different ways of accessing and processing the data

# Elements of File Management
![[Pasted image 20251114134614.png]]
# File Organization and Access
File organization is the logical structuring of the records as determined by the way in which they are accessed
In choosing a file organization, several criteria are important:
- Short access time
- Ease of update
- Economy of storage
- Simple maintenance
- Reliability
Priority of criteria depends on the application that will use the file
# File Organization Types
Five of the common file organization are:
- The Pile
- The Sequential File
- The Indexed File
- The Indexed Sequential file
- The direct, or hashed, file
## The Pile
![[Pasted image 20251114134831.png]]
- Data are collected in the order they arrive
- Each record consists of one burst of data
- Purpose: to accumulate the mass of data and save it
- Record Access: is by exhaustive search
- Advantage: Least complicated form of file organization
## The Sequential File
![[Pasted image 20251114135024.png]]
- A fixed format is used for records
- key field uniquely identifies the record
- Typical usage: in batch applications
- Note:
	- Only organization that is easily stored on tape as well as disk
	- Most common form of file structure
## Indexed File Sequential File
![[Pasted image 20251114135042.png]]
- Adds an index to the file to support random access
- Adds an overflow file
- Advantages:
	- Greatly reduces the time required to access a single record
	- Multiple levels of indexing can be used to provide greater efficiency in access
## Indexed File
![[Pasted image 20251114135143.png]]
- Records are accessed only through their indexes
- Variable-length records can be employed
- **Exhaustive index** contains one entry for every record in the main file
- **Partial index** contains entries to records where the field of interest exists
- Usage: mostly in applications where timeliness of information is critical e.g. airline reservation systems and inventory control systems
## Direct or hashed File
Access directly any block of a known address
Makes use of hashing on the key value
Often used where:
- Very rapid access is required
- Fixed-length records are used
- Records are always accessed one at a time
- Examples are :
	- Directories
	- Pricing Tables
	- Schedules
	- Name lists
# B-Trees
- A balanced tree structure with all branches of equal length
- Typical usage: in OS file systems, organizing indexes for databases
- Advantage: Provides for efficient searching, adding, and deleting of items
![[Pasted image 20251114135616.png]]
## B-Tree Characteristics
It satisfies the following properties:
- Every node has at most $2d-1 \text{ keys}$ and $2d \text{ children}$ or, equivalently $2d \text{ pointers}$
- Every node, except for the root, has at least d-1 keys and d pointers, as a result, each internal node, except the root, is at least half full and has at least d children
- The root has at least 1 key and 2 children
- All leaves appear on the same level and contain no information. This is a logical construct to terminate the tree; the actual implementation may differ
- A nonleaf node with k pointers contain k-1 keys
## Inserting Nodes into a B-tree
![[Pasted image 20251114140105.png]]
# Information Elements of a File Directory
## Basic Information
**File Name** - Name as chosen by create (user or program). Must be unique within a specific directory
**File Type** - For example: text binary, load module, etc.
**File Organization** - For systems that support different organizations
## Address Information
**Volume** - Indicates device which file is stored 
**Starting Address** - Starting physical address on secondary storage(e.g., cylinder, track, and block number on disk)
**Size Used** - Current size of the file in bytes, words, or blocks
**Size allocated** - The maximum size of the file
## Access Control Information
**Owner** - User who is assigned control of this file. The owner may be able to grant/deny access to other users and to change these privileges.
**Access Information** - A simple version of this element would include the user's name and password for each authorized user.
**Permitted Actions** - Controls reading, writing executing, and transmitting over a network
## Usage Information
**Date created** - When file was first placed in directory
**Identity of Creator** - Usually but not necessarily the current owner
**Date Last Read Access** - Date of the last time a record was read
**Identity of Last Reader** - user who did the reading
**Date Last Modified** - Date of the last update, insertion, or deletion
**Identity of Last Modifier** User who did the modifying
**Date of Last Backup** Date of the last time the file was backed up on another storage medium
**Current Usage** Information about current activity on the file, such as process or processes that have the file open, whether it is locked by a process, and whether the file has been updated in main memory but not yet on disk
# Operations Performed on a Directory
To understand the requirements for a file structure, it is helpful to consider the types of operations that maybe performed on the directory:
- Search
- Create files
- Delete files
- List directory
- Update directory
# Two-Level Scheme
![[Pasted image 20251114141551.png]]
One directory for each user and a master directory
- Master directory has an entry for each user directory providing address and access control information
- Each user directory is simple list of the files of that user
- Names must be unique only within the collection of files of a single user
Advantage: File System Can easily enforce access restrictions on directories
Disadvantage: Provides users with no help in structuring collections of files

# Tree-Structured Directory
![[Pasted image 20251114141738.png]]
At any level, a directory may consist of entries for subdirectories and/or entries for files
Advantage: a more powerful, flexible, universally adopted approach
Any file in the system can be located by following a path from the root or master directory down various branches until the file is reached.
The series of directory names, culminating in the file name itself, constitutes a **pathname** for the file
e.g. User_B/Word/Unit_A/ABC
# Example of Tree-Structured Directory
![[Pasted image 20251114141933.png]]
Awkward to use entire pathname every time a reference is made to a file an interactive user or process has associated with it a current directory or **working directory**.
Files are then referenced relative to the working directory e.g. working directory is Word" then pathname is "Unit_A/ABC"
When a interactive user logs on , or when a process is created, the default for the working directory is the user home directory.
During execution, the user can navigate up or down in the tree to change to a different working directory.
# File Sharing
Two issues arise when allowing files to be shared among a number of users:
- Access Rights
- User Access Rights
## Access Rights
1. None
	- The user would not be allowed to read the user directory that includes the file
2. Knowledge
	- The user can determine that the file exists and who its owner is and can then petition the owner for additional access rights
3. Execution
	- The user can load and execute a program but cannot copy it
4. Reading
	- The user can read the file for any purpose, including copying and execution
5. Appending
	- The user can add data to the file but cannot modify or delete any of the file's contents
6. Updating
	- The user can modify, delete and add to the file's data
7. Changing Protection
	- The user can change the access rights granted to other users
8. Deletion
	- The user can delete the file from the file system
## User Access Rights
1. Owner
	- Usually the initial creator of the file
	- Has full rights
	- May grant rights to others
2. Specific Users
	- Individual users who are designated by user ID
3. User Groups
	-  A set of users who are not individually defined
4. All
	- All users who have access to this system
	- These are public files
# Record Blocking
Blocks are the unit of  I/O with secondary storage
For I/O to be performed, records must be organized as blocks
Given the size of a block, the three methods of blocking can be used:
1. Fixed-length Blocking
	Fixed-Length records are used, and integral number of records are stored in a block
	- **Internal Fragmentation**
	unused space at the end of the block
2. Variable-Length Spanned Blocking
	variable-length records are used and are packed into blocks with no unused space
3. Variable Length Unspanned Blocking
	Variable-length records are used, but spanning is not employed
## Record-Blocking Methods
![[Pasted image 20251114142933.png]]
# File Allocation (1 of 2)
On secondary storage, a file consists of a collection of blocks
The operating system or file management system is responsible for allocating blocks to files
The approach taken for file allocation may influence the approach taken for free space management
Space is allocated to a file as one or more portions (contiguous set of allocated blocks)

**File allocation table** - Data structure used to keep track of portions assigned to a file

# Pre-allocation versus Dynamic Allocation
## Preallocation Policy
A requires that the maximum size of a file be declared at the time of the file creation request

- For many applications, it is difficult to estimate reliably the maximum potential size of the file
	- tends to be wasteful because users and application programmers tend to overestimate size

## Dynamic allocation
Allocates space to a file in portions as needed

# Portion Size
In choosing a portion size there is a trade-off between:
- efficiency from the point of view of a single file versus
- overall system efficiency
Items to be considered:
- **contiguity of space** increases performance, especially for `Retrieve_Next` operations, and greatly for transactions running in a transaction-oriented operating system
- Having a **large number** of small portions increases the size of tables needed to manage the allocation information
- Having **fixed-size** portions simplifies the reallocation of space
- Having variable-size or small fixed-size portions minimizes waste of unused storage due to overallocation

Two Major Alternatives
- **Variables** (Large contiguous portions)
	- Provides better performance
	- The variable size avoids waste
	- The file allocation tables are smal
- (Fixed) **Blocks**
	- Small fixed portions provide greater flexibility
	- They may require large tables or complex structures for their allocation
	- Contiguity has been abandoned as a primary goal
	- Blocks are allocated as needed
# File Allocation Methods
![[Pasted image 20251114143829.png]]

# Contiguous File Allocation
![[Pasted image 20251114143842.png]]
# Contiguous File Allocation (After Compaction)
![[Pasted image 20251114143853.png]]
# Chained Allocation
![[Pasted image 20251114143904.png]]
# Chained Allocation (After Consolidation)
![[Pasted image 20251114143912.png]]
# Indexed Allocation with Block Portions
![[Pasted image 20251114143931.png]] 
# Indexed Allocation with variable-length portions
![[Pasted image 20251114143939.png]]
# Free space management
Just as allocated space must be managed, so must the unallocated space
To perform file allocation, it is necessary to know which blocks are available
A disk allocation table is needed in addition to a file allocation table
# Bit Tables
This method uses a vector containing one bit ofr each block on the disk
Each entry of a 0 corresponds to a free block, and each 1 corresponds to a block in use

Advantages:
Works well with any file allocation method
It is as small as possible
# Chained free portions
The free portions may be chained together by using a pointer and length value in each free portion
advantages
- Negligible space overhead because there is no need for a a disk allocation table
- Suited to all file allocation methods
Disadvantages
- Lead to fragmentation
- Every time you allocated a block you need to read the block first to recover the pointer to the new first free block before writing data to that block
# Indexing
- Treats free space as a file and uses an index table as it would for file allocation
- For efficiency, the index should be on the basis of variable-size portions rather than blocks
Advantage:
- This approach provides efficient support for all of the file allocation method
# Free block list
- Each block is assigned a number sequentially
- The list of the numbers of all free blocks is maintained in a reserved portion of the disk
	- Depending on the size of the disk, either 24, or 32 bits will be needed to store a single block number
	- The size of the free block list is 24 or 32 times the size of the corresponding bit table and must be stored on disk
There are two effective techniques for storing a small part of the free block list in main memory:
- As a push-down **stack** with the first few thousand elements of the **stack** kept in main memory
- As a FIFO **queue** with a few thousands entries from both the head and the tail of the queue in main memory
# Volumes
A collection of addressable sectors in secondary memory that an OS or application can use for data storage
- The sectors in a volume need not be consecutive on a physical storage
- device (but appear that way to OS or applciation)

# UNIX File management
In the UNIX file system, 6 type of files are distinguished:
- **Regular, or ordinary** - Contains arbitrary data in zero or more data blocks
- **Directory** - Contains a list of file names plus pointers to associated inodes (index nodes)
- **Special** - Contains no data but provides a mechanism to map physical devices to file names
- **Named pipes** - An interprocess communications facility
- **Links** - An alternative file name for an existing file
- **Symbolic Links** - A data file that contains the name of the file which it is linked
# File Allocation (2 of 2)
All types of UNIX files are administered by the OS by means of inodes
## Inode
An inode (index node) is a control structure that contains the key information needed by the operating system for a particular file
- Several file names may be associated with a single inode
- An activate inode is associated with exactly one file
- Each file is controlled by exactly one inode
- File allocation is done on a **block basis**
- Allocating is **dynamic** ,as needed, rather than using Preallocation
- An **indexed** method is used to keep track of each file, with part of the indexed stored in the inode for the file
- In all UNIX implementation the inode includes a number of direct points and three indirect pointers (single, double, triple)
## Structure of Free BSD Inode and File
![[Pasted image 20251114145658.png]]
# Unix Directories
![[Pasted image 20251114145928.png]]
- Directories are structured n a hierarchical tree
- Each directory can contain files and/or other directories.
- A directory that is inside another directory is referred to as a **subdirectory**
- A **directory** is simply a file that contains a list of file names plus pointers to associated inodes
- Each directory entry (dentry) contains a name for the associated file or subdirectory plus an integer called the i-number (index number)
- When the file or directory is accessed, it is i-number is used as a index into the inode table.
# Volume Structure
A UNIX file system resides on a single logical disk or disk partition and is laid out with the following elements:
**Boot Block** - Contains code required to boot the OS
**Superblock** - Contains attributes and information about the file system
**Inode table** -Collection of inodes for each file
**Data blocks**- Storage space available for data files and subdirectories.