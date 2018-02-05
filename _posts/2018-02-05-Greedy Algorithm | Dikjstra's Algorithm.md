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

## Implementation
```c
// A C++ program for Dijkstra's single source shortest path algorithm.
// The program is for adjacency matrix representation of the graph
  
#include <stdio.h>
#include <limits.h>
  
// Number of vertices in the graph
#define V 9
  
// A utility function to find the vertex with minimum distance value, from
// the set of vertices not yet included in shortest path tree
int minDistance(int dist[], bool sptSet[])
{
   // Initialize min value
   int min = INT_MAX, min_index;
  
   for (int v = 0; v < V; v++)
     if (sptSet[v] == false && dist[v] <= min)
         min = dist[v], min_index = v;
  
   return min_index;
}
  
// A utility function to print the constructed distance array
int printSolution(int dist[], int n)
{
   printf("Vertex   Distance from Source\n");
   for (int i = 0; i < V; i++)
      printf("%d tt %d\n", i, dist[i]);
}
  
// Funtion that implements Dijkstra's single source shortest path algorithm
// for a graph represented using adjacency matrix representation
void dijkstra(int graph[V][V], int src)
{
     int dist[V];     // The output array.  dist[i] will hold the shortest
                      // distance from src to i
  
     bool sptSet[V]; // sptSet[i] will true if vertex i is included in shortest
                     // path tree or shortest distance from src to i is finalized
  
     // Initialize all distances as INFINITE and stpSet[] as false
     for (int i = 0; i < V; i++)
        dist[i] = INT_MAX, sptSet[i] = false;
  
     // Distance of source vertex from itself is always 0
     dist[src] = 0;
  
     // Find shortest path for all vertices
     for (int count = 0; count < V-1; count++)
     {
       // Pick the minimum distance vertex from the set of vertices not
       // yet processed. u is always equal to src in first iteration.
       int u = minDistance(dist, sptSet);
  
       // Mark the picked vertex as processed
       sptSet[u] = true;
  
       // Update dist value of the adjacent vertices of the picked vertex.
       for (int v = 0; v < V; v++)
  
         // Update dist[v] only if is not in sptSet, there is an edge from 
         // u to v, and total weight of path from src to  v through u is 
         // smaller than current value of dist[v]
         if (!sptSet[v] && graph[u][v] && dist[u] != INT_MAX 
                                       && dist[u]+graph[u][v] < dist[v])
            dist[v] = dist[u] + graph[u][v];
     }
  
     // print the constructed distance array
     printSolution(dist, V);
}
```

Notes:  
1) The code finds shortest distances from source to all vertices. If we are interested only in shortest distance from source to a single target, we can break the for loop when the picked minimum distance vertex is equal to target (Step 3.a of algorithm).

2) Time Complexity of the implementation is O(V^2). If the input graph is represented using adjacency list, it can be reduced to O(E log V) with the help of binary heap. 

3) Dijkstra’s algorithm doesn’t work for graphs with negative weight edges. For graphs with negative weight edges, Bellman–Ford algorithm can be used.

4) If the count of shortest path is needed, we can maintain an array called spCnt(shortest path counter). Then spCnt[i] indicates the count of shortest path from source node to node i. The core codes are as follow:
```c
     // This Initialization is nessesary.
     spCnt[src] = 1; 
     // Find shortest path for all vertices
     for (int count = 0; count < V-1; count++)
     {
       // Pick the minimum distance vertex from the set of vertices not
       // yet processed. u is always equal to src in first iteration.
       int u = minDistance(dist, sptSet);
  
       // Mark the picked vertex as processed
       sptSet[u] = true;
  
       // Update dist value of the adjacent vertices of the picked vertex.
       for (int v = 0; v < V; v++)
  
         // Update dist[v] only if is not in sptSet, there is an edge from 
         // u to v, and total weight of path from src to  v through u is 
         // smaller than current value of dist[v]
         if (!sptSet[v] && graph[u][v] && dist[u] != INT_MAX )
            if(dist[u]+graph[u][v] < dist[v])
            {
                dist[v] = dist[u] + graph[u][v];
                spCnt[v] = spCnt[u];        // update the count of paths of v.
            }
            else if(dist[u]+graph[u][v] < dist[v])
                spCnt[v] = spCnt[u] + spCnt[v];
     }
  
```

