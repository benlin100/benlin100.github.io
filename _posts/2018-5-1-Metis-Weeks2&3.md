---
layout: post
title: Week 2&3 - Predicting NBA Salaries
--- 
  
3 weeks of Metis is in the books! For the past 2 weeks, we’ve been learning about web scraping with BS4 and Selenium to all the capabilities of Linear Regression. For my second project, I used NBA player statistics to build a model that predicts their salary.   
  
Imagine being an NBA agent for Golden State Warriors’s Klay Thompson. His contract is expiring at the end of this season and your job is to maximize his value. The question then lies - what is the maximum amount of money you should negotiate for? This is the motivation behind this project - and the answer is, $20.9 million. 
This is the process behind the answer:  


### Data Scraping & Cleaning
I scraped ~400 NBA player statistics from the 2016-2017 season and ~400 NBA player salaries from the 2017-2018 season. The player statistics consisted of relative basic stats: Games, Games Started, Minutes Played, FG, FGA, 3P, 3P%, 2P, 2P%, FT, Rebounds, Assists, Steals, Blocks, Etc. I then merged these two dataframes on names (luckily, there’s no one in the NBA with the same name)!  
  
While putting together my final dataset, I ran into a couple of minor issues. Some players from 2016-2017 retired the following year so they were missing salary data. On the other hand, players that came in the league this year did not have any statistics data. To resolve this issue, I dropped them out of my final dataset. Another issue was that for players that got traded, their “Team” label was “TOT”, instead of the team they were traded to. I had to manually assign each traded player to their current respective teams. As an aside, I also added a binary playoff column indicating whether or not the player made the playoffs. My hypothesis is that players that make the playoffs get more exposure and spotlight, which increase their value in the following season.  
  
  
### Analysis
I first looked at the distribution of my predictor variable, salary, and realized I needed to apply a square-root transformation to normalize the data.   
  
### *Distribution of Salary and sqrt(Salary)*
Sqrt(Salary)               |  Salary
:-------------------------:|:-------------------------:
![](/images/blog.png)      |  ![](/images/blog1.png)  
  
The two graphs above shows how sqrt(salary) provides a more normal distribution than just salary. Furthermore, the sqrt(salary) also showed significantly less heteroskedasticity than the raw value of salary. Because of these reasons, I moved forward with the sqrt(Y) being my predictor variable. 
  
Before building models, I was interested to see how different features were correlated with salary. The left graph below shows the correlation of minutes played to salary, and the right graph shows the correlation of age to salary. 

![image tooltip here](/images/blog2.png)  

It intuitively makes sense that minutes played has a strong correlation with salary, because if you play more minutes, you are likely more valuable to a team. On the other hand, age has a weaker correlation, because age is not a determinant of skill-level or value to a team.  
  
I also looked at the average difference of salaries between players who made the playoffs, and those who didn’t.  
![image tooltip here](/images/blog4.png)  
  
This shows that players who made the playoffs, on average, make around $200,000 more than players who don’t.  

### Model Selection
  
I split my dataset into a 80% training and 20% test set and then fit 3 models on the training dataset. Here’s a quick overview of how I decided what features to use for each model: 

Model 1: Used the highest correlated features to salary (removing multicollinear features)
Model 2: Used the highest correlated features to salary (including multicollinear features)
Model 3: Used all features except for age 

I used 5-fold cross validation R2  scores to determine which model performed best. With each model, Linear Regression showed overfitting, so I used Ridge, Lasso, and ElasticNet to regularize the models (optimizing hyperparameters using grid-search). Here are the results: 

![image tooltip here](/images/blog24.png)  

My best performing model was using the features in Model 3 with the Ridge technique, which gave a R2  score of 0.564. It’s also interesting to note that model 3 shows the greatest sign of overfitting because it has the greatest R2 difference in comparison to the regularized models. This makes sense as Model 3 provides greater predictive power from more variables, and the Ridge controls the overfitting by using regularization, which results in the best model. The score of 0.564 means that my model captures only 56% of the variance in NBA salaries. The RMSE (or Standard Deviation) is around $720,000.  

### Conclusion  
Below is a graph that shows the actual salaries on the X-axis, and my predicted salaries on the y-axis.  
![image tooltip here](/images/blog25.png)  
  
While there is a correlation of 0.81, it’s clear that there are still some outliers in my predictions. I pinpointed one player, Klay Thompson, which my model accurately predicted. Thompson’s actual salary this year is $17.8 million, while my model predicted $18.7 million. With an RMSE of $700K, I can be 95% confident that Klay’s salary should be between $17.9 and $20.9 million. As his agent, you should aim to negotiate a deal for that upper threshold!  
  
*Note: My current model disregards how salaries are set up in the NBA, and how they are based on contracts. If I had more time, I would set rules for my models to take into account years of contracts and furthermore, predict how long of a contract a player is expected to get.  
