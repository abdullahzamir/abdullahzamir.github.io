---
layout: post
title:  "Quadratic Residue Cryptohack Writeup"
---


##### Given:
Find the quadratic residue and then calculate its square root. Of the two possible roots, submit the smaller one as the flag.
```
p = 29
ints = [14, 6, 11]
```

##### solution
```python
from math import *
p = 29
ints = [14,6,11]


for i in ints:
	for j in range(1,p):
		if i == j**2 % 29:
			print(j**2 % 29) 

print("")
for a in range(1,29):
	if a**2 % 29 == 6:
		print(a)

## ans: 8
```

###### Explanation:
```python
for i in ints:
	for j in range(1,p):
		if i == j**2 % 29:
			print(j**2 % 29)  
```
consider p = 7
as we know a^2 = x mod 7 
then
```
1^2 = 1 mod 7
2^2 = 4 mod 7
3^2 = 9 = 2 mod 7
```
here 1,4,9 are known as quadratic residues

running this part of the program returns 6 as an quadratic residue 

now to find a  
```python
for a in range(1,29):
	if a**2 % 29 == 6:
		print(a)
```
in simple english 
find a such that a^2 mod 29 is equal to 6  
a^2 =(congruent) 6 mod 29 or 
a^2 mod 29 = 6 mod 29 or
a^2 mod 29 = 6

we get 8,21
8^2 mod 29 = 6
Ans: 8 (smallest)

--- 