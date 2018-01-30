---
layout: post
title:  "float number formatting output in c++"
date:   2018-01-30
excerpt: "You can set precision by using setprecision() function provided by head file iomanip. So DO NOT forget to include iomanip before setting precision."
tag:
- C++
comments: false
---
You can set precision by using *setprecision()* function provided by head file **iomanip**. So **DO NOT** forget to include iomanip before setting precision.
```c
#include <iomanip>
```
*setprecision* always set significant figures by default.  If you want to accurate to *n*(n is a naturel number) decimal places, you have to setiosflags(ios::fixed) before. 
```c
float a = 123.456;
cout<<setiosflags(ios::fixed)<<setprecision(1)<<endl;    // 123.5
cout<<setiosflags(ios::fixed)<<setprecision(2)<<endl;    // 123.46
cout<<setiosflags(ios::fixed)<<setprecision(3)<<endl;    // 123.456
```
