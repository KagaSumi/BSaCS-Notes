# Introduction to Trees
Definitions:
**Tree**: A connected, acyclic graph where any two nodes are connected by exactly one path
**Root**: The topmost node of the tree, serving as the starting point.
**Edge**: A connection between two nodes
**Leaf Node**: A node with no children (degree 0)
**Internal Node**: A node with at least one child.
**Path** : A sequence of nodes such that each node is adjacent to the next node in the sequence
**Height of Tree**: The number of edges on the longest path from the root to a leaf.
**Depth**: The Depth of a node is the number of edges on the path from the root to the node.
**Level**: The level a node is on is determined by the number of edges on the path from the root to the node i.e. its depth
**Sibling**: Two nodes with the same parent
**Ancestor**A node *v* is an ancestor of a node *w* if *v* is in the path from the root to *w*.
**Descendant**: A node *w* is a descendant of a node *v* if *v* is in path from the root to *w*
**Subtree**: A tree consisting of a node and all its descendants.
**Binary Tree**: A tree where each node has at most two children.
## Tree ADT
ADT stands as **abstract data type** - a set of abstract objects representing data items with a collection of operations that can be performed on them

Here are some methods we should consider for the tree ADT:
- The tree ADT is a collection of nodes that are connected in a hierarchical structure
- How should we design this ADT to be useful? What should the interface look like?
### Functions
- getRoot()
- isEmpty()
- size()
- height()
- addChild(parent,child)
- removeChild(parent,child)

### Questions
How do we find the height of the tree?
> We need to figure out the length of every path from the root to a leaf node. The height is the length of the longest path
## Tree Traversal
A **tree traversal** is the process of visiting each node in a tree exactly once.
### Level Order Traversal/In Order Traversal (LrR)

Traverse the tree level by level. Once we run out of nodes to explore we have found the height of the tree. 

#### Code
```pseudocode
function LevelOrderTraversal(root)
	queue <- new Queue
	queue.enqueue(root)
	while queue is not empty do 
		node <- queue.dequeue()
		visi(node)
		for each child of node do
			queue.enqueue(child)
		end for
	end while
end function
```
Big-O Complexity of $O(n)$ 
### Pre-order Traversal (rLR)
Recursively visit children from left to right
#### Code (Stack)
```psueudocode
function preOrderTraversal(root)
	stack <- new Stack
	stack.push(root)
	while stack is not empty do
		node <- stack.pop()
		visit(node)
		for each child of a node do // Assume iterator gives 
			stack.push(child)       // right to left
		end for
	end while
end function
```


#### Code (Recursive)
```psuedocode
function preOrderTraversal(root)
	if root is null then
		return
	end if
	visit(root)
	for each child of root do
		preOrderTraversal(child)
	end for
end function
```
Big-O is $O(n)$ because it visit all nodes
### Post-Order Traversal (LRr)
For post-order traversal, nodes are visited in left -> right -> root
#### Code
Can refer to Pre-Order Traversal just change iterator to go left to right

## Revisiting Tree height
**Question**: We've seen different traversing trees. Can we use one of these algorithms to determine tree height?

> Yes! We can use the level order traversal algorithm to determine the height of the tree. The height of the tree is the number of levels int eh tree. We can use the level order traversal algorithm to determine the number of levels in the tree.
### Code
```psuedocode
function Height(root)
	queue <- new Queue
	queue.enqueue(root)
	height <- ()
	while queue isn ot empty do
		size <- queue.size()
		for i <- () to size do 
			node <- queue.dequeue()
			for each child of node do
				queue.enqueue(child)
			end for
		end for
		height <- height + 1
	end while
	return height
end function
```
## Sample Application of Tree Traversal
We know that file system contains folders nad files. Each folder can also have subfolders. We can represent the file system as a tree. Can we use tree traversals to list all the files in the system?
# Binary Trees
A binary tree is a tree in which no node can have more than two children.

## Why are we interested in Binary Trees?
Binary trees are a fundamental data structure used in many applicatoins:
- Binary Search Trees
- Expression trees
- Huffman Trees
- AVL trees
## Implementation
```java
class BinaryNode<T>{
	//Friendly data; accessible by other package routines
	T element; //Data stored in node
	BinaryNode<T> left; //Left child
	BinaryNode<T> right; //Right child
}
```

**Question**: We've already come across binary search. Why don't we use ternary/quaternary/quintenary search instead?

> The time complexity of binary search is O(h) where h is height of the tree. The height of a binary search tree is O(log n) where n is the number of nodes in the tree. This is the best time complexity we can achieve for searching in a tree.

**Question**: Why don't we just use a sorted array instead of a binary search tree>

>Insertion and deletion in a sorted array are O(n) operations

**Question**: Can 2 different binary search trees have different structure but represent the same data?
> Yes

## Search Procedure
```pseudocode
function search(root,value)
	if root is null the
		return false
	end if
	if value is equal to root.value then
		return true
	end if
	if value is less than root.value then
		return search(root.left,value)
	else
		return search(root.right,value)
	end if
end function
```
Big-O:
Worst case will be if we don't find the search target so it will drill down as far as O(h)

**Question**: is there a way that we can minimize h?
We'll cover next week


## Implementation (cont.)
In order to implement the binary search tree, we need to be able to 
1. Insert a node
2. Delete a node
3. Search for a node
### Insertion
```pseudocode
function insert(root,value)
	if root is null then
		return neww Node(value)
	end if
	if value is less than root.value then
		root.left <-insert(root.left, value)
	else
		root.right <- insert(root.right, value)	
	end if
	return root
end function
```
### Deletion
Let's break it down into the tree cases:
1. The node to be deleted is a leaf node
2. The node to be deleted has one child
3. The node to be deleted has two children

#### Case 1: leaf node
If the node to be deleted is a leaf node, we can simply remove it from the tree.
#### Case 2: one child node
If the node to be deleted has one child, the node can be deleted after its parent adjusts a link to bypass a node.
![[Pasted image 20260120141304.png]]
#### Case 3: two child node
If the node to be deleted has 2 children, the general strategy is to replace the data of this node with the **smallest** data of the right subtree (which is easily found). 
![[Pasted image 20260120141523.png]]

We know this choice will preserve the property that all nodes in the right subtree must be bigger than the root. So replacing the root (which we're deleting) with the next smallest node is safe. 

The node whose data we used as a replacement must then be recursively deleted. Because the  the smallest node in the right subtree cannot have a left child, the second remove is an easy one.