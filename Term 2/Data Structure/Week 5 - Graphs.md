# Graphs
## Definitions
**V**: A set of vertices (nodes)
**E** : A set of edges (connections between nodes)
Each edge **E** is represented by a pair of vertices(u,v)
Edges can be weighted or unweighted. If they are weights, then each edge has a value associated with it.
The **degree** of a vertex is the number of edges incident to it.
The **order** of a graph is the number of vertices, and the **size** a is the number of edges.
## Types of Graph
**Undirected Graph**: Edges have no direction (i.e. (u,v) and (v,u) represent the same thing)
**Directed Graph (Digraph)**: Edges have a direction.
**Weighted Graph**: Edges have weights(values).
**Unweighted Graph**: All edges have equal weight.
**Cyclic and Acyclic Graphs**: Presence or absence of cycles
**Complete Graphs**: Every pair of vertices is connected by an edge.
## Tours
Many graph algorithms involve visiting every vertex/edge in the graph (analogous to a tree traversal).
- A tour is a path that visits every vertex exactly once.
- A **Hamiltonian** tour visits every vertex exactly once.
- A **Eulerian** tour visits every edge exactly once.
## Paths
A path is a sequence of vertices $v_{1},v_{2},v_{N} ~\text{Where}(v_{i}v_{i+1}\in E$ for $i \le i \lt N$
Path length is the number of edges in the path.
A simple path contains distinct vertices, except the first and last may be the same.
## Cycles
A Cycle is a path that starts and end at the same vertex.
A graph with no cycles is acyclic
A directed acyclic graph (DAG) has no cycles.
## Components
A graph is connected if there is a path between every pair of vertices.
A connected component  is a **subgraph** where every **pair** of vertices have a path between them.
A strongly connected component is a subgraph where every pair of vertices have a directed path between them.
## Graph Representations
We know that graphs can be used to represent many real-world phenomena. How can we design a graph ADT which is efficient and easy to use?

Graphs ADTs are similar to trees in that we need to store more information about nodes and edges. We have the following common ways to represent graphs
- Adjacency matrix
- Adjacency list
- Edge list
- Using explicit node and edge classes
## Adjacency matrix
Uses a $n \times n$ matrix, where $n$ is number of vertices
![[Pasted image 20260203134903.png]]
$A[i][j]=1$ if there is a edge between $i$ and $j$, otherwise 0.
Suitable for dense graph - why?


**Question**: What is the time complexity of checking if there is between two vertices in an adjacency matrix.
$O(1)$

**Question**: What is the space complexity of an adjacency matrix?
$O(n^{2})$. We can see that if we are mostly storing0s (i.e. if the graph is *sparse*), this is not very space efficient.

## Adjacency list
Uses an array of lists where each index represents a vertex.
Each vertex stores a list of its adjacent vertices.
More suitable for sparse graphs since you only store the edges that are present.
![[Pasted image 20260203135143.png]]

**Question**: What is the time complexity of checking if there is an edge between two vertices in a adjacency list?
$O(V)$, since we have to search through the list of adjacent vertices.

**Question**: What is space complexity of an adjacency matrix?
$O(V+E)$. This is more space efficient than an adjacency matrix for sparse graphs.
## Choosing a graph Representation
![[Pasted image 20260203135429.png]]
## Applications of Graphs
- Neural Networks
	![[Pasted image 20260203134600.png]]
- Bayesian Networks
	![[Pasted image 20260203134553.png]]
- PageRank for web search
	![[Pasted image 20260203134544.png]]
# 6 Degrees of Separation Between Any Two Individuals
The idea that any two people in the world are connected by at most 6 acquaintances.
This can be represented as a graph where each person is a *vertex* and each acquaintance is an edge.
This is a special case of a 'small-world network'.

>**Idea**: If I know 30 people, and each of those know 30 other people, and so on, how many people can I reach in 6 steps by asking my friends to mail their friends (and so on?)
>
	**Answer**: $30^{6}\approx 7.8 \times 10^{9}$
## Erdos Number
**Paul Erdos** was a Hungarian Mathematcician who collaborated with amny other mathematicisans. The Erdos number is a measure of how closely a mathematician is connected to Erdos.
![[Pasted image 20260203135824.png]]

# Graph Sorting And Searching
## Topological Sort
topological Sort is a way to order the vertices of a graph such that if there is a path from $v_{i}$ to $v_{j}$ appears after $v_{i}$.
>Example: course prequisites.
>![[Pasted image 20260203140054.png]]

A directed edge *v*,*w* indicates that *v* must be completed before course *w* may be attempted. The toplogical ordering makes it easy to understand the graph structure.
### Steps
1. Find a vertex with no **incoming** edges.
2. 'Visit' the vertex and remove it from teh graph along with its edges.
3. Repeat until all vertices are removed.

>Example: 
![[Pasted image 20260203140320.png]]
There is only one vertex with no incoming edges: $v_{1}$. We note it down as being 'top' of the hierarchy and remove it from the graph.
>
Next we can see that $v_{2}$ has no incoming edges. We note it down being next in the hierarchy and remove it from the graph.
>
Next we can see that $v_{5}$ has no incoming edges. We note it down as being next in the hierarchy and remove it from the graph.
>
We continue and see that the two following sequences are valid topological sorts.
$V_{1}$,$V_{2}$,$V_{5}$,$V_{4}$,$V_{3}$,$V_{7}$,$V_{6}$
$V_{1}$,$V_{2}$,$V_{5}$,$V_{4}$,$V_{7}$,$V_{3}$,$V_{6}$

## Pseudocode
We can see that we need to compute incoming edges. We can store this in our graph data structure in attribute called `in_degree`
```pseudocode
void topsort() throws CycleFoundException {
	for(int counter=0; counter<NUM_VERTICES; counter++){
		Vertex v = findNewVertexOfIndegreeZero();
		
		if(v==null){
			throw new CycleFoundException();
		}

		v.topNum = counter;
		
		for(each Vertex w adjacent to v){
			w.indegree--;
		}
	}
}
```
## Sort Analysis
Because of `findNewVertexOfIn`-`degreeZero` is a simple sequential scan of the array of vertices, each call to it takes $O(|{V}|)$ time.
Since there are $|V|$ such calls, the running time of the algorithm is $O(|V|^{2})$
But we know that if the graph is sparse, relatively few vertices will have their in-degree updated.

So, to improve the runtime, we can set aside all of the unassigned vertices with in-degree equal to zero
The easiest way to do this is using stack or queue.
## More Efficient Topological Sort Algorithm
1. Compute the in-degree of all nodes
2. Add the vertices with in-degree 0 to a queue.
3. While the queue is not empty:
	1. Remove the next vertex v
	2. Decrement in-degree of its adjacent vertices.te the in-degree of all nodes.
	3. Add any adjacent vertices to queue if their in-degree become 0.dd the vertices with in-degree 0 to a queue.
### Pseudocode
```Pseudocode
void topsort() throws CycleFoundException {
	Queue<Vertex> q = new Queue<Vertex>();
	int counter = 0;
	
	for (each Vertex v){
		if (v.indegree == 0){
			q.enqueue(v);
		}
	}
	
	while (!q.isEmpty()){
		Vertex v= q.dequeue();
		v.topNum = ++counter; //Assign Next number
		
			for (each Vertex w adjacent to v){
				if (--w.indegree == 0) {q.enqueue(w);}
			}
		if (counter != NUM_VERTICES){
		throw new CycleFound Exception();
		}
	}
}
```
![[Pasted image 20260203141717.png]]
### Analysis
The running time of this algorithm is $O(|V|+ |E|)$, where $|V|$ is the number of vertices and $|E|$ is the number of edges.
This is because each vertex is added to the queue once and each edge is examined once.
# Shortest path algorithms
**Motivation**: Shortest path algorithms are used to find the most efficient route between two points in a graph. They are used in a variety of applications, such as:
- GPS navigation systems
- Network routing protocols.
- Game AI pathfinding.

### Single-Source Shortest-Path Problem
The single-source shortest-path problem asks us to find the shortest path from one source to every other vertex in the graph. In more specific terms:
- **Input**: A weighted graph $G=(V,E)$ and a source vertex $s$
- **Each edge ($v_{i}$,$v_{j}$)** has a weighted/cost $c_{i,j}$
- **Goal**: Find the shortest weighted path from $s$ to every other vertex in $G$
- **Cost of a Path**: $\sum c_{i,i+1}$

>**A Tangible Example**
>In the case of a road network, the vertices are intersections and edges are roads. The weights could represent distance, time, or any other metric. The shortest path algorithm would help us find the quickest route from one intersection to another

## Unweighted Shortest paths (BFS)
>We can easily see that if all edge weights are equal, the shortest path is the one with the fewest edges. This is known as the unweighted shortest path problem. The solution to this problem is **Breadth-First Search** (BFS). BFS is analogous to level-order search in trees- we explore the graph 'layer by layer'. The shorts path to each vertex in the graph is simply found by keeping track of what 'layer' we are on when exploring each node.

>We need to be a bit careful, however. In contrast to trees, graphs can have cycles. If we don't keep track of which nodes we have visited, we can end up in an infinite loop 
>(This is illustrated in the graph below where we'd go 
>$v_{3}$->$v_{1}$->$v_{4}$->$v_{3})

>So we can see that we need to keep track of which nodes we have visited. We can do this by marking each node as visited. We can also keep track of the distance from the source to each node:
>![[Pasted image 20260203143103.png]]

### Steps
1. We will record the distance from $s$ in the entry $d_{v}$. 
	- These are initialized as $\infty$ and updated when we find a shorter path.
2. We will use variable *known* to indicate if we have visited the node.
	- Remember that we need this to avoid infinite loops.
3. When a vertex is marked as *known*, we have a guarantee than no cheaper path will ever be found, and so processing for that vertex is essentially complete.
4. We record $p_{v}$ to keep track of the shortest path to reach the vertex

### Pseudocode
```pseudocode
void unweighted(Vertex s){
	Queue<Vertex> q = new Queue<Vertex>();
	
	for (each Vertex v){
		v.dist = INFINITY;
	}
	
	s.dist = 0;
	q.equeue(s);
	
	while (!q.isEmpty()){
		Vertex v = q.dequeue();
		
		for (each Vertex w adjacent to v){
			if (w.dist == INIFITY){
				w.dist = v.dist + 1;
				w.path = v;
				q.enqueue(w);
			}
		}
	}
}
```
### Analysis
We can see how BFS finds shortest path in an **unweighted graph** by examining our example. As we explore layer by layer, we see that there are 2 problems that could occur:
1. The first is infinite looping due to a cycle. We have resolved this by keeping track of *known* (visited) nodes.
2. The second is that we updated a node to have a longer path once we visit it for a second time. We avoid this by have a `!v.known` condition within our for loop to prevent repeated visits.

>Before analyzing the runtime of this algorithm, we can note that it’s in jeopardy of suffering from the same issue as topological sort where we examine nodes that we know won’t have any bearing on the current work being done. 
>To avoid this, we perform the same optimization where instead of iterating over all nodes, we only iterate over those which are adjacent to the ones at the current ’level’. We use a queue to manage these node
>![[Pasted image 20260203143941.png]]
>![[Pasted image 20260203143941.png]]


**Question**: Why is the unweighted graph shortest path problem a special case of the weight graph shortest path problem

In a weighted graph, the shortest path is not necessarily the one with the fewest edges (why?).
We need to consider the weights of edges to find the shortest path.
The shortest path may involve more edges if the total weight is lower.
## Weighted Shortest path (Dijkstra)
>**A Tangible Example**
>In the case of a road network, the vertices are intersections and edges are roads. The weights could represent distance, time, or any other metric. The shortest path algorithm would help us find the quickest route from one intersection to another

>We can see in the graph below that running a breadth-first search from node $v_{1}$ would erroneously tell us that the shortest path to $v_{6}$ would be ($v_{1}\text{->}v_{4}\text{->}v_{6}$) when in fact the shortest path is ($v_{1}$ -> $v_{4}$ -> $v_{7}$ -> $v_{6}$)
![[Pasted image 20260203144620.png]]

### Updating BFS for Weighted Shortest Paths
We can update our BFS algorithm to handle weighted graphs by considering the weights of edges. We will need to keep track of the total weight of the path to each node to compute the shortest path.

**Key observation reiterated**: We want the algorithm to perform in a similar manner, but we know that we might need to update the shortest path to a node if we subsequently find a shorter path. The shortest path may involve more edges if the total weight is lower.

As it turns out, we can implement a greedy algorithm which is guaranteed to find the shortest path in a weighted graph. This algorithm is known as Dijkstra's Algorithm. We will see why it finds the best solution when studying at heuristic searches. The **key changes** from BFS are as follows:
1. With BFS, we know that once we've visited a node, we have found the shortest path. Because edges can have different weights, we now can visit the same node multiple times when a shorter path is found.
2. We want to explore the 'frontier' nodes in order of their weight (we'll see why shortly) so need to use a priority queue to achieve this.
## Understanding Dijkstra's Algorithm
We can see from the following diagam that by using a priority queue, we are repeatedly exploring unexplored nodes which minimize the following expresssion:
$\pi(w) = \min_{(v,w):v \in S} \pi(v) + c(v, w)$

![[Pasted image 20260203145326.png]]
>i.e. the next node to explore is shortest path to some v in the explored part, following by a single edge e = (v,w). We can summarize by saying the algorithm decides whether or not it is a good idea to use $v$ on the shortest path to $w$

The priority queue is used to store the nodes in the frontier. The nodes are ordered by the weight of the path to reach them. We can see that the algorithm is greedy in that it always explores the node with the lowest weight first.
We see that when we explore a new node, if we have found a shorter path to it, we update the path. This is why we need to use a priority queue to ensure we explore the nodes in the correct order.
### Step-by-Step
Here we assume the start node is $v_{1}$. The priority queue is trivially $[(v_{1},0)$,$(v_{2},\inf)$,$(v_{3},\inf)$,$(v_{4},\inf)$,$(v_{5},\inf)$,$(v_{6},\inf)$,$(v_{7},\inf)]$. $v_{1}$ will be popped from the queue and marked as known, and its neighbors, $v_{2}$ and $v_{4}$ will be updated to have values of $d_{v}$ of 2 and 1 respectively
![[Pasted image 20260203145951.png]]

The priority queue now looks like:
\[($V_{4}$,1),($V_{2}$,2),($V_{3}$,inf),($V_{6}$,inf),($V_{7}$,inf)]. $v_{4}$ will be removed from the queue, marked as known and its neighbors will be updated:
1. $v_{2}$: $d(v_{2}) =$ min(2,1+3) = 2 (no change)
2. $v_{3}$: $d(v_{3}) =$ 1 + 2 = 3
3. $v_{3}$: $d(v_{3}) =$ 1 + 2 = 3
4. $v_{4}$: $d(v_{4}) =$ 1 + 8 = 9
5. $v_{5}$: $d(v_{5}) =$ 1 + 4 = 5 5 5 5 5

Priority queue now looks like: 
\[($V_{4}$,1),($V_{2}$,2),($V_{3}$,inf),($V_{6}$,inf),($V_{7}$,inf)]. $v_{4}$ will be removed from the queue, marked as known and its neighbors will be updated:
## Graph Search Algorithms
### Breadth-first
### Depth-First Search
