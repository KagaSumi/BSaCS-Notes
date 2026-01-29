# Vector
A Mathematicla vector can be represented in 2D, or 3D space
- 2D: x,y coordinate
- 3D: x,y,z coordinate


The best way to visualize a vector is to picture an arrow (start from 0,0)

Vector has a direction and a magnitude (length)
	Direction is represented by the location of hte point 
## Example
![[Pasted image 20260128113347.png]]
To Calculate the length we use Pythagoreans theorem
$c = \sqrt{(a^{2}+b^{2})}$

$c = \sqrt{(3^{2}+4^{2})}$
$c = \sqrt{(9+16)}$
$c = \sqrt{(25)}$
$c = 5$

Definitions
**Position**: The coordinates of a vector represent where an entity is located in the game world or window
**Direction**: A vector can show which way an entity is facing or moving toward (though it doesn't have to stop at that point)
**Velocity**: Combines a direction with speed, showing not just where the entity is headed, but how fast it's moving
# Normalizing
$v = (\frac{x}{\text{length}},\frac{y}{\text{length}})$
![[Pasted image 20260128113742.png]]

With a normalized vector you can apply speed as a constant multiplier, and it would make vector length equal to the speed.