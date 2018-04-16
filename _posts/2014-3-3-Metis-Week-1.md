---
layout: post
title: Week 1 - Using MTA Data to Optimize Food Truck Locations
--- 
  
  
First week of Metis is in the books! While I was pretty nervous and anxious going in, I had a great time. From meeting the instructors to my classmates, everyone at Metis is like-minded and dedicated to learning which makes a very positive and inclusive atmosphere. On the first day, we hit the ground running with Project Benson - a Data Exploratory Project that used the MTA Turnstile Data in New York.  

The project was that each group had to create a scenario, in which we would present to a “company” about how we could leverage the MTA data to help them. I really enjoyed how open-ended the first assignment was because it forced us think about Data Science from the other perspective. My group and I decided to create a fake Mexican food company, BurritoFull, 
that was looking to place a fleet of food trucks around NYC. Our presentation was focused on leveraging the MTA data to optimize the placement of their food trucks.  

### Introduction  
We had to add some context to the story, so we assumed that the food trucks will be serving breakfast/lunch, and dinner, with different menus for each meal. The fleet of trucks can be relocated once, between breakfast/lunch and dinner. The angle that my group and I took on this, was to highlight the distinction between Hub Stations (such as Penn Station, Times Sq 42nd, etc) and Destination Stations (such as Wall Street, 103rd Street). The logic is that Hub Stations are very popular and filled with people, that they are oversaturated with other food trucks and brick-and-mortar eateries. On the other hand, destination stations are less attractive for brick-and-mortar eateries because they only tend to be busy during one specific part of the day. But because of this same reason, they are perfect for food trucks, if placed correctly and strategically. Another key angle is that we strategically focused on the destination stations with a high level of exits, as people are much more likely to eat after exiting a station, than before entering a station.  
  
### Analysis  
Here’s a graph that highlights how we determined if a station is a morning destination, evening destination, or a hub:  

![an image alt text]({{ site.baseurl }}/pic.png "an image title")
