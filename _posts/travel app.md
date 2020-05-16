---
layout: post
title: Travel Schedule App
date: 2020-04-24
Author: realcyh
tags: [projects]
---


We developed a map application that can visualize multiple traffic information and can predict traffic conditions and traveling time using machine learning techniques in Atlanta for users and help them figure out when to set off will be the best.


## Frontend Visualization

We use some functions provided by Google Map javascript API to draw a map, where users can draw, show and hide markers, enter locations, get route information back.
	
First, we use `google.maps.Map` to initialize the whole map and set the map center to Greater Atlanta Area.

--default pic

Then we add a direction Service from `google.maps.DirectionsService` and a direction render from `google.maps.DirectionsRender` for the purpose of getting route information. We also add a geocoder from `google.maps.Geocoder` for the purpose of translating an address in English into latitude and longitude.

For navigation information, a function `calculateAndDisplayRoute` is implemented to show the route from the source to the destination location.  We use `directionsRender.setDirections(response)` to visualize the route information. 

We use processed data from Uber Movement to draw zones.

--pic

We use accident logs from Georgia Open Data to show the number of accidents at a certain place.

-- pic

We use d3.js to draw a bar chart which includes the estimated time to travel from source to destination in a day.

--pic


##Frontend - Backend Interaction

We use EEL library to call a Python function in JavaScript.

We use Promise class to deal with the asynchronous callback functions on translating the source and destination address into longitude and latitude at the same time. 

To obtain predicted time, the frontend sends a REST request to the backend to get the predicted time on the desired date from the source to the destination. We use `XMLHttpRequest` in JavaScript to send the REST request. 


##Backend Construction


We use Shapely’s binary predicates which can evaluate the topolocical relationships between geographical objects to translate input coordinates to Uber MovementID. 

According to the dataset we have, we use LightGBM with five variables (sourceID, destinationID, month, day, hour) to predict travel time. 

Our backend server is constructed with Spring boost. This server simply provides a `Get` rest call interface for the frontend to call a python script to pass these parameters into the prediction model and get the predicted travel time.




## Dijkstra's algorithm

The Dijkstra's algorithm is a faster way to compute the shortest paths from one source to all of the other edges in 
a weighted graph. It can also be used for finding the shortest path from a single source to a single destination by 
stopping the proceed once the shortest path to the destination has been determined. The basic idea of Dijkstra's 
algorithm is also **Relaxation**, but it use a priority queue to greedily choose the closest vertex that has not been 
proceeded yet and perform relaxation process on all of its outgoint edges. So we use a set $S$ to maintain all the 
vertices that have already been processed and the shortest path to that vertex has been computed, and another set $Q$ 
to maintain the remainint vertices. 

The time complexity mainly depends on the data structure we use. If we simply use a list or an array to store the 
distances, the time complexity will be $O(|V|^2)$, since each time, we have to linearly search the list or array to find 
the vertex with smallest distance in $Q$. If we use a binary heap, the time complexity will be $O((|V|+|E|)log(|V|))$.

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
