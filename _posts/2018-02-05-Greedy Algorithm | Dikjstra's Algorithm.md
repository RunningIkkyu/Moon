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
In *Dijkstra's Algorithm*, we maintain two sets, one sets(we call it set **Q**) contains nodes included in shortest path, the other set includes nodes not yet included in shortest path.At every step of the Algorithm, we'll find a node which is not in set **Q** and has minimum distance from source node.

## Algorithm
1. Create a set sptSet (shortest path tree set) that keeps track of vertices included in shortest path tree, i.e., whose minimum distance from source is calculated and finalized. Initially, this set is empty.
2. Assign a distance value to all vertices in the input graph. Initialize all distance values as INFINITE. Assign distance value as 0 for the source vertex so that it is picked first.
3. While sptSet doesn’t include all vertices  
    a) Pick a vertex u which is not there in sptSetand has minimum distance value.  
    b) Add u to sptSet  
    c) Update distance value of all adjacent vertices of u. To update the distance values, iterate through all adjacent vertices. For every adjacent vertex v, if sum of distance value of u (from source) and weight of edge u-v, is less than the distance value of v, then update the distance value of v.


