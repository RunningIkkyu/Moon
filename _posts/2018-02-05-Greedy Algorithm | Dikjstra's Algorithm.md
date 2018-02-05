---
layout: post
title:  "Greedy Algorithm | Dikjstra's Algorithm"
date:   2018-02-05
excerpt: "Given a graph and a source vertex in graph, find shortest paths from source to all vertices in the given graph"
tag:
- Greedy Algorithm
- Graph
comments: flase
---

# Greedy Algorithm | Dikjstra's Algorithm
*Dijkstra's Algorithm* is an algorithm for finding shortest paths between nodes in graph. For a given source node in the graph, the algorithm finds the shortest paths between that node and every other.  
In *Dijkstra's Algorithm*, we maintain two sets, one sets(we call it set **sptSet**) contains nodes included in shortest path, the other set includes nodes not yet included in shortest path.At every step of the Algorithm, we'll find a node which is not in set **sptSet** and has minimum distance from source node.

## Algorithm
1. Create a set sptSet (shortest path tree set) that keeps track of vertices included in shortest path tree, i.e., whose minimum distance from source is calculated and finalized. Initially, this set is empty.
2. Assign a distance value to all vertices in the input graph. Initialize all distance values as INFINITE. Assign distance value as 0 for the source vertex so that it is picked first.
3. While sptSet doesn’t include all vertices  
    a) Pick a vertex u which is not there in sptSetand has minimum distance value.  
    b) Add u to sptSet  
    c) Update distance value of all adjacent vertices of u. To update the distance values, iterate through all adjacent vertices. For every adjacent vertex v, if sum of distance value of u (from source) and weight of edge u-v, is less than the distance value of v, then update the distance value of v.

## Example
Let's understand the algorithm with this example:
![image](https://raw.githubusercontent.com/RunningIkkyu/runningikkyu.github.com/master/assets/img/Dijkstra-s%20Algorithm/2018-02-05-1.jpg)  
This is initial status, where INF indicates infinite :  

|sptSet|distance array|  
|-|-|  
|Empty|{0, INF, INF, INF, INF, INF, INF, INF, INF}|  
  
  
Now pick the vertex with minimum distance value. The vertex 0 is picked, include it in sptSet.So sptSet becomes {0}. After including 0 to sptSet, update distance values of its adjacent vertices. Adjacent vertices of 0 are 1 and 7. The distance values of 1 and 7 are updated as 4 and 8. Following subgraph shows vertices and their distance values, only the vertices with finite distance values are shown. The vertices included in sptSet are shown in green color.  

![image](https://raw.githubusercontent.com/RunningIkkyu/runningikkyu.github.com/master/assets/img/Dijkstra-s%20Algorithm/2018-02-05-2.jpg)    

|sptSet|distance array|  
|-|-|  
|{0}|{0, 4, INF, INF, INF, INF, INF, 8, INF}|  

Pick the vertex with minimum distance value and not included in sptSet. The vertex 1 is picked and added to sptSet. So sptSet now becomes {0, 1}. Update the distance values of adjacent vertices of 1. The distance value of vertex 2 becomes 12.  
![image](https://raw.githubusercontent.com/RunningIkkyu/runningikkyu.github.com/master/assets/img/Dijkstra-s%20Algorithm/2018-02-05-3.jpg)

|sptSet|distance array|  
|-|-|  
|{0, 1}|{0, 4, 12, INF, INF, INF, INF, 8, INF}|  
  
Pick the vertex with minimum distance value and not already included in sptSet. Vertex 7 is picked. So sptSet now becomes {0, 1, 7}. Update the distance values of adjacent vertices of 7. The distance value of vertex 6 and 8 becomes finite (15 and 9 respectively).  
![image](https://raw.githubusercontent.com/RunningIkkyu/runningikkyu.github.com/master/assets/img/Dijkstra-s%20Algorithm/2018-02-05-4.jpg)  
|sptSet|distance array|  
|-|-|  
|{0, 1, 7}|{0, 4, 12, INF, INF, 9, INF, 8, 15}|  
  
Pick the vertex with minimum distance value and not already included in sptSet. Vertex 6 is picked. So sptSet now becomes {0, 1, 7, 6}. Update the distance values of adjacent vertices of 6. The distance value of vertex 5 and 8 are updated.  
![image](https://raw.githubusercontent.com/RunningIkkyu/runningikkyu.github.com/master/assets/img/Dijkstra-s%20Algorithm/2018-02-05-5.jpg)  

|sptSet|distance array|  
|-|-|  
|{0, 1, 7, 6}|{0, 4, 12, INF, 11, 15, INF, 8, 15}|  
  
We repeat the above steps until sptSet doesn’t include all vertices of given graph. Finally, we get the following Shortest Path Tree (SPT).  
![img](https://raw.githubusercontent.com/RunningIkkyu/runningikkyu.github.com/master/assets/img/Dijkstra-s%20Algorithm/2018-02-05-6.jpg)  
