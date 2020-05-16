---
layout: post
title: Travel Schedule App
date: 2020-04-24
Author: realcyh
tags: [projects]
---


We developed a map application that can visualize multiple traffic information and can predict traffic conditions and traveling time using machine learning techniques in Atlanta for users and help them figure out when to set off will be the best. Here is a [DEMO VIDEO](https://www.youtube.com/watch?v=zzuPhJ_puPo&t=24s) of our APP.


## Frontend Visualization

We use some functions provided by Google Map javascript API to draw a map, where users can draw, show and hide markers, enter locations, get route information back.
	
First, we use `google.maps.Map` to initialize the whole map and set the map center to Greater Atlanta Area.

![img](https://raw.githubusercontent.com/realcyh/yuhang-chen/master/images/default.png "default page")

Then we add a direction Service from `google.maps.DirectionsService` and a direction render from `google.maps.DirectionsRender` for the purpose of getting route information. We also add a geocoder from `google.maps.Geocoder` for the purpose of translating an address in English into latitude and longitude.

For navigation information, a function `calculateAndDisplayRoute` is implemented to show the route from the source to the destination location.  We use `directionsRender.setDirections(response)` to visualize the route information. 

We use processed data from Uber Movement to draw zones.

![img](https://raw.githubusercontent.com/realcyh/yuhang-chen/master/images/zonesandmarkers.png "zones and markers")

We use accident logs from Georgia Open Data to show the number of accidents at a certain place.

![img](https://raw.githubusercontent.com/realcyh/yuhang-chen/master/images/traffic.png "traffic conditions")

We use d3.js to draw a bar chart which includes the estimated time to travel from source to destination in a day.

![img](https://raw.githubusercontent.com/realcyh/yuhang-chen/master/images/time.png "predicted time")
![img](https://raw.githubusercontent.com/realcyh/yuhang-chen/master/images/time2.png "predicted time")


## Frontend - Backend Interaction

We use EEL library to call a Python function in JavaScript.

We use Promise class to deal with the asynchronous callback functions on translating the source and destination address into longitude and latitude at the same time. 

To obtain predicted time, the frontend sends a REST request to the backend to get the predicted time on the desired date from the source to the destination. We use `XMLHttpRequest` in JavaScript to send the REST request. 


## Backend Construction

We use Shapely’s binary predicates which can evaluate the topolocical relationships between geographical objects to translate input coordinates to Uber MovementID. 

According to the dataset we have, we use LightGBM with five variables (sourceID, destinationID, month, day, hour) to predict travel time. 

![img](https://raw.githubusercontent.com/realcyh/yuhang-chen/master/images/restcall.png "rest call")

Our backend server is constructed with Spring boost. This server simply provides a `Get` rest call interface for the frontend to call a python script to pass these parameters into the prediction model and get the predicted travel time.

![img](https://raw.githubusercontent.com/realcyh/yuhang-chen/master/images/trainingres.png "training result")
