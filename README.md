# **Hate Speech**
Author: Naomi Weinberger
_________________________________________________________________________________________________________________________
# **Motivation**

**WARNING: DUE TO THE NATURE OF THE PROJECT,THIS NOTEBOOK CONTAINS HATEFUL SPEECH. THIS IN NO WAY REFLECTS THE VIEWS OF THE AUTHOR.**

A hate crime is defined as a crime plus a biased motive.

![Capture](https://user-images.githubusercontent.com/78061842/137785605-eca7644e-cdd1-4be8-8089-37deca4dd731.JPG)
According to [justice.gov](justice.gov) , from the years of 2004-2015 there were approximately 250,000  hate crimes commited each year. The majority of these cases were not reported to law enforcement. 

The pie chart below shows a breakdown of the bias motivation for hate crimes in 2020.

![bais motivation](https://user-images.githubusercontent.com/78061842/137782179-2bc7ed4a-d70b-4fbb-9a52-bde72d919da1.jpg)

This next chart shows how those stats changed from 2019 to 2020. 

![bar-chart-1](https://user-images.githubusercontent.com/78061842/137782234-5d4c7afb-232a-4a80-99b5-b958db19f49a.jpg)

I created an interactive map to show each state's hate crime rates from 2000-2020.

<img width="772" alt="map" src="https://user-images.githubusercontent.com/78061842/139447092-a0f5a0a0-9ad4-4b92-9773-5b4ec438ec7b.PNG">

A study from NYU entitled [Race, Ethnicity and National Origin-based Discrimination in Social Media and
Hate Crimes Across 100 U.S. Cities](https://arxiv.org/pdf/1902.00119.pdf) 
shows that there is a correlation between cities with high rates of hate speech and cities with high rates of hate crimes. 
The goal of this project is to create a hate speech filter for twitter to effectively control hate speech. 
_____________________________________________________________________________________________________________________________
# **Data** 
I took two data sets from Kaggle one entitled [Hate Speech and Offensive Language](https://www.kaggle.com/mrmorj/hate-speech-and-offensive-language-dataset) and the other one entitled [Twitter Sentiment Analysis](https://www.kaggle.com/arkhoshghalb/twitter-sentiment-analysis-hatred-speech) and synthesized them. The hate speech data set categorized tweets into three classes: hate speech, offensive language, and neither. The twitter sentiment analysis categorized the data into sexist/racist or neither. After exploring the data, I scraped Twitter using Tweepy (searching for some common words from the previous dataset) and created a validation set. I then tested the model on this validation set (more on that below.)
_____________________________________________________________________________________________________________________________
# **EDA**

Below is a histogram depicting the amounts of tweets per class (0 is hate speech, 1 is offensive, and 2 in normal.)

![hist of class](https://user-images.githubusercontent.com/78061842/137782292-d4dcd242-be46-4ac5-8bba-a350a8be8e91.png) 

As you can see, there is a clear class imbalance. We will use SMOTE on some of the models to see if it helps.
I printed word clouds and plotted word frequencies for each of the classes. 

![hate word cloud](https://user-images.githubusercontent.com/78061842/137782337-10ae4dee-ac4b-45b2-b654-e9969dbaf0ed.png)


![offensive word cloud](https://user-images.githubusercontent.com/78061842/137782347-91401ea1-1c14-4809-bd9e-2b644b94e5eb.png)
![download](https://user-images.githubusercontent.com/78061842/137782358-9fab0f98-f0a0-4ae1-bc26-e43af61c524c.png)
![Normal Speech Freq](https://user-images.githubusercontent.com/78061842/139445622-d05cc78c-53e6-4067-803f-f9c44996c63f.png)

![Offensive Speech Freq](https://user-images.githubusercontent.com/78061842/139445658-daf33ea2-7b7d-4271-bc69-74f6a4e5acdc.png)

![Hate Speech Freq](https://user-images.githubusercontent.com/78061842/139445686-11232e91-cc2d-4410-88ae-d6a1a0d48cb7.png)


_____________________________________________________________________________________________________________________________
# **Date Pre-processing Part 1**
I used two different methods to preprocess the data. The picture below shows both processes.

![Ash Grey and Beige Dark Theme Professional Investor Business Presentation](https://user-images.githubusercontent.com/78061842/137785984-656e8de4-69cb-43ff-8778-81feab29cd6e.png)

I created a function to clean the tweets (removing capitalization,punctuation, numbers etc.) Then I used lemmatokenizer to split the words into tokens and find the root meaning of each word. I then used a vectorizer to transform the data to numerical form. 
_____________________________________________________________________________________________________________________________
# **Data Pre-processing Part 2**

I also used a seperate notebook to preprocess the same data using the neural network library spaCy. Cleaning the text isn't required for spaCy as it takes in the contextual meaning from the text. 
_____________________________________________________________________________________________________________________________
# **Modeling**

I started off with a Naive Bayes as the base model. 


![base model new](https://user-images.githubusercontent.com/78061842/139445279-4cfdffd0-0ebc-48a3-86a5-aed3d790d278.JPG)

![base model new 1](https://user-images.githubusercontent.com/78061842/139445278-8d76cfe2-402d-49dd-8ce0-d96cc0458d27.JPG)


There were many other models run both with the spaCy notebook and the standard pre-processing notebook.

The best model was a random forest model that was preprocessed with spaCy and utilized SMOTE.


![final spacy model 1](https://user-images.githubusercontent.com/78061842/139443352-cf89f9e9-3347-45e8-8039-793deb92f759.JPG)

![final spacy model 2](https://user-images.githubusercontent.com/78061842/139445508-32072931-67fc-4a59-bdaa-142ecde1648b.JPG)



I then pickled the model and imported the data that I scraped from Twitter. I ran the model on the Twitter data as a validation set. 

![rfSMOTE_validation_2](https://user-images.githubusercontent.com/78061842/139444543-dea80e6d-497f-45fb-a575-339d4a398ec3.JPG)

![rfSMOTE_Validation_1](https://user-images.githubusercontent.com/78061842/139444586-904ceef3-de57-4c24-9d49-9558e49f1b13.JPG)


# **Conclusion**
The model performed almost perfectly on the test data. On the validation set, the accuracy dropped but was still able to predict what class the tweet would be classified in with an 80% accuracy. 

# **Next Steps**

There are many next steps that I would like to explore for this project:
1) Collect a larger sample of tweets and explore the location data to see if the locations with high rates of late speech tweets correlate to the areas with high rates of hate crimes (as the study suggests)
2) Look into famous hate crimes and see if there are high rates of hate speech surrounding those crimes
3) Create a front-end with an imput box so that people can test their tweet to predict if it will be classified as hate speech. 

# **For More Information**

Check out the [presentation](https://www.canva.com/design/DAEsJmWtLWs/4GmtDUzmR-2X_FE5xfTpOw/view?utm_content=DAEsJmWtLWs&utm_campaign=designshare&utm_medium=link&utm_source=publishsharelink) or reach out via email weinberger.naomi@gmail.com




