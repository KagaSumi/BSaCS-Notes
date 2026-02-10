# Graph Search
## Graph Search Problem
Given a graph G=(V,E), a start nodes $s \in V$ and a goal node $g \in V$, find the shortest path from s to g
![[Pasted image 20260210133428.png]]
Sometimes we only want to compute a single shortest path. it may not even be feasible to run Dijkstra's algorithm on a large graph

We can see that DFS, BFS and Dijkstra's algorithm can be modified so that once we mark our goal node as 'visited'. These all give us an immediate answer to the graph search problem

We group these strategies under the term '**Uninformed Search**' because they do not use any information about the goal node to guide the search.

## Why do we not want to use uninformed search strategies from graph search:
![[Pasted image 20260210133703.png]]
Its bovious that we don't want to search the entire graph to find the shortest path to another. We can see that when expanding the **frontier** set of nodes. It makes sense to explore towards the goal rather away from it. This is where **Informed Search comes in**
## Bi-Directional Search
before we move on to the informed searches, we will quickly take a look at bi-directional search. The idea behind bi-directional search is that if we start running a search from both the start and goal nodes, we can try to 'meet in the middle' to decrease search time.

If the two algorithms intersect, then we can stop. The check nca be done with each node is generated or selected for expansion, and with a hash table, **will take constant time**
# Informed/Heuristic Search
Bi-Directional search has helped us to gain some intuition on how we might do better than DFS/BFS/Dijkstra when searching. In this section, we will look at *informed* search strategies, that uses problem-specific knowledge beyond the definition of the problem itself. 

## Best-First Search
The General approach we consider is **best-first search**. Best-first search is an instance of the general graph search algorithm in which a node in the frontier is selected for expansion based on **evaluation function**, $f(n)$. The evaluation function can be construed as a <u>cost estimate,</u> so the node with **the lowest evaluation** is **always expanded first**.


### Choosing f(x)
The choice of *f* determines the search strategy. BFS and DFS both used a simple evaluation function that only considered the depth of the node in the search tree. Dijkstra's algorithm used the cost of the path to the node. 
>$f(n)$ for Dijkstra's algorithm = The cost of the path from the start node to $n$

Most best-first algorithms include, as a component of *f*, a **heuristic function** denoted $h(n)$

>$h(n)$ = estimated cost of the cheapest path from the state at node n to a goal state


Generally speaking, we can say that nodes in the frontier are expanded in order lowest cost. For **uninformed searches**, we avoid using heuristics to estimate the cost to the goal and instead minimize the cost from the start node to the current. 

## Greedy Best-First Search
**Greedy best-first search** tries to expand the node that is closest to the goal, on the grounds that this is likely to lead to a solution quickly. Thus it evaluates nodes by using just the **heuristic function; that is, $f(n) = h(n)$**

This means that we ignore the cost of the path to the node, and only consider the estimated cost of the cheapest path from the state at node `n` to a goal state.

### Example
![[Pasted image 20260210134712.png]]
![[Pasted image 20260210134720.png]]
>Assume we start at Arad and want to get to Bucharest

1. First node to be expanded from Arad will be Sibiu because its closer to Bucharest than either Zerind or Timisoara
2. Next node to be expanded will be Fagaras because it is closest.
3. Fagaras in turn generates Bucharest, which is the goal. Search will terminate.

#### Evaluation
We can see that the path is not optimal as the path selected is 32 km longer than Rimnicu Vilcea and Pitesti. This is why the algorithm is called 'greedy'.
### Pseudocode
```pseudocode
fucntion GreedyBestFirstSearch(start, target):
	mark start as visited
	add start to queue
	
	while(queue is not empty):
		current_node = vertex of queue with min distance to target
		remove current_node from queue
		
		foreach(neighbour n of current_node):
			if n not in visited then:
				if n is target:
					return n
				else:
					mark n as visited
					add n to queue
	return failure;
```
### Analysis
We can see that Greedy Best-First Search is **not guaranteed to find the shortest path.** We can also see that the **worst case** time and space complexity is $O(b^{m})$, where m is the maximum depth and b is the branching factor

We could potentially improve the algorithm by using a better heuristic function. This will lead to a better solution and potentially more efficient search procedure.

## A* Search

A* is a celebrated algorithm which was created as part of **Shakey project** and was first published in 1968 by Peter Hart, Nils Nilsson, and Bertram Raphael. As an extension of Dijkstra's Algorithm and uses both the actual cost to reach the node and the estimated cost to reach the goal.

### The A* Algorithm
The A* Algorithm finds the **least-cost path** from a given initial node to one goal node. As with Greedy Best-First Search, A* uses a heuristic function to estimate the cost of the cheapest path from the current node to the goal node. 

However, A* also uses a cost function that gives the actual cost of the cheapest path from the start node to the current node.

The evaluation function for A* is:

>$f(n) = g(n) + h(n)$

where:
- $g(n)$ is the cost of the path from the start node to node n (we used this in Dijkstra's Algorithm)
- $h(n)$ is the estimated cost of the cheapest path from the state at node n to a goal state

We can see that this is a modified Greedy Best-First Search to include the cost of path from the start node to the current node. This will cause A* to be **guaranteed** to find the **shortest path** from the start node to the goal node.

### Example
![[Pasted image 20260210134712.png]]
![[Pasted image 20260210134720.png]]
>Assume we start at Arad and want to get to Bucharest
>Same Example as above Arad -> Bucharest
![[Pasted image 20260210140143.png]]

We can see that the frontier nodes are now oriented towards the goal (unlike Dijkstra, where the search spread out in all directions.).
### PseudoCode
```pseudocode
function A_Star(start,goal,h);
	priority_q = {start}
	cameFrom = an empty map
	
	//currently known cost of the cheapest path from start to n.
	gScore = map with default value of infinity
	gScore[start] = 0
	
	//fScore[n] := gScore[n] +h(n)
	fScore = map with default value of Infinity
	//g(start) is zero so no need to add
	fScore[start] = h(start)
	
	while priority_q not empty:
		current = the next node in priorty_q
		if (current == goal): 
	        return reconstruct_path(cameFrom, current)
		priorty_q.remove(current)
		for each neightbour of current:
			tentative_gScore = gScore[current] + d(current,neighbour)
			if tentative_gScore < gScore[neighbour]:
				cameFrom[neighbour] = current
				gScore[neighbour] = tentative_gScore
				fScore[neighbour] = tentative_gScore + h(neighbour)
				if neighbour is not in priority_q:
					priority_q.add(neighbour)
	return failure
```

The algorithm looks a bit intimidating, but what we can see is that we have something very similar to Dijkstra's Algorithm. We can visualize how the search is carried out by using contour lines.
![[Pasted image 20260210140918.png]]
Inside the contour labelled x, all nodes have f(n) less than or equal to x, and so on. Because A* expands the frontier node of the lowest f-cost we can see that an A* search fans out from the starting node, adding nodes in concentric bands of increasing f-cost

### Optimality of A*
With uniform-cost search (A* search using $h(n)= 0$), the bands will be "circular" around the start state. With more accurate heuristics, the bands will stretch toward the goal state and become more narrowly focused around the optimal path.

As it turns out, A* is guaranteed to find the shortest path from the start node to goal node. 
#### Admissible
For A* to be optimal when used with tree,s we require to guarantee that a shortest path is found is that $h(n)$ be an **admissible heuristic**. An admissible heuristic is one that never overestimates the cost to reach the goal. Because $g(n)$ is the **actual cost** to reach n along the current path, and $f(n) = g(n) + h(n)$, we have as an immediate consequence that $f(n)$ never overestimates the true cost for a solution along the current path through n 
#### Consistent
A Second, slightly stronger condition called consistency (or sometimes monotonicity) is required for guaranteed shortest paths with graphs. A heurists $h(n)$ is consistent if, for every node n and every successor $n\prime$ of n generated by exploration, the estimated cost of reaching the goal from n is no greater than the step cost of getting to $n\prime$ plus the estimated cost of reaching the goal from $n\prime$

$h(n) <= c(n,n\prime) + h(n\prime)$
### Proof of Optimality
To prove A* is optimal we can
1. First establish that $h(n)$ is consistent, then the values of $f(n)$ along any path are nondecreasing.
2. Next we prove that whenever A* selects a node n for expansion, the optimal path to that node has been fonud.
3. Finally, we'll conclude the sequence of nodes expanded by A* is in nondecreasing order of $f(n)$. hence, the first goal node selected for expansion must be an optimal solution because f is the true cost for goal nodes (which have h = 0) and all later goal nodes will be at least as expensive

>If $h(n)$ is consistent, then the values of $f(n)$ along any path are nondecreasing.
>Suppose $n\prime$ is a successor of $n$; then
> $g(n\prime) = g(n) + c(n,n\prime)$ and we have:
$f(n\prime) = g(n\prime) + h(n\prime) = $ 
$= g(n) + c(n,n\prime) + h(n\prime)$ $>= g(n) + h(n)  =f(n)$

>ie: $f(n\prime) >= f(n)$

Whenever A* selects a node n for expansion, the optimal path to that node has been found.
>Were this not the case, there would be have to be another frontier node $n\prime$ on the optimal path from the start node to $n$ which would be placed higher in the priority queue.
>I.e because $f$ is nondecreasing along any path, $n\prime$ would have lower f-cost than $n$ and would have been selected first.

### Choosing Heuristic
Analysis of A* has shown that the choice of heuristic has a large impact on the runtime performance of the algorithm, since a good heuristic allows A* to prune away many of the $b^{d}$ nodes that an uninformed search would expand.

Its quality can be expressed in terms of the effective branching factor b*, which can be determined empirically for a problem instance by measure the number of nodes generated by expansion, N and the depth of the solution

If the total number of nodes generated by A* for a particular problem is N and the solution depth is d, then b* is the branching factor that a uniform tree of depth $d$ would have to have in order to contain $N+1$ nodes.

>$N+1 = 1+b\star+(b\star)^{2} +... + (b\star)^{d}$

For example, if A* finds a solution at depth 5 using 52 nodes, then the effective branching factor is $\approx 1.92$

Good Heurisitcs are those with low effective branching factor b*
# Minimum Spanning Trees
**Spanning Tree** - A spanning tree of a graph is a tree that spans all the vertices of the graph (ie it contains all the vertices of the graph). A spanning tree must have the same number of vertex as the graph, but less edges
**Minimum spanning Tree (MST)**: A minimum spanning tree is a spanning tree that has the minimum possible total edge weight.

## Minimum Spanning Tree (MST)
MSTs are used in a variety of applications, including network design, circuit design, and clustering. We'll look at one algorithms for finding MSTs: Prim's Algorithm. 

## How do MST look like
![[Pasted image 20260210145237.png]]
![[Pasted image 20260210145215.png]]
We can see that the MST is a tree that spans all the vertices of the graph and has the minimum possible total edge weight.

Note that if we removed $v_{3},v_{4}$ edge, and added the $v_{3},v_{1}$ edge, we'd end up with a spanning tree (but not a MST)
### Example
>What is the MST for the following graph
![[Pasted image 20260210145351.png]]
Answer:
![[Pasted image 20260210145412.png]]

>Question: Can there be more than one MST for a graph?
## Applications of MST

1. For the Travelling Salesman problem, The MST-based heuristic gives an approximation within 1.5 times the optimal solution via Christofides algorithm
2. If a government wants to plan road/road improvements between multiple villages, an MST ensures that all villages are connected with the minimum total road length.
3. In image segmentation (dividing an image into meaningful regions) an MST is used to rouping similar pixels while minimizing the  total "difference" between connected pixels.
# Prim's Algorithm
Prim's Algorithm is a greedy algorithm that finds a minimum spanning tree for a weighted undirected graph. The algorithm operates by building this tree one vertex at a time, from an arbitrary starting vertex, at each step adding the cheapest possible connection from the tree to another vertex.

Similar to Dijkstra's Algorithm

## From Dijkstra's to Prim
We need just a few modifications to turn Dijkstra's Algorithm into a MST algorithm. For each vertex we keep values $d_{v}$ and $p_{v}$ and an indication of whether it is known or unknown. $d_{v}$ is the weight of the shortest edge connecting $v$ to a known vertex, and $p_{v}$, as before, is the last vertex to cause a change in $d_{v}$.o

The update rule is now: After vertex v is selected, for each unknown w adjacent to v, $d_{w} = min(d_{w},c_{w},v)$

## Example:
![[Pasted image 20260210150523.png]]
![[Pasted image 20260210150548.png]]
![[Pasted image 20260210150555.png]]
![[Pasted image 20260210150602.png]]
![[Pasted image 20260210150609.png]]
![[Pasted image 20260210150614.png]]
![[Pasted image 20260210150620.png]]