# Greedy Algorithms
Greedy Algorithms work in **phases**, in each phase a decision is made that appears to be good, **without regard** for future consequences
- Take What you can get now strategy
- Generally the decision we make at each phase is to choose some local optimum
- When the algorithm terminates, we hope that the **local optimum is equal to the global optimum**
		If this is the case, the the **algorithm is correct**, otherwise the algorithm has produced a **suboptimal solution**
- Sometimes used to generate approximate answers if the best answer is the not required.

## Examples
### Djikstra's
Each iteration choose then next node to explore, from the priority queue, with the least cost so far (local optimum)
### Prim's
At each iteration add the path with least cost(local optimum) as long as the node it leads to has not been visited already and does not create a cycle.
# Divide and Conquer
Divide-and-Conquer algorithms consist of two parts:
- **Divide**: Smaller problems are solved recursively (except base case)
- **Conquer**: the solution to the original problem is then formed from the solutions to the subproblem
## Example
- Merge Sort
- Quick Sort

## Runtime of Divide-and-Conquer Algorithms
By the nature of how Divide-and-Conquer algorithms are structure their runtime can be calculated using the following recurrence relation:
$$T(N) = aT(N/b)+f(N)$$
where *a* is the number of **subproblems** we solve at each step
*b* is how large the **original** problem size is compared to the subproblem size
and $f(n)$ is any additional work to solve the sub problem

$$
T(N) =
\begin{cases}
O(N^{log_{b}a})& a>b^k(1) \\
O(N^Klogn)& a=b^k(2)\\
O(N^k)& a<b^k(3)
\end{cases}
$$

this covers the case where $f(n)$ runs in the $O(N^k)$

### MergeSort Run Time Calc
Mergesort operates on two problem at each step $(a=2)$, each of which is **half** the size of the original $(b=2)$, and then also does up to $(O(N) = f(N))$ additional work at each step to recombine arrays. 

So we can calculate the time it takes for mergesort using the follow recurrence relation: 
$$T(N) = 2T(N/2) + O(N)$$
Since mergesort has $a=b=2$ and $k=1$. The second case (2) applies, giving the answer $O(Nlog(N))$
# Dynamic Programming

## Motivation - Fibonacci Revisited
In week 1, we looked a the Fibonacci sequence when discussing Big-O notation. The analysis showed that to calculate the $n^th$ Fibonacci number, we need to calculate the $(n-1)^th$ and $(n-2)^th$ Fibonacci numbers. This results in a time complexity of $O(2^n)$ since we create a tree of depth $n$ with a branching factor of 2.
## Tabulation (Bottom Up)
So sintead of a top down approach, let's try building the Fibonacci sequence from the bottom up, this is known as **tabulation**

### Example code
```java
public class FibonacciSimple {
	public static int nth(int n){
	if(n==1){return 0;}
	if(n==2){return 1;}
	int previous = 0;
	int current = 1;
	while (n - 2 > 0){
		int temp = current;
		current = previous + current;
		previous = temp;
		n--;
	}
	return current;
}
```
### Question
**Question**: What is the time complexity of the above code?
O(n)

## Recursive (Top-Down)
**Question**: Can we identify why the recursive approach is so slow?
The recursive approach is slow because it recalculates the same Fibonacci numbers multiple times. We can see that fib(2) is calculated 3 times, for example

### Main Reason this is Slow:
The recursive solution breaks the main problem down into **sub-problems** which **are**:
- symmetric
- have a lot of overlap between them
This is a common feature of many problems and dynamic programming a technique that can be used to solve these problems more efficiently.


For certain problems, like calculating the nth Fibonacci number, We like the **top-down** (recursive) approach because it is **easy to understand** and **represents the problem well**.

**Question:** Is there a way to combine the top-down approach with the runtime efficiency of bottom-up approach?

If we **store the results of sub-problems**, we can use the top-down approach to solve the problem. This is called **memoization**.
## Memoization
Let's try to write the program where we use memoization to store the results of the sub-problems so that we can look them up rather than re-compute them. THat way we avoid repeated compuations.

**Question**: what kind of data structure should we use?
Hashing! Use Java HashMaps
### Code Example
```java
import java.util.*;

public class FibonacciMemoized {
	static Map<Integer,Integer> memoizedValue = new HashMap();
	
	static {
	memoizedValue.put(2,1);
	memoizedValue.put(1,0);
	}
	
	public static int nth(int n){
		if(memoizedValue.containsKey(n)){
			return memoizedValue.get(n);
		}
		int value1 = nth(n - 1);
		int value2 = nth(n - 2);
		int value = value1 + value2;
		memoizedValue.put(n,value);
		return value;
	}
}
```
#### RunTime
**Question:** What is the time complexity of the above code?
**Answer:** 
1. If the value if being **calculated is in the memoization hash table** it will be O(1).
2. If value being calculated is **not** in the hash table, but there are smaller results in the hash table, then we need to **perform some calculations** but we can **use the smaller values** present. O(N)
3. If the value being calculating is **not** in the hash table and there are **no smaller results** in the hash table, then we need to **compute the result recursively**.

## Terminology and Background
A technique used to solve problems by breaking them down into simpler sub-problems (divide-and-conquer). With the important difference between it and the divide-and-conquer approach being that the simpler problems are not a clear division of the original. because sub problems are repeatedly solved, it is important to record their solutions (in a table) rather than recompute them.

**Effective** when the sub-problems are **symmetric** and there is **a lot of overlap** between them
## Optimal SubStructures
Dynamic programming is based on the **principle of identifying optimal substructures.**
This means that the optimal solution to problem can be constructed from the optimal solutions to its sub-problems.

The **challenge with dynamic programming** is to identify the sub-problems and the relationship between them, as well as how to compute them efficiently.

In the case of Fibonacci sequence, the means of constructing the optimal substructures were given to us by the definition i.e.
$$F_n = F_{n-1} + F_{n-2}$$
Let's look at some other examples to see if we can identify the sub-problems and the relationship between them.
- The Climbing Stairs Problem
- Optimal Binary Search Tree Creation
## Climbing Stairs Problem
The climbing stairs problem is described as follows:
- you are given an integer array cost where `cost[i]` is the cost of the ith step on the staircase. Once you pay the cost, you can either climb one or two steps.
- You can either start form the step with index 0, or the step with index 1.
- Return the minimum cost to reach the top of the staircase.

Let's think about how we can approach the problem. We could take the same approach as we did the Fibonacci sequence and use a recursive approach. If `minCost(i)` denotes the minimum cost to get to the last step from step `i`, then we have:
$$
minCost(i) = cost[i] + min(minCost(i-1),minCost(i-2))
$$
## Top-Down
### Time Complexity
What is the time complexity for the **top-down** approach **<u>without dynamic programming?</u>

- Assuming the cost to calculate the minimum of 2 values is O(1).
- At each step we have 2 choices: 1 step or 2 steps
- So, the total of function calls will be $2^n$ where $n$ is the number of steps.
- Thus, the time complexity is $O(2^n)$

As Fibonacci, let's start with the approach (top-down **without** memoization) and then figure out what the overlapping sub-problems are.
#### Code Example (Without DP)
```java
public class ClimbingStairs{
	private int[] costs;
	
	public ClimbingStairs(int[] costs){
		this.costs = costs;
	}
	
	public int getMinCost(){
		return Math.min(minCost(costs.length - 1),
		minCost(costs.length-2));
	}
	
	private int minCost(int currentIndex){
		if (currentIndex < 0) return 0;
		if (currentIndex == 0 || currentIndex == 1) return costs[currentIndex];
		
			return costs[currentIndex] + Math.min(minCost(currentIndex - 1),minCost(currentIndex -2));
		
	}
}
```

How can we identify where the overlapping sub-problems are?

We can do this **analytically** or by **observing the stack trace** in the debugger.

Using either method, we will quickly observe that finding the minCost from step i will always involve calculating minCost(j), where $j<i$ (assuming we start from the last step and work backwards, like for the Fibonacci top-down approach without memoization)

Instead of re-computing we can use memoziation to store than recompute
## Memoization
Look at slides for code

**Questions:** What is the time complexity of the above code?
O(n), for the exact same reasons as the Fibonacci memozied solution.


... you get ti by now i'm done transcribing 
## Summary