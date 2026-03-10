# Preamble
>Q: Don't BST already store data in a sorted order?
Yes, but if we agiven a collection of n things, we need to do a in-order traversal, we'd require O(nlogn) to inser the n things, then a further O(n) for in-ordre traverseal
# Sorting Algorithms
## Bogo Sort
A brute force approach to sorting to give us an understanding of how inefficient it can be, called **bogosort**. Thankfully it is simple to write, we just randomly swap two elements in the array until it is sorted:

**Best Case**: O(n)
**Average Case** E\[operations] = E\[failures] $\times \frac{operations}{failures} +O(n)$
..
$O(n*n!)$
**Worst Cast** O($\infty$)

## Bubble Sort
Iterate over the array and every time we see a pair of elements out of place we swap them:

**Best Case** O($n^2$)
**Average Case** O($n^2$)
**Worst Case** O($n^2$)
## Insertion Sort
Build an sorted array from scratch by sequentially inserting the elements into the correct position
**Best Case** O(n)
**Average Case** O($n^2$)
**Worst Case** O($n^2$)
## Merge Sort
We split the array in two halves then recursively repeat till size 1 then we merge the arrays back together in a sorted order
![[Pasted image 20260310134309.png]]

**Best Case** $O(nlogn)$
**Average Case** $O(nlogn)$
**Worst Case** $O(nlogn)$
## Heap Sort
Heap sort is a **comparison-based** sorting algorithm that uses a binary heap data structure.
- the tree is complete, meaning all levels are fully filled except possibly the last level, which is filled from left to right
- The heap property must be maintained, meaning for a max-heap, each parent node is greater than or equal to  tis children, and for a min-heap, each parent node is less than or equal to its children.

Heap sort involves 2 main steps:
1. Build a **max-heap** from the input data
2. Repeatedly extract of the maximum element from the heap and rebuild the heap until all elements are sorted.
![[Pasted image 20260310134545.png]]

**Best Case** $O(nlogn)$
**Average Case** $O(nlogn)$
**Worst Case** $O(nlogn)$
## Quick Sort
Divide-and-conquer algorithm which is similar to merge sort. It works by a *pivot* element form the array and partitioning the other elements into 2 sub-arrays.

When Selecting pivot
- Select first element in the array as the pivot.
- Parition the array into 2 sub-arrays:
- We then recurse in the sub arrays

![[Pasted image 20260310134811.png]]

**Best Case** $O(nlogn)$
**Average Case** $O(nlogn)$
**Worst Case** $O(n^2)$
# Linear Time Sorts
In some special cases, we can reduce the time taken to sort an array to O(n), which is the best possible time complexity for a comparison-based sorting algorithm. We'll look at two such algorithms: bucket sort and radix sort
## Bucket Sort
![[Pasted image 20260310134953.png]]

The input for bucket sort ($A_1,A_2,...,A_N$) must consist of only positive integers smaller than $M$. If this is the case, then the algorithm is simple:
- Keep an array called count , of size $M$, which is initialized to all 0s. So count has $M$ cells, or *buckets*, which are initially empty.
- When $A_i$ is read, increment count\[$A_i$] by 1.
- After all the input is read, simply scan the count array/hashtable. Since we are reading/writing to/from random locations in an array, we known this is a fast operation (i.e. constant time).
- If an item appears twice in the output, it can be added twice to the end of the output array.

O(1) read each element (become O(N))
We need to scan count array, O(M)
**Best Case** O(n+M)
**Average Case** O(n+M)
**Worst Case** O(n+M)

### Analysis
**Question:** If i know that I am sorting a list of numerical student IDs, would bucket sort be a good choice?
**Answer:**: If the student IDs are all positive integers and the range of IDs is not too large, then bucket sort would be a good choice.

## Radix Sort
**Radidx** sort is sometimes known as *card sort* because it was used until advent of modern computers to sort old-style punch cards. It is a non-comparison-based sorting algorithm that works by distributing elements into buckets based on their individual digits.

The general idea is that if we have numbers in a big range (that might not fit in memory), we can iteratively sort them by their digits. We start by sorting the least significant digit and work our way up to the most significant digit. We'll essentially be doing several passes of bucket sort.

The natural algorithm would be to bucket sort by the most significant digit (digit is taken to base $b$), then next most significant, and so on.

A simpler idea is to perform bucket sorts in the reverse order, starting with the least significant digit first. Of course, more than one number could fall into the same bucket, and unlike the original bucket sort, theses numbers could be different , so we keep them in a list (like separate chaining in a hash table)

- We start by sorting the numbers by their least significant digit.
- We then sort the numbers by their next least significant digit.
- In general, after the $k$th pass, the items are sorted on the $k$ least significant digits
- We continue this process until we have sorted the numbers by their most significant digit.

![[Pasted image 20260310140227.png]]

$b$ = number of buckets 
$n$ = number of elements

time complexity to scan and place in correct bucket is $O(n+b)$

**Best Case**/**Average Case**/**Worst Case**
Then we need to do for $d$ (each digit) $O(d(n+b))$
