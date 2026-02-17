# From Trees to Hash Tables
Given this set of requirements, we can start to piece together how we could design a data structure to manage this:
- We know that random access in our arraylist is fast O(1) faster than O(n) for a tree
- However, we also know that searching in an arraylist is O(n) so we will need to get around that
- We can see that our tree structure is fundamentally flawed for this problem as we don't need to order the words, so we will focus on some kind of array-based representation.

Let's think about how we might modify our arraylist to support quicker inserts/deletes:
- Random access is quick due to array indexing so we will try keep that.
- Insertion is slow because we may have to do a 'shuffle forward' operation to make space for the new element. Same with deletion and 'shuffle back'

To avoid the shuffle forward/backward problem, we need to be able to place list elements elsewhere (anywhere free perhaps) in the array-like data structure. But still be able to efficiently retrieve them.
# HashTable
The answer to the **quick insertion/deletion** is perhaps not fully intuitive. We will introduce the concept of a **hash table** to give the solution. You can think of a hash table as a being similar to an array list. Both use an **array as the underlying data structure**

The key difference is that in a hash table, we use something called a **hash function** to determine **where to place the element** in the array, whereas in an array list, we use the index of the element.
## Example
Let's take a simple, contrived example to illustrate the concept of a hash table. Suppose you have a set of friends and you know that their names are unique and begin with aa different letter of the alphabet. To store them in a hash table, you could use the first letter of their name as the hash function.
### Sample Example
![[Pasted image 20260217134238.png]]

We can see that lookup, insertion and deletion are all O(1) operations. This is because we can calculate the index of the element in the array in constant time (by just taking the first letter of the persons name).

However, we have a severe problem in that we can only store a maximum of 26 elements in our array. This is made even worse because we are limited to one person per letter of the alphabet
## Handling Collisions
A **collision** is the term used to describe when <u>two elements map to the same index in the hash table</u>. This is a problem because we can't store two elements in the same index. We can see that there are 2 approaches to dealing with collisions:
1. Avoid them by designing a good hash function.
2. Handle them well when they do occur.
We'll star by describing some strategies for handling collisions.

# Separate Chaining
In our example, if we have already inserted 'Adam' into our hash table, then we try to insert 'Abigail', we can see that both map to the same index. So we we need to figure out what todo with 'Abigail'

>**Separate Chaining**
Separate Chaining is a strategy where we store a linked list at each index in the hash table. When we have a collision , we add the new element to the linked list. This means that we can store multiple elements at the same index.
## Supplemental info
- Invented in 1953 by Hans Peter Luhn while working at IBM- 
## Example
![[Pasted image 20260217134754.png]]

This offers a solution to our problem, where now we have overcome the limitations we had. But we can see that we have introduced a new problem.

The problem is that we introduced the linked list into our hash table which will slow down our operations. As Big-O of the operation are now O(n) where n is the number of elements in the linked list.

>Does this mean we are back to Square 1?
### Analysis
- **Worst Case**: Scenario is that all n elements map to the same index. This mean we have to iterate through all elements of the linked list to find the element we are looking for. This is O(n)
- **Average Case** is that we have $n/m$ elements in each linked list, where $m$ is the number of indices in the array. This means that the average case is O(n/m)
- **Best Case** is the that we have $n<=m$ elements, where $m$ is the number of indices in the array and each element is mapped to a unique index. This means that the best case is O(1)

>So, it depends; on the data that we anticipate using the hash function.  If we know the will have a lot of collisions, then we can see that the worst case will be O(n) - all of the elements are chained in a a linked list for the same index- which is not ideal. But if we know that we won't have many collisions, then the average case should get close to O(1) when $n$ and $m$ are about the same which is ideal.

So depending on the application, we might realize that the data structure is suitable. We may also realize that it is not quite suitable, but if we were to make a small change too the hash function( i.e. now we could use the first 2 letters of the name), then we could make it suitable. But that would come at the cost of a lot more space for a larger hash table.
![[Pasted image 20260217135643.png]]

#### Analysis
In total, this table would require $26 * 26 = 676$ indices. We can see that we have more positions to insert, but we  can also see that we have a lot of empty space. This is the trade-off we make when we increase the number of indices in the array. If we anticipate we have a lot of names being entered, this might be a good trade off. If we anticipate we have a very few names being entered this might not be a good trade off.

>Hash function for 2 letters
>f(name) = name\[0] + name\[1]
>where a->0, b->1, c->2, etc.


Why is this not ideal
(How often Da will appear compared to Dx)

## Separate Chaining Load Factor

To help the perform our analysis, we can introduce a new variable $\lambda$ which is the <u>ratio of the number of elements in the hash table to the table size</u>. We can see that in our example, $\lambda=n/m$ where n is the number of elements in the hash table and m is the number of indices in the array.
## Summary
>Take Home Message
>The distribution of the data that we will be working with should have a very strong influence on how we design our hash function and hash table. Even in different languages, certain pairs of letters will occur much more frequently than others, resulting in a cluster of collisions.

- Separate chaining is a strategy to handle collisions in a hash table.

Assuming that the *load* factor, $\lambda$, is $\approx1$ (i.e. each bucket in the table has approximately the same, small number of elements), the average case for insertion/deletion/lookup is O(1). But we can see that is not guaranteed and the worst case is O(n), where every element ends up in the same bucket

### Code
Points to note:
- The hash function is general purpose.
	- Designed so that it would work with any string data and distributes the data evenly
- It contains a rehash function, which gets called if an list gets too big
	- Common strategy to ensure that the load factor remains low
- It will use a prime number to decide the number of buckets
	- We will see why later
# Probing Hash Tables and Open Addressing
We've seen that separate chaining gives a mechanisms to deal with collisions as they happened. But we can also see that we have introduced a new data structure (linked list) which will slow down our operations. We'll now examine a new strategy to deal with collisions call **open addressing**

Probing - searching for next available slot to fit result
## Open Addressing
The idea behind open addressing is that when we have a collision, we will try to find the next available index in the array to place the element. So our hash function will give us the index of the elements, but if that index is already taken, we will try the next index, and the next index, etc.  according to another function.

>We can immediately conclude that probing hash tables will have to be bigger than separate changing hash tables. This is because we can't have linked list at each index. We can see that the size of the probing hash table will have to be at least the size of the data we are storing. Let's take a look at how this might look

![[Pasted image 20260217140834.png]]
We can see that in these cases, our hashing function maps names beginning with A to index 0 and then we use linear probing to find the next available index. We can se that hte hash function is

f(name) = name\[0] and the probing function is g(i) = i+1

As long as the **table is big enough**, a <u>free cell can always be found</u>, but the <u>time</u> to do so can <u>get quite large</u>.

### Analysis
There is a **fundamental problem**, we can see that the time to find a free cell can get quite large. This is because of <u>time to find a free cell</u> is $O(n)$ where n is the number of elements in the hash table. This is because we may have to iterate through all elements in the hash table to find a free cell. Think what will happen if everyone in our dataset has a name beginning with A.

![[Pasted image 20260217141143.png]]
We can see that linear probing will sometimes create unwanted 'clusters'. If we now add anyone who's name begin with either 'A' or 'B', we'll have to probe to find the next free cell
## Probing Function
The **probing function** is clearly very important (as well as the hash function). We can see that a couple of **important criteria** that it should aim to meet:
1. It should be designed to ensure that we can always <u>find a free cell</u>.
2. It should be designed to ensure that we <u>don't</u> end up in a <u>infinite loop</u>.
3. It should be designed to ensure that we <u>don't</u> end up in a situation where we have a <u>lot of empty space</u> in the table.
The result of not meeting these criteria is that we may end up in a situation where we've essentially implemented a linked list and will have to iterate through all elements to find the one we are looking for

# Quadratic Probing


# Double Hashing
# Re-Hashing