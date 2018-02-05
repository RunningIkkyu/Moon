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
1. Assign to every node a tentative distance value: set it to zero for our initial node and to infinity for all other nodes.
2. Set the initial node as current. Mark all other nodes unvisited. Create a set of all the unvisited nodes called the unvisited set.
3. For the current node, consider all of its neighbors and calculate their tentative distances. Compare the newly calculated tentative distance to the current assigned value and assign the smaller one. For example, if the current node A is marked with a distance of 6, and the edge connecting it with a neighbor B has length 2, then the distance to B (through A) will be 6 + 2 = 8. If B was previously marked with a distance greater than 8 then change it to 8. Otherwise, keep the current value.
4. When we are done considering all of the neighbors of the current node, mark the current node as visited and remove it from the unvisited set. A visited node will never be checked again.
5. If the destination node has been marked visited (when planning a route between two specific nodes) or if the smallest tentative distance among the nodes in the unvisited set is infinity (when planning a complete traversal; occurs when there is no connection between the initial node and remaining unvisited nodes), then stop. The algorithm has finished.
6. Otherwise, select the unvisited node that is marked with the smallest tentative distance, set it as the new "current node", and go back to step 3.

## Pseudocode
```c/c++
function Dijkstra(Graph, source):

create vertex set Q
    for each vertex v in Graph:             // Initialization
        dist[v] ← INFINITY                  // Unknown distance from source to v
        prev[v] ← UNDEFINED                 // Previous node in optimal path from source
        add v to Q                          // All nodes initially in Q (unvisited nodes)

    dist[source] ← 0                        // Distance from source to source
      
    while Q is not empty:
        u ← vertex in Q with min dist[u]    // Node with the least distance
                                                    // will be selected first
        remove u from Q 
         
        for each neighbor v of u:           // where v is still in Q.
            alt ← dist[u] + length(u, v)
            if alt < dist[v]:               // A shorter path to v has been found
                dist[v] ← alt 
                prev[v] ← u 

    return dist[], prev[]
```
