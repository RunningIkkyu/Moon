---
layout: post
title:  "Sort in decreasing order"
date:   2018-08-02
excerpt: "There is an convient way to sort sth without compare function."
tag:
- C++
comments: true
---
# Sort in decreasing order

Find an example on the c++ reference page.

```cpp
// greater example
#include <iostream>     // std::cout
#include <functional>   // std::greater
#include <algorithm>    // std::sort

int main () {
  int numbers[]={20,40,50,10,30};
  std::sort (numbers, numbers+5, std::greater<int>());
  for (int i=0; i<5; i++)
    std::cout << numbers[i] << ' ';
  std::cout << '\n';
  return 0;
}
```
