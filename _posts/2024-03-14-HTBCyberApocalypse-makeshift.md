---
layout: post
title: HTB CyberApocalypse Makeshift Writeup
categories:
  - HTB CyberApocalypse
  - Crypto
---

### Given:

source.py
```python
from secret import FLAG

flag = FLAG[::-1]
new_flag = ''

for i in range(0, len(flag), 3):
    new_flag += flag[i+1]
    new_flag += flag[i+2]
    new_flag += flag[i]

print(new_flag)

```

output.txt
```bash
!?}De!e3d_5n_nipaOw_3eTR3bt4{_THB
```

running the same program with the encrypted text gives us the flag

#### Solution:
```python

FLAG = "!?}De!e3d_5n_nipaOw_3eTR3bt4{_THB"
flag = FLAG[::-1]
new_flag = ''

for i in range(0, len(flag), 3):
    new_flag += flag[i+1]
    new_flag += flag[i+2]
    new_flag += flag[i]

print(new_flag)

```

### Flag:
HTB{4_b3tTeR_w3apOn_i5_n3edeD!?!}
