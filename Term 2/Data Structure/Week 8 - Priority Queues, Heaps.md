# Priority Queue
Priority Queues are used in many applications:
- Bug-tracking systems where we want to fix the most critical bugs first
- Scheduling tasks in an operating system
- In a printing system staff might get priority over students.
- In our file system we want to identify the biggest or smallest file.

## How we characterize Priority Queues
A **priority queue** is a data structure that stores elements with associated priorities.

The **priority** an element is used to determine the order in which elements are removed from the queue.

The element with the **highest** priority is removed first

Priority queues will typically support the following operations:
- Insert(x,p) - Insert x with p priority
- deleteMin() - Remove with highest priority
- findMin() - Return the element with highest priority
### Priority Queue analogous
![[Pasted image 20260303134107.png]]

## Naive Implementation using Lists and BSTs
We could use a list and sort it every time we insert an element. this would give us a time complexity of $O(nlogn)$ for each operation.

We could use a binary search tree and insert elements in a way that the element with the highest priority is as the root. This would give us a time complexity of O(logN) for each operation

Similar to hash table, we can see that although these implementations will work and leverage things we're already familiar with, we know that we're doing **extra work** to maintain **full ordering** of the elements when we only care about hte highest priority element.

# Heaps
A heap is a tree data structure
More specifically, a **heap** is a binary tree that satisfies the heap property
The **heap property** is that value of each node is greater than equal to the values of its children (max-heap)
The root of the tree is the element with the highest priority.
We'll be looking at **binary heaps**, where each node has at most two children.

## Binary Heap
A binary heap is a **complete binary tree**. This means that **all levels** of the tree are **fully filled** except possibly for the last level, which is filled from **left to right**. Below is an example of a complete binary tree:
![[Pasted image 20260303134503.png]]

Note: We can have both *min-heaps* and *max-heaps*.
Both are analogous to each other but for a **min-heap** the **heap property** is that the value of each node is **less than** or equal to the values of its children.

**Question**: Can a Binary Heap be a BST?
**Answer**: In some cases, Yes!
![[Pasted image 20260303134733.png]]
## The Heap Property
Let's think about the heap property and how it relates to the structure of the tree. Why does it make sense to design things this way?
1. The root of the tree is the element with the 'highest priority'. We usually store a **direct reference to the root** so it can access it in constant time.
2. We can also see that each subtree maintains the heap property, this will reduce the time complexity of performing operations.
There is an outstanding question, however, and that is how to maintain the heap property when we insert or delete elements.

# Insertion in Priority Queues
## Heap Insertion

Let's tackle insertion. We know that when inserting, the new node must be placed at the next available location in the tree to ensure that it remains complete. We then need to figure out if we need to re-arrange the tree to maintain the heap property.
![[Pasted image 20260303135131.png]]

Note: Technically we could insert the node at any suitable location on the last level of the tree, but we'll see why the left-most choice actually makes things easy for us shortly.

Similar to AVL trees, we have 2 cases:
1. The new node obeys the heap property, in which case we're done.
![[Pasted image 20260303135252.png]]
2. The new node does not obey the heap property, in which case we need to do some work.

### Case 2 Example:
For case 2, we need to come up with an algorithm to regain the heap property. We can study the example below to try to come up with something. If we want to insert the value 23, we know that it will violate the heap property.
![[Pasted image 20260303135307.png]]


As for AVL trees, restructuring the tree is actually not too hard as long as we maintain the heap as we go. We can just look 'up' the tree and swap the new node with its parent until the heap property is satisfied. We know this is safe to do because each parent is greater than or equal to its children. 
![[Pasted image 20260303135351.png]]

If we insert 14 instead
![[Pasted image 20260303135449.png]]

### Binary Heap Insertion Big-O
Best Case - O(1) 
	{To achieve this we must keep track of the next 'free spot in the tree'}
Worst Case - O(log(n))
Average Case - O(log(n))


For insertion, we notice that we have the following options to keep track of the next location to insert
Either:
1. Traverse the tree to find the next avaiable spot.
2. Explicitly hold onto a reference to the last inserted node in the tree.
There is a third, **better option**
3. Since the tree must be *complete*, we can actually project it down onto an array and then use the array to find the next available spot. This is often referred to as the 'percolate up' strategy.

## Implementing Heaps Using Arrays
We're familiar with storing trees in a set of nodes. But we've only done this n the past to give us flexibility in creating/adding/removing nodes. For a complete tree, we don't need this since its structure is rigid. here's how we can use an array to store it instead:
![[Pasted image 20260303135927.png]]


This looks more complicated that it is. We can quickly see that each successive level of the tree will have $2^{i}$ nodes, since it is complete (with the exception of the last level). Since we only need to be able to find the indices of parents and children, we can use the following formulas. For any element in array postilion i:

- The left child is in position $2i$
- The Right child is in the ell after the left child $2i+1$
- The parent is in the position $\lfloor\frac{i}{2}\rfloor$

# Deletion in Priority Queues
In order to retain the property of having a complete binary tree, we must
- Remove the last instead node structure.
- Replace the value of the deleted node while retaining its structure.
![[Pasted image 20260303140352.png]]

So we've shifted the problem to dealing with where to put node $31$, and how to shuffle around the other nodes to maintain the heap property.


## Procedure 
If we place 31, in the deleted node structure we must carry out operations to maintain the heap property (children $\le$ their parent)
The procedure is as follows:
1. Place the floating value x in the deleted node's structure
2. Check if x $\le$ all of its children
3. if it is then stop and deletion is complete
4. otherwise swap it with its min child and repeat from step 2
5. keep repeating until x $\le$ its children or you've reached a leaf node.

![[Pasted image 20260303140552.png]]
### Big-O Analysis
Best Case - Heap property is trivially satisfied and we can replace the root - O(1)
Worst Case - We need to swap the root with its children until the heap property is satisfied - O(logn)
Average Case - Assuming we need to swap $\approx$ h/2 times - O(logn)


# Dijkstra's Algorithm Priority Queue
In order to use priority queue in Dijkstra's algorithm. We are still missing something, what is it?

We need to be able to update the priority of an element in the queue if we have found a new shorter path to it! So let's think about a how to add an update Priority method.


## Updating Priority
If we want to update the priority of an element, we simply need to find the element in the tree and then percolate it up or down the tree until the heap property is satisfied. This is relatively straightforward and doesn't require any new ideas.

## Non-Minimum Deletion
If we want to delete something from the priority queue altogether (maybe a print job can be canceled), we need to write a method to do this.

Like updating priorities, we don't need to introduce any new ideas - we can find the key and then call *updatePriority* with $\infty$ or $-\infty$ as the new argument. We can then call *deleteMin* to remove it.


## Create the Heap from a Given List
If we have a given list of elements, we might want to create the heap right away. We can do this by inserting each element into the heap one by one. This will give us a time complexity of $O(nlogn)$, but if you look at the process we can see that redundancy in the way we insert elements.

If instead we insert all the elements into the array arbitrarily and then call *percolateDown()* on each element, we can achieve a time complexity of O(n) instead. This is because we can copy everything into the array quickly and then just move the elements around to satisfy the heap property.

![[Pasted image 20260303141418.png]]

### Procedure
1. Select the last inserted parent node and denote it as x.
2. if x $\le$ any child stop
3. otherwise swap it with the min child
4. repeat step 3 until either x $\le$ child or you reach a leaf
5. repeat from step one with the next (last inserted) parent until you reach the root
# Using Heaps to solve the Selection Problem

The selection problem is a classic problem in computer science. It is the problem of finding the $k$th smallest element in a unsorted list.

The naive solution is to sort the list and then return the $k$th element. Depending on the algorithm chosen, this will result in a runtime of between $O(nlogn)$ and $O(n^2)$


## Using a Binary Heap to solve the selection problem

We can solve the selection problem using a binary heap in $O(nlogk)$. The algorithm is as follows:
1. Read all elements into the heap using our *buildHeap* method - O(n)
2. Call *deleteMin* $k$ times $O(k*log(n))$
3. The $k$th element return is the $k$th smallest element in the list.
4. The total time complexity is $O(n+klogn)$ . if $k=O(\frac{n}{log(n)})$, the running time is dominated by the buildHeap operation and is $O(n)$. For larger values of $k$, the running time is $O(k*log(n))$.

# Summary
Priority queues are useful data structure that can be used in many applications. Binary heaps are good way to implement priority queus.
We an use an array to store teh binary heap and that we can use the array to find the children and parrents of a node.
We can insert, delete, update priorities, and delete elements from the priority queue in $O(logn)$ time.