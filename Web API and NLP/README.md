# A Tale of Two Subreddits : Using Web APIs & NLP

### Problem Statement:

   What are the similarities and difference between the two subreddit and if given a word or set of words, using machine learning modeling, predict which subreddit it should be posted on.

#### Background:

Reddit is a social news aggregation, web content rating, and discussion website, recently including livestream content through Reddit Public Access Network. Registered members submit content to the site such as links, text posts, and images, which are then voted up or down by other members. (Wikipedia)

For the reaching the goal, I picked two subreddits. /r/Coffee is a reddit page, known as subreddit, where people discuss or follow discussions that is related to Coffee. r/Tea is the subreddit for discussions about tea.

#### Goals:

   1. Using Pushshift's API, collect posts from two subreddits: r/Coffee and r/Tea
   2. Use NLP to train a classifier on which subreddit a given post came from.

   ### Description of data

   #### Source:

   Pushshift's API can be use for webscrapping subreddit pages with a limit of 100 posts per run. You can find all raw scrapped data in subreddit1 and subreddit2 folders.
   
   For r/Coffee, (https://www.reddit.com/r/Coffee), I used the following url: https://api.pushshift.io/reddit/search/submission?subreddit=coffee then created a helper function for webscrapping the r/Tea page.

   I gathered data using request and global library for each subreddit and created dataframes for exploratory data analysis on which I later combined into one dataset for machine learning modeling and evaluation.

   SUBREDDIT1.csv and SUBREDDIT2.csv are data from r/Coffee and r/Tea respectively with 3500 rows each, which are individual updated text posts, and 6 features gathered approximately around Mar 04 2021 19:17:07 GMT-0800 (Pacific Standard Time). 

   #### Target:


   Binary classification problem that uses Natural Language Processing to train a classifier to answer on which subreddit a given post came from. Please see code notebook at API_NLP_Classifiers_Notebook.ipnyb



   #### Data Dictionary:

The final processed data ready for modeling excludes posts only from unique users and not missing selftext post to prevent bias between dataframes. I also excluded posts that are removed or have deleted author name as well as posts from AutoModerator to capture unique users of both pages.


   * Coffee DataFrame

   | Feature      | Description | Size    |
   | :---        |    :----:   |          ---: |
   | subreddit     | Name of the subreddit channel of where the data has been pulled       | 1 value = Coffee  |
   | title   | Title of a post on subreddit        | String of Text      |
   | selftext   | Body of a post        | Strings that can include one letter upto paragraphs    |
   | statuswordcount   | Word count of selftext after tokenizing        | int      |
   | raw_text   | Preprocessed words ready for modeling        | list of strings      |

   * Tea DataFrame

   |Feature      | Description | Size    |
   | :---        |    :----:   |          ---: |
   | subreddit     | Name of the subreddit channel of where the data has been pulled       | 1 value = Tea  |
   | title   | Title of a post on subreddit        | String of Text      |
   | selftext   | Body of a post        | Strings that can include one letter upto paragraphs    |
   | statuswordcount   | Word count of selftext after tokenizing        | int      |
   | raw_text   | Preprocessed words ready for modeling        | list of strings      |


   * Data DataFrame

   | Feature      | Description | Size    |
   | :---        |    :----:   |          ---: |
   | raw_text      |Preprocessed words ready for modeling      | list of strings   |
   | subreddit   | Name of the subreddit channel of where the raw_text was from |2 values = Coffee or Tea |
   
   ### Modeling
   
   I used NLP methods for data processing such as removal of special characters, tokenization, lemmatizing, and stop word removal. I used a combined data, after cleaning, from both subreddits with equal number of rows to prevent bias and split that data into training and test datasets on which I can use for training and evaluating the classifier models.


   #### Performance on training/test data
   Below are some of the classifier models that I ran for this project. I picked the Multinomial Naive Bayes classifier to optimize because it has the best performing score. Please see API_NLP_Classifiers_Notebook.ipnyb for more information.

   | Model      | Training Accuracy Score    | Testing Accuracy Score    |
   | :---        |    :----:   |          ---: |
   | Random Forrest Classifier      | 95.01%       |94.35% |
   | Extra Trees Classifier   | 94.12% | 92.94%|
   | Multinomial Naive Bayes Classifier      |98.38% |95.76%|



   #### Primary findings



   Top 15 Common Words After Stop Word Filter and removing "Coffee" and "Tea" for comparison.

   | r/Coffee | r/Tea    |   Both subredddits
   | :---    |    :----:   |           ---: |
   | water       |water   | water |
   | beans        | loose-leaf      |  use|
   | grinder       | time   | time|
   | use        |taste| cup |
   | espresso        | tried      | grinder |
   | time       | love  | make |
   | cup        | drink     | brew  |
   | machine       | use  | want |
   | brew        |find   |looking |
   | make       |thanks |taste |
   | want        |make | tried |
   | new        |different | thanks |
   | pour        |even | first |
   | taste        |got | new |
   | thanks        |brew | got |



   Users

   |      | r/Coffee | r/Tea    |
   | :---        |    :----:   |          ---: |
   | Unique Users      |  2026      |  1287  |
   | Max Post of a User      |   60     |   10 |
   | Min Post of a User      |   1     |   1 |
   | Average Post per User   |   1.149   |   1.26    |
   | Average Word Counts per Post   |   115.54     |  84.43     |
   
   In addition on the data above, I spent some time on both subreddit pages and discovered that most r/Tea recent posts includes photos which were not captured by API. This is an additional insight on the culture of the page that added context to the data pulled.



   #### Conclusions

   r/Coffee members posts more discussions, suggestions, and questions and r/Tea posts more photos. r/Tea users also posts emotion words like “love” and “thanks” where r/Coffee users more on coffee-related words. There are plenty of common words that has similar meaning in both pages including “brew”, “looking”, and “want".Both pages mainly talks about coffee and tea drinks that includes preparation, suggestions, and stories the difference is r/Tea users uses emotion words on their posts while r/Coffee users are mainly focused on coffee.


   As for Machine Learning modeling with NLP, for this project, the Multinomial NB Classifier performed better than the rest of the other classifiers because I optimized it by using the best parameters on Pipeline and Gridsearch. Scores above shows some overfitting that happened but still acceptable.

   ### Next steps

Looking forward on working with strings (n_grams) to get more context and insights from the users of each subreddit. Then I plan on setting a more subreddit channel focused stop word dictionary to be able to filter the data better. I'm also considering to extract emojis and explore some quotations marks that might be used to change the tone of the posts as this can change the context of the string.
