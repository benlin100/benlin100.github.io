![image tooltip here](/images/title.png)  
  
### Backstory & Motivation  
Imagine the forest department in Colorado is looking to expand the National Roosevelt Forest by developing the surrounding land. They have access to an open dataset that tracks cartographic and environmental variables for 30x30m sections of the forest. Their objective is to use this dataset to expedite the development of the surrounding land. Specifically, being able to predict the predominant tree type in an area, so they can provide the proper nutrients and irrigation to maximize growth.  

Here is how I would approach this objective:  
    
### Data 
The USDA Forest Service published a dataset that looks at many cartographic and environmental variables for each section of the Roosevelt National Forest. Most notably, they track the predominant tree type in each area, which will be what I’m trying to predict.  
  
Here’s a quick overview of the data:  

##### Response Variables: 

Tree Type*: the type of tree that is predominantly in that area (7 different trees)

##### Predictor Variables: 

Elevation - Elevation in meters  
Aspect - Aspect in degrees azimuth  
Slope - Slope in degrees  
hDist_Water - Horz Dist to nearest surface water features  
vDist_Water - Vert Dist to nearest surface water features  
hDist_Road - Horz Dist to nearest roadway  
shade_9am -  (0 to 255 index) - Hillshade index at 9am, summer solstice  
shade_noon (0 to 255 index) - Hillshade index at noon, summer solstice  
shade_3pm (0 to 255 index) - Hillshade index at 3pm, summer solstice  
hDist_Fire - Horz Dist to nearest wildfire ignition points  
Wilderness Area* - Designated wilderness area (4 different areas)   
Soil Types* - Designated soil type (40 different soils)  
    
###### * = Categorical

  
### Data Analysis
I first looked at the distribution of all 7 tree types in my dataset using PCA. PCA, principal component analysis, essentially takes all my predictor variables, and creates 2 new components (shown on the X and Y axes). Within each component, each predictor variable is assigned a new value that signifies its’ importance. Here is the visualization:   
  
![image tooltip here](/images/trees.png)  
  
From this chart, it’s clear that all 7 tree types (7 colors) have unique distributions in respect to the two components. Digging a little deeper, I looked at the most important variables in both Component 1 and 2. For Component 1, Wilderness Area 4, Slope, and Soil Type 10, captures the most variance. For Component 2, 9am shade, Wilderness Area 1, and Soil Type 30 captures the most variance. It’s interesting to note that specifically Wilderness Area 4/1 and Soil Type 10/30 are more important than the other 2, and the other 38. With PCA, I was able to quickly visualize the distribution of the varying tree types and gain a better intuition about my variables.    
  
 
 
 
  
My next step was to check for high multicollinearity between any of my predictor variables. Thankfully, none of the variables were too highly correlated, but I did find some very interesting relationships along the way. The correlation between elevation and the horizontal distance to the road especially stood out to me. Here is the correlation plot with respect to the 7 tree types. 
  
![image tooltip here](/images/elevation.png)  
  
From first glance, it’s clear that each tree type has very distinct ranges of both elevation as well as horizontal distance to the road. For example, if we just look at Tree 2 (Lodgepole Pine), it has a small range of elevation (2875-3200) and a much larger range of horizontal distance to the road (0 to 6000). Just by looking at these plots, I further gained a deeper knowledge and understanding of what’s most important to determining the type of tree in an area.  
  
  
### Models
  
Before modeling, I split my dataset into a 80% training and a 20% test set. I experimented with different sets of predictor variables, but including all of them gave me the best metrics, so that is the final dataset I used.  
  
I ran 6 different models on all my variables - optimizing for each model’s specific parameters. I first started with Naive Bayes as a baseline model, which gave me a F1 score (average of precision and recall) on the test set of 0.54. I then moved on to more advanced models, like KNN and SVM, which gave me relatively much better F1 scores of ~0.82. I was curious to dive in a little deeper so I experimented with tree models, specifically Decision Tree Classifier to Extra Trees Classifier to Random Forest Classifier. Here’s a snapshot of the F1 scores for each model:  
  
![image tooltip here](/images/models.png)    
  
One thing to note here, is that as you scan right, the interpretability of the model becomes more abstract and difficult to understand. However with this particular objective, I just needed the model with the best predicting power. So I went with Random Forest, which did the best with an F1 score of 0.87.  
  
I then took a look at the most important variable for my Random Forest model. Here is a chart that lists the top 5 most important variables with their “importance” score on the y-axis.  
  
![image tooltip here](/images/features.png)  
  
Elevation is by far the most important variable. If you recall from the correlation plot earlier, this makes sense, as each tree type had an especially unique distribution of elevation. I also found it interesting how important the distance to the road, fire, and water are. After some thinking, it makes sense because all 3 metrics technically measure how “deep” into the forest one area is, which would be very important in determining tree type.  
  
### Conclusion  
  
To wrap everything together, my model can predict a tree type in the undeveloped land with 87% accuracy. Not too bad! Now the forest department can go into these areas with the proper nutrients and irrigation levels to expedite the development process.  
  
If I had more time, I would have loved to implement deep learning to see if I could improve that F1 score.   
  
Thanks for reading!  
Ben  
