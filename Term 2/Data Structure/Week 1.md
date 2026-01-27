**Time Complexity** - An analysis of the **time required** to solve a problem of a **particular size**.
**Space Complexity** - An analysis of the computer memory required to solve the problems


# Calculations
If/Else - Treat worst case scenario as the one to happen all of the time

```
sum = 0;
for (i =1; i < n; i++){
	for(j = i ; j < i + i ; j++){
		for (k = 1; k <j; k++){
			sum ++
		}
	}
}
```
$\sum_{i=1}^{n}(\sum_{j=1}^{2i}(\sum_{k=1}^{j}1)$


$\sum_{k=1}^{j}1 = (j-1)*1 = j-1$
$\sum_{j=1}^{2i-1}j-1 = \sum_{j=1}^{2i-1}j - \sum_{j-1}^{2i-1} 1$
Using $\sum_{k=1}^{n}k = \frac{n(n+1)}{2}$
$\sum_{j=1}^{2i-1}j = \frac{4i^2-2i}{2}$
$\frac{4i^{2}-2i}{2}-2i+1$

Last Sum:
$\sum_{i=1}^{n}\frac{4i^{2}-2i-4i+2}{2}$

$=\frac{1}{2}*(4*\sum_{i=1}^{n}i^{2} -6\sum_{i=1)}^{n}i + \sum_{i=1}^{n}2)$
can use 
$\sum_{k=1}^{n}k^2 = \frac{n(n+1)(2n+1)}{6}$

In the end
$2(\frac{n^{3}}{3}+\frac{n^{2}}{2}+\frac{n}{6})+n$
it is a polynomial of degree 3, so we know it will be O($n^{3}$)

