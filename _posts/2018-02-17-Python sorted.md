---
layout: post
title:  "Python sorted function"
date:   2018-02-17
excerpt: "How to sort a list of tuple by the second element?"
tag:
- python
comments: true
---

# Python sorted()

By giving para *key*, we can sort a list of tuple by the n-th element in python. 

## Examples

```python
import operator
stu=[('jhon', 'a', 15), ('jane', 'b', 12), ('save', 'b', 10)]  
sorted(stu, key=operator.itemgetter(2))  
```

```python
[('save', 'b', 10), ('jane', 'b', 12), ('jhon', 'a', 15)]
```
