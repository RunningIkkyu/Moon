---
layout: post
title:  "Converting int and string to each other in c++"
date:   2018-01-30
excerpt: "How to convert int to string , or, string to int in c++?"
tag:
- C++
comments: true
---

### convert int to string

```c
#inlude <sstream>
string int2string(int a){
    stringstream ss;
    ss<<a;
    return ss.str();
}
```

### conert string to int
```c
#include <sstream>
int strin2int(string s){
    stringstream ss;
    ss<<s;
    int a;
    ss>>a;
    return a;
}
```
