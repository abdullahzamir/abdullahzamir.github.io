---
layout: post
title: UIUCTF X Marked the Spot writeup
categories:
  - UIUCTF
  - Crypto
---

#### Given:
For the challenge we were given and encrypted file and the encryption algorithm 

```python
from itertools import cycle

flag = b"uiuctf{????????????????????????????????????????}"
# len(flag) = 48
key  = b"????????"
# len(key) = 8
ct = bytes(x ^ y for x, y in zip(flag, cycle(key)))

with open("ct", "wb") as ct_file:
    ct_file.write(ct)

```

This is simple XOR, and we can retrieve the key using the association property of the XOR operation
as we know some part of the plaintext, which is `uiuctf` and key is ok 8 charaters, to get the full key we only need to bruteforce one character

#### Solve Script:

```python

from itertools import cycle
from pwn import xor 


f = open('ct','rb')
flag = f.read()

pt = bytes.fromhex("uiuctf{".encode().hex())

key = xor(flag[:7],pt)

for i in range(0xff):
    key = key + bytes([i])
    pt = xor(flag,key)
    if b'uiuctf{' in pt:
        if b'}' in pt[len(pt)-1:]:
            print(pt)
    key = key[:-1]
```


flag:
`uiuctf{n0t_ju5t_th3_st4rt_but_4l50_th3_3nd!!!!!}`
