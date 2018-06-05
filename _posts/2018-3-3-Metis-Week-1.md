---
layout: post
title: Week 1 - Optimal Food Truck Locations
--- 
  
![image tooltip here](/images/burrito.jpg)  
  
First week of Metis is in the books! While I was pretty nervous and anxious going in, I had a great time. From meeting the instructors to my classmates, everyone at Metis is like-minded and dedicated to learning which makes a very positive and inclusive atmosphere. On the first day, we hit the ground running with Project Benson - a Data Exploratory Project that used the MTA Turnstile Data in New York.  

The project was that each group had to create a scenario, in which we would present to a “company” about how we could leverage the MTA data to help them. I really enjoyed how open-ended the first assignment was because it forced us think about Data Science from the other perspective. My group and I decided to create a fake Mexican food company, BurritoFull, 
that was looking to place a fleet of food trucks around NYC. Our presentation was focused on leveraging the MTA data to optimize the placement of their food trucks.  

### Introduction  
We had to add some context to the story, so we assumed that the food trucks will be serving breakfast/lunch, and dinner, with different menus for each meal. The fleet of trucks can be relocated once, between breakfast/lunch and dinner. The angle that my group and I took on this, was to highlight the distinction between Hub Stations (such as Penn Station, Times Sq 42nd, etc) and Destination Stations (such as Wall Street, 103rd Street). The logic is that Hub Stations are very popular and filled with people, that they are oversaturated with other food trucks and brick-and-mortar eateries. On the other hand, destination stations are less attractive for brick-and-mortar eateries because they only tend to be busy during one specific part of the day. But because of this same reason, they are perfect for food trucks, if placed correctly and strategically. Another key angle is that we strategically focused on the destination stations with a high level of exits, as people are much more likely to eat after exiting a station, than before entering a station.  
  
### Analysis  
Here’s a graph that highlights how we determined if a station is a morning destination, evening destination, or a hub:  

![image tooltip here](/images/pic.png)  
  
To start, we had to calculate the ratio of exits to total traffic (y-axis) and tracked that throughout the hours of a day (x-axis). The dotted line on the graph represents when the ratio of exits is equal to entries, so anything that’s above the dotted line is a higher ratio of exits, and anything below is a lower ratio of exits.  
  
Starting from the left graph, we can see that the World Trade Center station is a morning destination because it has a high ratio of exits in the morning time and a low ratio of exits in the evening time. This intuitively makes sense as the WTC is a business-heavy location.  
  
In the middle graph, we can see that Aqueduct Station is a evening destination because there’s a high ratio level of exits in the evening time, and a low ratio in the morning time. This also intuitvely makes sense as Aqueduct is more of a residential area.  
  
In the right graph, we can see that Grand Central is a hub destination because the line floats a lot closer to 0.5. That’s because in a hub like Grand Central, there’s always a large flow of people exiting and entering throughout the day which brings the ratio closer to equal.  
  
  
  
As next steps, we wanted to expand that initial classification across all stations, and determine which stations had both a high ratio of exits and  substantial station size. We graphed a scatter plot of all the Stations with regards to their ratio of exits (y-axis) and station size (x-axis). 

Here is one of the 4 graphs that highlights Weekday Dinners:  
![image tooltip here](/images/pic2.png)  
*(3 different graphs for Weekday - Breakfast/Lunch, Weekend - Breakfast/Lunch, Weekend - Dinner)
  
We are most interested in the stations that fall well above the 0.5 ratio of exits, as well as those with a high numbers of exiting riders. Those stations, on the plot, lie in the upper middle-right region. We did this analysis for the other 3 charts to determine the best location for the varying times and days. 

### Summary  
We summarized the results here:  
![image tooltip here](/images/pic3.png)  

We narrowed down the choices of stations based on both our analysis and domain knowledge. We took into consideration that we wanted to have a high level of geographic diversity (i.e. not all food trucks parked in lower Manhattan)  Additionally, even though Newark Penn Station shows up as high on our list, we know that it is a transit center, so even people exiting the PATH train will likely be getting on another train and not be amenable to purchasing burritos. For weekends, our data analysis didn’t show as clear of patterns, but we understand the top tourist destinations are those in midtown and lower manhattan during the morning, and the residential neighborhoods at dinner are spread more evenly across boroughs.  

If given more time, we would have loved to analyze the trend in our metrics over the course of the previous year.  It’d also be interesting to pull in other food truck location data by accessing the Twitter API. Additionally, we would perform surveys in various neighborhoods around New York to understand customer tastes.  

This first project at Metis was challenging yet exciting. I understand the journey is long and treacherous, but I’m looking forward to the rest of the bootcamp! 
