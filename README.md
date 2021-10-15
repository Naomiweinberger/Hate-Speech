# **Hate Speech**
Author: Naomi Weinberger
_____________________________________________________________________________________________________________________________
# **Motivation**
A hate crime is defined as a crime plus a biased motive.
![hatecrime picture](http://localhost:8888/view/pictures/hate.PNG)
According to justice.gov, from the years of 2004-2015 there were approxitamely 250,000  hate crimes commited each year. The majority of these cases were not reported to law inforcement. 
The pie chart below shows a breakdown of the bias motivation for hate crimes in 2020.
![2020 motivation](http://localhost:8888/view/pictures/bais%20motivation.jpg)
This next chart shows how those stats changed from 2019 to 2020. 
![2019/2020 motivation](http://localhost:8888/view/pictures/bar-chart-1.jpg)
I created an interactive map to show each state's hate crime rates from 2000-2020.
a study from NYU entitled [Race, Ethnicity and National Origin-based Discrimination in Social Media and
Hate Crimes Across 100 U.S. Cities](https://arxiv.org/pdf/1902.00119.pdf) shows that there is a correlation between cities with high rates of hate speech and cities with high rates of hate crimes. 
The goal of this project is to create a hate speech filter for twitter to effectively control hate speech. 
_____________________________________________________________________________________________________________________________
# **Data** 
I took two data sets from kaggle one entitled [Hate Speech and Offensive Language](https://www.kaggle.com/mrmorj/hate-speech-and-offensive-language-dataset) and the other one entitled [Twitter Sentiment Analysis](https://www.kaggle.com/arkhoshghalb/twitter-sentiment-analysis-hatred-speech) and synthesiszed them. The hate speech data set categorized tweets into three classes: hate speech, offensive language, and neither. The twitter sentiment analysis categorized the data into sexist/racist or neither. After exploring the data, I scraped twitter using tweepy (searching for some common words from the previous dataset) and created a validation set. I then tested the model on this validation set (more on that below)
_____________________________________________________________________________________________________________________________
# **EDA**
**Disclaimer: The word clouds and the frequent word plots contain sensitive words due to the nature of the project.** 
Below is a histogram depicting the amounts of tweets per class (0 is hate speech, 1 is offensive, and 2 in normal.)
![histogram of class](http://localhost:8888/view/pictures/hist%20of%20class.png) As you can see, there is a clear class imbalance. We will use SMOTE on some of the models to see if it helps.
I printed word clouds and plotted word frequencies for each of the classes. 
![Hatecloud](http://localhost:8888/view/pictures/hate%20word%20cloud.png)
![offensivecloud](http://localhost:8888/view/pictures/offensive%20word%20cloud.png)
![normalcloud](http://localhost:8888/view/pictures/normal%20word%20cloud.png)

![freqhate](http://localhost:8888/view/pictures/freq%20hate.png)
![freq offensive](http://localhost:8888/view/pictures/frq%20offensive.png)
![freqnormal](http://localhost:8888/view/pictures/freq%20normal.png)
_____________________________________________________________________________________________________________________________
# **Date preprocessing Part 1**
diagram
I created a function to clean the tweets (removing capitalization,punctuation, numbers etc.) Then I used lemmatokenizer to split the words into tokens and find the root meaning of each word. I then used a vectorizer to transform the data to numerical form. 
_____________________________________________________________________________________________________________________________
# **Data preprocessing Part 2**
I also used a seperate notebook to preprocess the same data using the neural network library SpaCy. Cleaning the text isn't required for spaCy as it takes in the contextual meaning from the text. 
_____________________________________________________________________________________________________________________________
# **Modeling**
I started off with a Naive Bayes as the base model. 
![classification report](http://localhost:8888/view/pictures/freq%20hate.png)
![confusion matrix](http://localhost:8888/view/pictures/freq%20hate.png)
There were many other models run both with the spaCy notebook and the standard preprocessing notebook.
The best model turned out to be the standard preprocessed data with a xgboost classification model (without SMOTE)
![classification report](http://localhost:8888/view/pictures/new%20final%20model%20classification%20report.PNG)
![confusion matrix](http://localhost:8888/view/pictures/new%20final%20model%20confusion.png)
I then pickled the model and imported the data that I scraped from twitter. I ran the model on the twitter data as a validation set. 
![classification report](http://localhost:8888/view/pictures/validation%20classification%20report.PNG)
![confusion matrix](http://localhost:8888/view/pictures/validation%20confusion%20matrix.png)

# **Conclusion**
While the model preformed very well on the test data, it only had a 58% accuracy on the validation set. This could because of the limitations of the validation set in terms of amount of tweets and key words chosen to create the data for each class. Also because the line of offensive and hate is a very narrow one, and it is very much a judgement call, the model has a hard time discerning one from the other.  
# **Next Steps**
There are many next steps that I would like to explore for this project:
1) Getting the gridsearch to work for the models
2) collecting a larger sample of tweets and exploring the location data to see if the locations with high rates of late speech tweets correlate to the areas with high rates of hate crimes (as the study suggests)
3) look into infamous hate crimes and see if there are high rates of hate speech surrounding those crimes
# **For More Information**
Check out the [presentation](https://www.canva.com/design/DAEsJmWtLWs/4GmtDUzmR-2X_FE5xfTpOw/view?utm_content=DAEsJmWtLWs&utm_campaign=designshare&utm_medium=link&utm_source=publishsharelink) or reach out via email [weinberger.naomi@gmail.com]