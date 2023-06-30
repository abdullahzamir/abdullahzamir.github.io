
---
layout: post
title:  "BSidesTLV 2023 Passino Writeup"
categories: [BSidesTLV, Hardware]
---

Given File:

```cpp
int message[] = {1, 1, 1, 7, 8, 3, 4, 1, 2, 3, 8, 6, 5, 1, 2, 7, 8, 4, 5, 1, 2, 3, 8, 4, 5, 1, 2, 7, 6, 5, 8, 4, 1, 8, 7, 2, 3, 4, 1, 2, 7, 6, 5, 8, 4, 1, 7, 8, 3, 4, 1, 2, 7, 6, 5, 8, 4, 1, 2, 7, 8, 4, 5, 1, 2, 3, 4, 1, 2, 3, 8, 4, 5, 1, 2, 7, 8, 4, 5, 1, 7, 8, 3, 4, 1, 7, 8, 3, 4, 1, 2, 7, 6, 5, 1, 2, 7, 8, 4, 5, 1, 2, 7, 6, 5, 8, 4, 1, 2, 3, 8, 4, 5, 1, 2, 3, 8, 6, 5, 1, 2, 3, 8, 4, 5, 1, 2, 3, 4, 5, 6, 7, 1, 2, 3, 8, 4, 5, 1, 2, 3, 8, 6, 5, 1, 2, 3, 8, 4, 5, 1, 2, 3, 8, 4, 5, 1, 2, 3, 4, 1, 7, 6, 8, 4, 5, 1, 2, 7, 6, 5, 8, 4, 1, 2, 3, 4, 5, 6, 7, 8, 1, 2, 3, 8, 4, 5, 1, 7, 8, 3, 4, 1, 2, 7, 6, 5, 8, 4, 1, 7, 6, 1, 2, 3, 4, 1, 2, 3, 8, 6, 5, 1, 2, 7, 8, 4, 5, 1, 2, 3, 4, 1, 2, 7, 6, 5, 8, 4, 1, 2, 7, 8, 6, 1, 2, 3, 4, 1, 2, 3, 8, 6, 5, 1, 2, 7, 6, 5, 8, 4, 1, 7, 6, 8, 4, 5, 1, 7, 8, 3, 4, 1, 7, 6, 1, 2, 7, 6, 5, 8, 4, 1, 2, 7, 8, 6, 5, 1, 2, 7, 6, 5, 8, 4, 1, 7, 8, 3, 4, 1, 7, 8, 3, 4, 1, 2, 3, 4, 5, 6, 7, 8, 1, 2, 3, 8, 4, 5, 1, 7, 8, 3, 4, 1, 2, 3, 4, 1, 2, 3, 8, 6, 5, 1, 2, 7, 6, 5, 8, 4, 1, 7, 8, 3, 4, 1, 2, 3, 4, 1, 2, 3, 4, 1, 2, 7, 6, 5, 8, 4, 1, 7, 6, 1, 2, 3, 4, 1, 2, 3, 8, 6, 5, 1, 2, 3, 8, 4, 5, 1, 2, 3, 8, 4, 5, 1, 7, 8, 3, 4, 1, 2, 3, 8, 6, 5, 1, 2, 3, 8, 4, 5, 1, 2, 3, 4, 5, 6, 7, 1, 2, 3, 4, 1, 7, 8, 3, 4, 1, 2, 7, 6, 5, 8, 4, 1, 2, 3, 4, 5, 6, 7, 8, 1, 7, 8, 3, 4, 1, 7, 6, 1, 2, 3, 4, 1, 2, 3, 8, 6, 5, 1, 2, 3, 8, 4, 5, 1, 2, 3, 8, 4, 5, 1, 7, 8, 3, 4, 1, 2, 7, 6, 5, 8, 4, 1, 2, 3, 4, 1, 2, 7, 8, 4, 5, 1, 2, 7, 6, 5, 8, 4, 1, 2, 7, 8, 6, 5, 1, 2, 7, 8, 4, 5, 1, 8, 7, 2, 3, 4, 1, 2, 7, 6, 5, 8, 4, 1, 7, 6, 1, 2, 3, 4, 1, 8, 7, 2, 3, 4, 1, 2, 7, 6, 5, 8, 4, 1, 7, 6, 1, 2, 3, 4, 1, 8, 7, 2, 3, 4, 1, 2, 3, 4, 1, 3, 4, 8, 6, 5, 1};
int msglen = sizeof(message) / 2 ;
int delaysec = 500;

// Set A-G, DP as OUTPUT pins, COM is 5V
void setup() { for(int i=2; i<=9;i++) pinMode(i, OUTPUT); }

void loop() { for (int i=0; i<msglen; i++) message[i] == 1 ? clean() : digitalWrite(message[i], LOW); }

void clean() { delay(delaysec); for(int i=2; i<=9;i++) digitalWrite(i, HIGH); delay(delaysec); }
```

### Solution:

> // Set A-G, DP as OUTPUT pins, COM is 5V

looking at this, this code appears to be of 7 segment display

we found an online arduino simulator
https://wokwi.com/projects/new/arduino-uno

paste the provided code 

![[Pasted image 20230630204033.png]]
add the seven segment display 

![[Pasted image 20230630204200.png]]

connect the wires

pin 2-8 connected to A-G on seven segments
2->A
3->B 
and so on

connect COM1 to 5V
![[Pasted image 20230630204519.png]]

Run the Simulation
and read the Hex characters displayed on the seven segment

![[Pasted image 20230630211006.png]]

output:
425369646573544c56323032337b68346172576f726b416e6448347264776172334230746841723346756e59617961797d

convert from hex

#### flag:
BSidesTLV2023{h4arWorkAndH4rdwar3B0thAr3FunYayay}