# AVL Trees
Self-Balancing trees, where the difference between heights of left and right subtrees for any nodes cannot be more than one.

$\text{Balance Factor} = \text{Left Subtree Height} - \text{Right subtree Height}$
For a balanced tree (For every node): -1 <= Balance Factor <= 1 

## AVL Trees Background
Applications, where insertion and deletions are less common but frequent data lookups along with other operations of BST like sorted traversal, floor, ceil, min and max.

AVL Trees can be used in a real time environment where predictable and consistent performance is required.
## Minimum Number of Nodes in a Balanced Tree
$N(h) = N(h-1) +N(h-2)+1$
N = Number of nodes in sub tree height (x)

## Rotation
Rotations are designed to restore balance in $O(1)$ time while ensuring the overall time complexity remains $O(log n)$ AVL uses **four** cases to rebalance themselves after insertions and deletion:
- Left-Left
- Right-Right
- Left-Right
- Right-Left
### Single Rotations
#### Left-Left
Occurs when a node is inserted into the left subtree of the left child causing the balance factor to become **more than +1**

Fix: Perform a single **right** rotation
![[Pasted image 20260127134632.png]]
![[Pasted image 20260127134645.png]]
![[Pasted image 20260127134657.png]]
#### Right-Right
Occurs when a node is inserted into the right subtree of this right child, making the balance factor **less than -1**

Fix: Perform a single **left** rotation

![[Pasted image 20260127134742.png]]
![[Pasted image 20260127134750.png]]
![[Pasted image 20260127134757.png]]
### Double Rotations
#### Left-Right
Occurs when a node is inserted into the **right subtree** of the **left child** which disturbs the balance factor of an ancestor node, making it **left-heavy**

Fix: Perform a Left Rotation on the left child, followed by a right rotation on the node.
![[Pasted image 20260127134908.png]]
![[Pasted image 20260127134916.png]]
![[Pasted image 20260127134924.png]]
![[Pasted image 20260127134932.png]]
![[Pasted image 20260127134940.png]]
#### Right-Left
Occurs when a node is inserted into the **left subtree** of the **right child**, which disturbs the balance factor of an ancestor node, making it **right-heavy**

Fix: Perform a right rotation on the right child, followed a left rotation on the node.
![[Pasted image 20260127135038.png]]
![[Pasted image 20260127135046.png]]
![[Pasted image 20260127135052.png]]
![[Pasted image 20260127135105.png]]
![[Pasted image 20260127135112.png]]
## Deletion
To make sure that the given tree remains AVL after every deletion, we must augment the standard BST delete operation to perform some re-balancing. Folowing are two basic operations that can be performed to re-balance a BST without violating the BST property L < r < R
![[Pasted image 20260127135600.png]]
1. Left Rotation
2. Right Rotation
### Example
![[Pasted image 20260127135616.png]]
![[Pasted image 20260127135652.png]]
![[Pasted image 20260127135704.png]]
![[Pasted image 20260127135715.png]]
![[Pasted image 20260127135723.png]]
![[Pasted image 20260127135731.png]]
# Insertion Summary
## Example:
>In this example we have just inserted the 13 node

![[Pasted image 20260127142811.png]]
![[Pasted image 20260127142856.png]]

# Deletion Summary
# Time Complexity
In summary AVL trees will have the same average and worst case scenario of 
$O(log(n))$ run time for any operation

Space Complexity: $O(n)$
# Worked Examples

# Resources
[AVL Tree Data Structure](https://www.geeksforgeeks.org/dsa/introduction-to-avl-tree/)
[Deletion in an AVL Tree](https://www.geeksforgeeks.org/dsa/deletion-in-an-avl-tree/)
[Insertion in a AVL Tree](https://www.geeksforgeeks.org/dsa/insertion-in-an-avl-tree/)
[AVL Tree Visualizer](https://www.cs.usfca.edu/~galles/visualization/AVLtree.html)