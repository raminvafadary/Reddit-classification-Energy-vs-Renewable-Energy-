# Reddit classification (Energy vs Renewable Energy)

## Problem Statement

The Renewable energy usage is increasing with a very high pace.There are numerous forums that talk about the Renewable enrgy. one of the places the people talk about Renewable Energy is Reddit. but there are both Renewable Energy and None-Renewable Energy subreddits.My goal is to use natural language processing and supervised learning to predict whether an article is from r/renewable  or from r/energy by the title and comments.


## Project Description


## Data Collection & Processing
The data for this project was collected using the pushshift.io API. It contains the 20,000 most recent submissions (at time of collection) to each subreddit, r/renewable  and r/energy.  

After collection, the texts of each submission were processed according to the following steps:
1. duplicates rows, HTML, Non-letter characters and stop words were removed
2. Words were lemmatized.
3. some words were manually droped like Energy, Renewable and renew to not make our model too simple
4. some words were removed manually from the EDA process like www, https, reddit, np, en, wikipedia, com, org, wiki, youtube, watch and message.

### EDA and Feature Engineering
The list of top words in each subreddit were shown thru EDA. for energy subreddit the top words are solar, oil, power, hydrogen, gas, fuel, year, coal, battery, nuclear, wind, price and plant. for renewable subreddit the top words are solar, power, wind, year, battery, new, storage, cost, like, need, nuclear, plant, fuel, coal and gas. as you can see there are very common words in both subreddits and this make the modeling process harder.
some numeric features like number of comments, the score of submission, word count and character count were produced. also another features like sentiment values and simple class were produced thru feature engineering and used in modeling process.  

### Data Dictionary
|Column|Type|Description|
|---|---|---|
|clean_text|*object (string)*|The processed title after lemmatization and removal of accents, punctuation, capitalization, and stop words.|
|Reddit|*int*|Indicates which subreddit the text came from.<br>1: r/Renewable energy<br>0: r/Energy|
|sentiment|*int*|Indicates the sentiment analyzer value for each text|
|simple_class|*int*|Indicates which subreddit the text came from.<br>1: r/Renewable energy<br>0: r/Energy (it is just a feature that was made by feature engineering)|

 
## Model Evaluation
I got cross-validation and accuracy scores for Logistic Regression (using GridSearch)and KNN models. The logistic regression performed better than KNN with test_accuracy score of 0.65 versus 0.59(auc of 0.66 versus .59) ,so I selected Logistic Regression and also for interpretability.

### Selected Model Details  
**LogisticRegression(solver='liblinear')**  

|Metric|Value|
|-----|-----|
|Training accuracy|87%|
|Testing accuracy|66%|
|Recall / Sensitivity|67%|
|Specificity|67%|


||predicted negative|predicted positive|  
|-----|-----|-----|  
|**actual negative**|2493|1369|  
|**actual positive**|1267|2609|

## Conclusions
This model was able to predict with 66% accuracy whether an article was from r/renewable or r/energy by sumbmissions and comments.Some misclassifications could result from a title containing a word the model associates with the other subreddit. the two subreddits are very similar and this is the reason for small accuracy.

The words that were more likely to be from text in r/renewable energy were hawaii , career, wind, solar, turbine and uk. The words that were more likely to be from text in r/energy were oil, hydrogen, market, shale, saudi, price anad opec .

TFID performed better than count vectorizer in identifying most popular words in each subreddit. since TFIDF keeps the words that are rare in some texts and penalize the words that are very common in texts.

Next steps:

- Take a deeper dive into understanding the misclassified text.
- Try filtering out submissions that were removed from the subreddits.
- Try other supervised moels
- make our own list of stop words

























  
