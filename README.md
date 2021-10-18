# **Hate Speech**
Author: Naomi Weinberger
_____________________________________________________________________________________________________________________________
# **Motivation**
A hate crime is defined as a crime plus a biased motive.
<img width="780" alt="hate" src="https://user-images.githubusercontent.com/78061842/137782136-11b23e84-bc58-400a-b39c-b83242b029ec.PNG">
According to justice.gov, from the years of 2004-2015 there were approxitamely 250,000  hate crimes commited each year. The majority of these cases were not reported to law inforcement. 
The pie chart below shows a breakdown of the bias motivation for hate crimes in 2020.
![bais motivation](https://user-images.githubusercontent.com/78061842/137782179-2bc7ed4a-d70b-4fbb-9a52-bde72d919da1.jpg)
This next chart shows how those stats changed from 2019 to 2020. 
![bar-chart-1](https://user-images.githubusercontent.com/78061842/137782234-5d4c7afb-232a-4a80-99b5-b958db19f49a.jpg)
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
![hist of class](https://user-images.githubusercontent.com/78061842/137782292-d4dcd242-be46-4ac5-8bba-a350a8be8e91.png) As you can see, there is a clear class imbalance. We will use SMOTE on some of the models to see if it helps.
I printed word clouds and plotted word frequencies for each of the classes. 

![hate word cloud](https://user-images.githubusercontent.com/78061842/137782337-10ae4dee-ac4b-45b2-b654-e9969dbaf0ed.png)


![offensive word cloud](https://user-images.githubusercontent.com/78061842/137782347-91401ea1-1c14-4809-bd9e-2b644b94e5eb.png)
![download](https://user-images.githubusercontent.com/78061842/137782358-9fab0f98-f0a0-4ae1-bc26-e43af61c524c.png)
![freq hate](https://user-images.githubusercontent.com/78061842/137782417-c1fddaaa-8b17-4c8f-b5ab-76d534694d16.png)

![frq offensive](https://user-images.githubusercontent.com/78061842/137782432-e40d62c4-4e72-4bac-bc4a-b883ff672d1c.png)
![freq normal](https://user-images.githubusercontent.com/78061842/137782422-f013f3a6-f3b6-4d05-95ac-8339dcc2f717.png)

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

<img width="254" alt="base model classification report" src="https://user-images.githubusercontent.com/78061842/137782538-963566bd-fe84-4c19-85ca-8db608777ded.PNG">
![base model confusion plot test](https://user-images.githubusercontent.com/78061842/137782533-a8ecfb4c-5c72-433d-983a-9d26a06395ad.png)
There were many other models run both with the spaCy notebook and the standard preprocessing notebook.
The best model turned out to be the standard preprocessed data with a xgboost classification model (without SMOTE)
![new final model confusion](https://user-images.githubusercontent.com/78061842/137782696-2f7683e4-51d7-4984-974c-3ed1fda8b02e.png)
<img width="423" alt="new final model classification report" src="https://user-images.githubusercontent.com/78061842/137782691-8d90e0bc-f4d6-4ddc-bdfb-6a578a9798ee.PNG">

I then pickled the model and imported the data that I scraped from twitter. I ran the model on the twitter data as a validation set. 
<img width="358" alt="validation classification report" src="https://user-images.githubusercontent.com/78061842/137782803-711e6c4e-5e97-4e9c-a200-b17966395c42.PNG">
![validation confusion matrix](https://user-images.githubusercontent.com/78061842/137782813-44bfa4b1-dbe9-4d1d-94ff-59a99cfc36ae.png)

# **Conclusion**
While the model preformed very well on the test data, it only had a 58% accuracy on the validation set. This could because of the limitations of the validation set in terms of amount of tweets and key words chosen to create the data for each class. Also because the line of offensive and hate is a very narrow one, and it is very much a judgement call, the model has a hard time discerning one from the other.  
# **Next Steps**
There are many next steps that I would like to explore for this project:
1) Getting the gridsearch to work for the models
2) collecting a larger sample of tweets and exploring the location data to see if the locations with high rates of late speech tweets correlate to the areas with high rates of hate crimes (as the study suggests)
3) look into infamous hate crimes and see if there are high rates of hate speech surrounding those crimes
# **For More Information**
Check out the [presentation](https://www.canva.com/design/DAEsJmWtLWs/4GmtDUzmR-2X_FE5xfTpOw/view?utm_content=DAEsJmWtLWs&utm_campaign=designshare&utm_medium=link&utm_source=publishsharelink) or reach out via email [weinberger.naomi@gmail.com]