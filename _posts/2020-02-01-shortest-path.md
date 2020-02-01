---
layout: post
title: Shortest Path
date: 2020-02-01
Author: realcyh
toc: true
tags: [algorithms]
---

# test

## Bellman-Ford algorithm

The Bellman-Ford algorithm is a fundamental way to compute the shortest paths from one source to all of the other edges 
in a weighted graph. The basic idea of Bellman-Ford algorithm is Relaxation, that is, the approximations to the correct 
distance are replaced with better ones until they eventually reach the solution. It simply relaxes all the edges each 
time and does this $|V|-1$ times, where $|V|$ is the number of vertices in the graph. The time complexity is $O(|V||E|)$.

```
// pseudocode
Bellman-Ford:
// initialize
	for each vertex v in vertices:
		distance[v] = inf
		predecessor[v] = null
	distance[source] = 0

// relaxation
	for i in range(size(vertices)-1):
		for each edge (u, v) in edges:
			if distance[u] + weight(u,v) < distance[v]:
				distance[v] = distance[u] + weight(u,v)
				predecessor[v] = u
```

### test2

# test3

## Dijkstra's algorithm

The Dijkstra's algorithm is a faster way to compute the shortest paths from one source to all of the other edges in 
a weighted graph. It can also be used for finding the shortest path from a single source to a single destination by 
stopping the proceed once the shortest path to the destination has been determined. The basic idea of Dijkstra's 
algorithm is also Relaxation, but it use a priority queue to greedily choose the closest vertex that has not been 
proceeded yet and perform relaxation process on all of its outgoint edges. So we use a set $S$ to maintain all the 
vertices that have already been processed and the shortest path to that vertex has been computed, and another set $Q$ 
to maintain the remainint vertices. 

The time complexity mainly depends on the data structure we use. If we simply 
use a list or an array to store the distances, the time complexity will be $O(|V|^2)$, since each time, we have to 
linearly search the list or array to find the vertex with smallest distance in $Q$. If we use a binary heap, the time 
complexity will be $O((|V|+|E|)log(|V|))$.

```
// pseudocode
Dijkstra:
// initialize
	for each vertex v in vertices:
		distance[v] = inf
		predecessor[v] = null
	distance[source] = 0
	S = {} // empty set
	Q = {vertices} // set of all vertices
  
// relaxation
	while Q is not empty:
		u = vertex with minimum distance value in Q
		S.append(u)
		Q.pop(u)
		for each edge outgoint from u as (u, v):
			if distance[u] + weight(u,v) < distance[v]:
				distance[v] = distance[u] + weight(u,v)
				predecessor[v] = u 
```
