---
layout: post
title: BlackhatMEA2024 Trypanophobia Writeup
categories:
  - BlackhatMEA2024
  - Crypto
---

## Solution:

for this challenge we were given the following code

first we have the update function
```py
def update(self):
    self.public['n'] = 1
    self.private['f'] = 1
    for p in self.private['p']:
        self.public['n'] *= p
        self.private['f'] *= (p - 1)
    self.private['d'] = inverse(self.public['e'], self.private['f'])

    print('n: ', self.public['n'])
```
this calculate the new key, for the new primes we provide to it

then we have the hash function
```py
def pad(self, x):
    #print('p:', self.private['p'])
    print(str(set(self.private['p'])).encode())
    y = int(hashlib.sha256(str(set(self.private['p'])).encode()).hexdigest(), 16)
    #print('y: ', y)
    while x < self.public['n']:
        x *= y
    x //= y
        
    return x
```
in this pad function we notice that if we send the same primes twice we get the same y, keeping in mind this information we can solve y, for the rest of the values of p

as length of n is 2048 bits, while the `while` loops run, where y is always 256 bits or 32 bytes, so the padded msg becomes
`pad(x) = x * y^k, as 256*8 = 2048, and depending in the length of the flag itself, we can say that the value of k is somewhat between ~5-10


now if we add the key, the key pool becomes something like this n = `[P,Q,p,p]`, and pad will be `[P,Q,p]` now if we add the key again, now the pool is
[P,Q,p,p,p,p] and will be be [P,Q,p], `y` will be fixed, now to the encryption part

`C1 = x*y1^(8+k)^e mod (n*p*p)`
`C2 = x*y1^(16+k)^e mod (n*p*p*p*p)`

`8+k` because now the length of n is 2048+2048 bits, similar for `16+k`

we can simplify the given problem 


`C1 = x*y1^(8+k)^e mod (p)`
`C2 = x*y1^(16+k)^e mod (p)`

We can now decrypt both $C{1}’$ and $C{2}’$ using $ϕ=p-1$ to get$$ M1 and M2


if we divide m2 with m1 we get y^8, then we can calculate the 8th root to get the padded value `y1` 
Once we get y1 we can get `x = m1/(y^k+8) mod p`, now we can bruteforce k from 5-10 to get the x

