---
layout: post
title:  "A Beautiful Class Counter in Python"
date:   2018-02-24
excerpt: ""
tag:
- Python
- Counter
comments: true
---

There's a *get()* function of dictionary type in python return the value of given key, and return default value if the key not in this dictionary.

```python
dict.get(key, default=None)
```

Here's an example of classCounter.

```python
tmplist = ['A', 'A', 'B', 'C', 'D', 'C', 'C', 'E', 'G']

classCount = {}
for i in tmplist:
    classCount[i] = classCount.get(i, 0) + 1
    
```
