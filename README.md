# Twitter_Archive_Investigation

**Introduction**

This project is about wrangling data from Twitter account "WeRateDogs" and analyzing the wrangled data. In this project, I analyzed the data from archive of Twitter account, tweet image predictions, and additional data from Twitter's JSON data. 

**What do you need to install?**

Python and its libraries:

1. Pandas
2. Numpy
3. Requests
4. Matplotlibs
5. Twitter's Tweepy 

I recommend using Anaconda and Jupyter Notebooks to work on the project. To query Twitter API, you need to create a Twitter's Developer account
and follow these steps:
* You will be guided through the steps, and asked to describe in your own words what you are building. 
* If you are asked for an app name, it can be anything appropriate, and if you’re asked for a Website URL, it can be anything in a standard URL format. You can do the same with other requested URLs, or perhaps leave them blank.
* You can then go to the Keys and Tokens tab on this page to find or generate the Consumer API keys, and the Access Token and Access Token Secret that you will need.

**Process**

**Part I. Data Gathering**

First, I used Python and its libraries to gather data from the tweet archive of Twitter account "WeRateDogs"(twitter_archive_enhanced.csv) and data of tweet image predictions (image_predictions.tsv) according to a neural network. Then, I gathered additional data, such as each tweet's retweet counts and favorite counts, by querying Twitter API for each tweet's JSON data. After that, I stored the entire JSON data into tweet_json.txt.I read the files twitter_archive_enhanced.csv, image_predictions.tsv using Pandas and store them into df and df2 correspondingly. I created a dataframe df3 based on the .txt file to put tweet id, retweet counts, and favorite counts.

**Part II. Data Assessing**

First, I applied functions to all three tables and found some quality issues. I applied .info() function for each of three dataframes and found that df has missing values for in_reply_to_status_id, in_reply_to_user_id, retweeted_status_id, retweeted_status_user_id, retweeted_status_timestamp, and expanded_urls columns. I also found that timestamp and retweeted_status_timestamp have wrong datatypes. Next, I applied .describe() function and found that not all rating_denominator equals to 10. Then, I looked at df rows that has no expanded_urls and found that most of them are replies to the original tweets. I also looked at the names in df and found that there are some dogs that has no names or wrong names. I checked tweet_id for all three tables and did not find duplicates. Finally, I checked the structure for each table and found two tidiness issues: dog stages were separated into four columns, and all three tables contain the same column "tweet_id". I recorded the issues and move on to data cleaning step.

**Part III. Data Cleaning**

I made copies for each of the three dataframes. For quality issues, I cleaned for missing values first. I dropped in_reply_to_status_id, in_reply_to_user_id columns. Since the project requires only original ratings. I located the rows that have values in retweeted_status_id column and dropped all these rows. After that, I dropped retweeted_status_id, retweeted_status_user_id, retweeted_status_timestamp columns. I dropped rows that do not have expanded_urls as I am not able to obtain this part of data. Next, I dealt with wrong data type issue. I converted timestamp column in df_clean to datetime data type. Then, I cleaned for rating_denominator that has values other than 10. I extracted correct ratings from the text and replace the wrong ratings. After that, I extracted real names from text and replace the wrong names with real names. I went back to dog ratings and dropped rows that not about real dog ratings. Finally, I went to df2_clean table and unified the dog breeds to lower case letters. For tidiness issues, I went to df_clean table and melted the doggo, puppo, pupper, and floofer columns to a stage column. Then, I combined all three tables into one table called df_master using "tweet_id" as my primary key.
I stored df_master table to a csv file called "twitter_archive_master.csv".

**Part IV. Data Analyzing**

Since dog has four stages (doggo, puppo, pupper, floofer) according to WeRateDogs, I divided the final data into four groups and investigated the characteristics for each dog stage. First, I am interested in which dog stage gets the highest and the lowest average rating.
I first calculated the average rating for each tweet because some tweets have posted multiple dogs while others have one, and it is hard to compare them together. Then I calculated the mean rating for each dog stage and created a bar chart.
Next, I wanted to investigate if the dog stage that gets the highest rating have the most favorite counts. I calculated average favorite counts for each dog stage and created a bar chart.
Finally, I was curious about how precise is our neural network to predict dog breeds. I checked each prediction and saw if it predicted correctly on the first try, or the second try, or the third. 
