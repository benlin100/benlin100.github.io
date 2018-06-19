---
layout: post
title: Musician's Alter Egos
--- 
  
![image tooltip here](/images/thetitle.jpg)   
  
Throughout time, artists have always adopted alter egos to express different sides of their personality. From Prince and his female alter ego Camille, to Eminem and his evil counterpart, Slim Shady. For this project, I focused on Logic, a hip-hop artist known for his range of diction, complex rhyme schemes, and captivating storytelling. While Logic stands for peace, love, and positivity, he also has 2 alter egos: Young Sinatra and Bobby Tarantino. Young Sinatra is his young and vengeful persona, motivated by success and money. On the other hand, Bobby Tarantino is his successful persona, where he’s achieved all his dreams and is boldly outspoken.  
  
![image tooltip here](/images/l2.png)   
  
### Logic, Young Sinatra, or Bobby Tarantino?      
      
My final dataset consisted of lyrics from six albums, two under each persona. Each row in my dataframe was one line of a song, with 2,000 rows under each persona.  
    
Normally, my next step would be to clean and normalize the text. However in this case, each of Logic’s alter egos have their own unique idiosyncrasies, so I limited normalizing to preserve those patterns.  
  
My first objective was to use topic modeling algorithms to group his lyrics text into 3 distinct themes. I was most interested in comparing how the models differentiated his text to his 3 alter egos and what each represent. My second objective was to build a model that allows a user to enter any phrase, and it will predict if it came from Logic, Young Sinatra, or Bobby Tarantino.  
  
### Tools & Algorithms:  
  
For scraping lyrics data, I used a nifty built-in package called ‘thecypher’, which scrapes lyrics from lyricwiki.com and formats it into a pandas dataframe. Unfortunately some of his earlier albums weren’t on lyricwiki.com so I had to use Beautiful Soup to scrape the remaining lyrics.  
  
For featuring engineering and preparing my data for the models, here are the main text tools I used: Spacy, CountVectorizer, tf-idf, and Word2Vec.  
  
For unsupervised/topic modeling, I used PCA (principal component analysis) and LDA (latent dirichlet allocation). For my predictive model, I experimented with 3 main algorithms: Support Vector Classifiers, Multi N.B., and KN Classifier.  
  
### Objective 1 - Topic Modeling: 
  
Once my data was in a good state, I ran LDA, a topic modeling algorithm. LDA essentially processes text and creates a number of topics that specific words are attributed to. I was especially interested to see if the topics LDA created would be synonymous with the 3 topics under his alter egos. As a quick reminder, here is what each of his alter egos is associated with: (Logic: peace, love, and society), (Young Sinatra: success, motivated, vengeful), (Bobby Tarantino: outspoken, fun, carefree).  
  
After running LDA, it most ‘logically’ broke into two topics, instead of three like his alter egos. The top terms under each topic was:  
    
![image tooltip here](/images/asd.png)   

The terms under Topic 1 are extremely synonymous with Logic and what he represents. On the other hand, the terms under Topic 2 are more synonymous with both Young Sinatra and Bobby Tarantino. When I tried to increase the number of topics to 3, one of the topics were still associated with Logic, but the other 2 became very abstract and unclear. LDA clearly separated topics for Logic Vs. Young Sinatra/Bobby Tarantino. However, it had difficulty differentiating between Young Sinatra and Bobby Tarantino.   
  
In terms of what I personally took away, Young Sinatra and Bobby Tarantino aren’t as different as I had thought. The data shows that the topics they cover have a lot of similarities.  

### Objective 2 - Predictive Model:  
  
My next objective was creating a model that accurately predicts which alter ego a phrase likely came from. Here is a snapshot of the permutations of features and algorithms I tried, and their respective accuracy score:  
  
![image tooltip here](/images/hi.png)   
  
With the tf-idf features and the multinomial Naive Bayes model, I came to my best test-set accuracy score of 0.674. Tf-idf, which stands for ‘term frequency–inverse document frequency’, is a numerical statistic that reflect how important a word is to the overall text. Unlike Bag of Words, which simply tracks the number of counts for each word, tf-idf puts each word in relation to the other words in the overall piece of text. Using tf-idf instead of Bag of Words is especially important in hip-hop lyrics because filler words are commonly used. Tf-idf is able to capture the most important significant words for each of his 3 personas, which is why it gave me the best accuracy score.  

Here is a snapshot of the model in work:  
![image tooltip here](/images/logic_demo.png)  
All 3 phrases are random and they all accurately classify to the correct alter ego.  
  
I really enjoyed working on this project because I’ve been listening to Logic grow throughout his career. I’ve always been intrigued by his different characters and his lyrical diversity.  I’ve never went into a project with preconceived notions of what I wished the data would show, so it was very interesting to compare my intuition with what the data actually showed. I hope you enjoyed the read!  
  
If interested, you can find more information on my Github: https://github.com/benlin100/artist_alter_egos  
  
Best,  
Ben
