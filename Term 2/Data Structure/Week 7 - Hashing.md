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
The result of not meeting these criteria is that we may end up in a situation where we've essentially implemented a linked list and will have to iterate through all elements to find the one we are looking for.

### Designing the Probing Function for Open Addressing
![[Pasted image 20260217141724.png]]
This is expected performance of Linear probing.


### Separate Chaining vs. Probing
It depends on the data we are working with. However these are some observation
- If space is at a real premium, then open addressing (probing) is better.
- Deletion is simpler to implement for separate chaining than open addressing 
	- Think about when Hash(x) == Hash(y) == Hash(z). If x deleted how to retrieve y,z
- Otherwise, we know linear probing suffers from clustering and separate chaining can suffer from long linked list, so neither is perfect
# Quadratic Probing
The next method is designed to deal with clustering problem: **Quadratic probing**. This idea is that instead of probing linearly, we probe quadratically.
Meaning if there is a collision at index $i$, we will probe at $i+1^{2}, i+2^{2},i+3^{2},$ etc. **until we find a free cell**.

We can see that this will help with avoid clustering since it introduces some 'random' behaviour, but we can also see that it will help to avoid the problem of having a lot of empty space in the table. This is because we can see that we will probing at a distance from the original index.

## Hash Table Size
We need to be careful when picking the size of the hash table. For example, if we pick a table of size 10, if our  hash function maps an elements to position 2, then we will look at position 3, 6,11(=1),18(=8),27(=7),38(=8),51(=1),66(=6),83(=3) etc.

As you can see we skip over a lot of indices.
### Reasoning
We want to find out if an element hashes to position $i$, what are the possible positions we can probe at. We can see that for a given hash function $h$, if h(x)=j,, then we can see that the possible positions we can probe at are $j+i^{2}$ for $i=0,1,2,...$ If we want every possible position to be probed, then we know that $j+i^{2}$ will need to eventually generate each value in the range $0,1,2,...,m-1$ where m is the size of the hash table.


So for each value $0,1,2,...m-1$, we need to find a value of $i$ such that $j+i^{2}$ = $k\%m$ for some k. As it turns out, we can't do this form any values of k, especially for non-prime m. 

As an example what happens with n=16.
![[Pasted image 20260217142957.png]]
Here we can see that 0,1,4, and 9 are the only buckets which will be probed when using quadratic probing for a value that hashes to 0. not good!

For linear probing it is a bad idea to let the hash table get nearly full, because performance degrades. For quadratic probing, the situation is even more drastic: There is no guarantee of finding an empty cell once the table gets more than half full, or even before the table gets half full if the table size is not prime( as we can see in the table above.)

Thankfully, we are given a guarantee that if quadratic probing is used and the **table size is prime** , the an new element can always be inserted if the table is at least half empty.


## Prime Size
Clearly this is quite a weak guarantee in that we're only guaranteed to find a free cell if the table is at least half empty. However, if the table is more than half full it turns out the probability of failure to find a location is low. This is because in the worst case, the empty slots are precisely those which are quadratic residues. There are few circumstances in which this will occur.

Again, it's really important to note that if the table size is not prime, ,the number of alternative locations can be severely reduced. As an example, if the table size were 16, then the only alternative locations would be at distance 1,4, or 9 away (why?)


### Drawback
One <u>drawback</u> we can observe with quadratic probing is **secondary clustering**, which is when the same sequence of probes is used for many elements. Even if the table size is prime, we can see that this can happen. This is because the quadratic function is deterministic and so if we have a lot of elements which hash to the same index, they will all probe at the same locations. this is directly analogous to the linear probing problem:
# Double Hashing
Collision Resolution method called **double hashing**. The idea is that we use <u>two hash functions to determine the next index to probe</u>. the first hash function gives us the <u>initial index</u>, and the second hash function gives us the <u>step size to probe</u>.

The idea is similar to quadratic probing - we want to avoid clustering, so we hope the second hash function distributes elements evenly across buckets:

Since we understand the general idea well now, we can skip ahead and take a look at some examples of **double hashing**. One populat choice for hte second hash is f(i) = i* $\text{hash}_{2}(x)$. This formula says that we apply a second hash function to $x$ and probe a at distance $\text{hash}_{2}$(x), etc.

As before, we ideally want it such that all cells can be probed. We know from our quadratic probing analysis that starting with a prime table size is a good idea. it then remains to figure out a a good choice of second hash. A function such as $hash_{2}$(x) = $R - (x \% R)$, where R is a prime smaller than TableSize, will work well, since it will ensure that all cells can be probed.

### Example
Let's see an example of this in action. Suppose we have a hash table of size TableSize =11 (a prime numbeer), and we use the following hash cuntions:
![[Pasted image 20260217145227.png]]
The final hash tbale after insterting these elements would look like:
![[Pasted image 20260217145243.png]]
This demonstrates how double hashing effectively resolves collisions while ensuring all cells can be probed.
## Bad Secondary Hash Function in Double Hashing
Let's see what a bad example is, TableSize = 10
![[Pasted image 20260217145411.png]]

**Problem**: The secondary hash function only produces values {2,3,4,5}, which doesn't allow all table indices to be probed.
![[Pasted image 20260217145443.png]]
**Key Issue**: The probe sequence does not visit indices {0,2,6,69}, meaning some slots can never be used! **Solution**: Hash 2(x) is **coprime** with Table Size or Use R-(x%R) with prime R

## Good properties
Some properties of good double hashing function are:
1. It should never yield an index of zero (to avoid infinite loops).
2. It should cycle through the whole table (to avoid clustering)
3. It should be very fast to compute (or we are defeating the purpose of hashing)
4. It should be pair-wise independent of $h_{1}$ (to avoid secondary clustering).
5. $h_{2}$ should have the same effect as a random-number generator (to avoid secondary clustering).

If double hashing is used correctly, empirical analyses imply that the expected number of probes is almost the same as for a random collision resolution strategy. This makes double hashing theoretically interesting. 

**Quadratic probing**, doesn't required the use of a second hash function and is thus likely to be simpler and faster in practice, especially for keys like strings whose hash functions are are expensive to compute.

## Big-O Complexity
We should not the Big-O complexity of double hashing is still O(n). This is because we can't guarantee that we will find a free cell in a reasonable amount of time and essentially end up with a linked list.

As before, if we make good choices for the table size and and out hash function based on the data we anticipate storing, it's much more likely to be close to O(1) (but not guaranteed.)

# Re-Hashing
One thing we have not addressed is what happens if our hash table fills up. If this happens, we know that we will be restricted to essentially a sequential search (which we don't want). In the case of probing insertions might even fail entirely.

Rehashing helps by increasing the size of the hash table. the idea is that we create a new hash table which is bigger than the old one. We then rehash all the elements in the old table into the new table. This is costly operation, but it is a necessary to ensure that the hash table remains efficient.

The run time of rehashing is **$O(n)$**, since there are N elements to rehash and the table size if roughly 2N, but it is actually not all that bad, because it happens very infrequent (if you have a good hash function).

One thing to be wary of is that if you're designing a user-facing system, the user who causes a re-hash might be waiting a lot longer than other users!

## When to Rehash
Rehashing can be implemented n several ways with quadratic probing.
1. One alternative is to rehash as soon as the tblaei s half full, since we know after this point insertions may be become problematic. This is clearly a pessimistic approach since it's still unlikely to have an issue at this stage.
2. We could go to the other extreme and only rehash when we have an insertion actually fail.
3. A third, middle-of-the-road strategy is to rehash when the table reaches a certain load factor. Since performance does degrade as the load factor increases, the third strategy, implemented with a good cut-off, could be best. 

### Getting to O(1) Performance
All of the hash table implementations we have studied so far reesult in a O(n) runtime in the worst case. In this section, we look at an implementation that will guarantee O(1) performance for insertion, deletion, and lookup. This is known as **perfect hashing**.

