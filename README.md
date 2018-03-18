# U008-special-project: 'WeRateDogs' Twitter data

### WranglingSpecial

Real-world data rarely comes clean. Using Python and its libraries, you will gather data from a variety of sources and in a variety of formats, assess its quality and tidiness, then clean it. This is called data wrangling. 

**WeRateDogs** is a Twitter account that rates people's dogs with a humorous comment about the dog. These ratings almost always have a denominator of 10. The numerators almost always greater than 10. 11/10, 12/10, 13/10, etc. Why? Because "they're good dogs Brent." WeRateDogs has over 4 million followers and has received international media coverage.

https://twitter.com/dog_rates

https://help.twitter.com/en/managing-your-account/how-to-download-your-twitter-archive

This archive contains basic tweet data (tweet ID, timestamp, text, etc.) for all 5000+ of their tweets as they stood on August 1, 2017.

The following packages (i.e. libraries) need to be installed. You can install these packages via conda or pip. 
 - pandas
 - numpy
 - requests
 - tweepy
 - json
 
__Task:__ Create interesting and trustworthy analyses and visualizations. The Twitter archive is great, but it only contains very basic tweet information. Additional gathering, then assessing and cleaning is required for "Wow!"-worthy analyses and visualizations.  

__Data01:__ **'Enhanced Twitter Archive'**: The WeRateDogs Twitter archive contains basic tweet data for all 5000+ of their tweets, but not everything. 
 - each tweet's text (which I used to extract rating)
 - rating
 - dog name
 - dog "stage" (i.e. pupper --> puppo --> doggo / ... floofer(fluffy) ) to make this Twitter archive "enhanced." 

Of the 5000+ tweets, I have filtered for tweets with ratings only (there are 2356). I extracted this data programmatically, but I didn't do a very good job. **The ratings probably aren't all correct.** Same goes for the **dog names** and probably **dog stages** (see below for more information on these) too. You'll need to assess and clean these columns if you want to use them for analysis and visualization.

__Data02:__ **'Image Predictions File'**: One more cool thing: I ran every image in the WeRateDogs **Twitter archive** through a neural network that can classify **breeds of dogs**. The results: a table full of image predictions (the top three only) alongside each **tweet ID**, **image URL**, and the **image number** that corresponded to the most confident prediction (numbered 1 to 4 since tweets can have up to four images). for the last row in that table:
 - **'tweet_id'** is the last part of the tweet URL after "status/" → https://twitter.com/dog_rates/status/889531135344209921
 - **'p1'** is the algorithm's #1 prediction for the image in the tweet → golden retriever
 - **'p1_conf'** is how confident the algorithm is in its #1 prediction → 95%
 - **'p1_dog'** is whether or not the #1 prediction is a breed of dog → TRUE
 - **'p2'** is the algorithm's second most likely prediction → Labrador retriever
 - **'p2_conf'** is how confident the algorithm is in its #2 prediction → 1%
 - **'p2_dog'** is whether or not the #2 prediction is a breed of dog → TRUE
 
__Data03:__ **'Additional Data via the Twitter API'**: Back to the basic-ness of 'Enhanced Twitter Archive': **retweet count** and **favorite count** are two of the notable column omissions. Fortunately, this additional data can be gathered by anyone from **Twitter's API**. Well, "anyone" (who has access to data for the 3000 most recent tweets, at least but you, because you have the **WeRateDogs Twitter archive** and specifically the **tweet IDs** within it,) can gather this data for all 5000+. And guess what? You're going to query Twitter's API to gather this valuable data.

> __*Key points__ to keep in mind when data wrangling for this project:
 - You only want original ratings (no retweets) that have images. Though there are 5000+ tweets in the dataset, not all are dog ratings and some are retweets.
 - Assessing and cleaning the entire dataset completely would require a lot of time, and is not necessary to practice and demonstrate your skills in data wrangling. Therefore, the requirements of this project are only to assess and clean at least **8 quality issues** and at least **2 tidiness issues** in this dataset.
 - Cleaning includes merging individual pieces of data according to the rules of tidy data. https://cran.r-project.org/web/packages/tidyr/vignettes/tidy-data.html
 - The fact that the rating numerators are greater than the denominators does not need to be cleaned. This unique rating system is a big part of the popularity of WeRateDogs.
 - You do not need to gather the tweets beyond August 1st, 2017. You can, but note that you won't be able to gather the image predictions for these tweets since you don't have access to the algorithm used.

*Fun fact: creating this neural network is one of the projects in Udacity's Machine Learning Engineer Nanodegree program and Artificial Intelligence Nanodegree program.


## Your tasks in this project are as follows:

 - Data wrangling, which consists of:
   - Gathering data
   - Assessing data
   - Cleaning data
 - Storing, analyzing, and visualizing your wrangled data
 - Reporting on 1) your data wrangling efforts and 2) your data analyses and visualizations


### A) Gathering each of the 3 pieces of data

__1. The WeRateDogs Twitter archive:__ 
 - can imagine it as a file on hand. ('twitter_archive_enhanced.csv')

__2. The tweet image predictions:__ i.e., what breed of dog (or other object, animal, etc.) is present in each tweet according to a neural network. This file ('image_predictions.tsv') is hosted on Udacity's servers and should be downloaded programmatically using the **Requests library** and the following URL: https://d17h27t6h515a5.cloudfront.net/topher/2017/August/599fd2ad_image-predictions/image-predictions.tsv

__3. Each tweet's retweet count and favorite ("like") count at minimum, and any additional data you find interesting:__ Using the **tweet IDs** in the **WeRateDogs Twitter archive**, query the Twitter API for each tweet's JSON data using Python's **Tweepy library** and store each tweet's entire set of JSON data in a file called **tweet_json.txt** file. Each tweet's JSON data should be written to its own line. Then read this .txt file line by line into a pandas DataFrame with (at minimum) **tweet ID, retweet count, and favorite count**. 

Note: do not include your Twitter API keys, secrets, and tokens in your project submission.

### B) Assessing data
After gathering each of the above pieces of data, assess them visually and programmatically for **quality** and **tidiness** issues. Detect and document at least eight (8) quality issues and two (2) tidiness issues in your wrangle_act.ipynb Jupyter Notebook. To meet specifications, the issues that satisfy the Project Motivation (see the Key Points header on the previous page) must be assessed.

### C) Cleaning data
Clean each of the issues you documented while assessing. Perform this cleaning in wrangle_act.ipynb as well. The result should be a high quality and tidy master pandas DataFrame (or DataFrames, if appropriate). Again, the issues that satisfy the Project Motivation must be cleaned.

### D) Storing, Analyzing, and Visualizing Data
Store the clean DataFrame(s) in a CSV file with the main one named **twitter_archive_master.csv**. If additional files exist because multiple tables are required for tidiness, name these files appropriately. Additionally, you may store the cleaned data in a SQLite database (which is to be submitted as well if you do).

Analyze and visualize your wrangled data in your wrangle_act.ipynb Jupyter Notebook. At least **three (3) insights and one (1) visualization** must be produced.


### How to Query Twitter Data
Use **Tweepy** library to query Twitter's API for additional data beyond the data included in the WeRateDogs Twitter archive. This additional data will include **retweet count** and **favorite count**. Some APIs are completely open, like **MediaWiki** (accessed via the **wptools** library). Others require authentication. The Twitter API is one that requires users to be authorized to use it. This means that before you can run your API querying code, you need to set up your own Twitter application. ( https://www.slickremix.com/docs/how-to-get-api-keys-and-tokens-for-twitter/ ) you must sign up for a Twitter account. * Once you have these set up, the following code, which is provided in the "Getting started" portion of the tweepy documentation, ( https://media.readthedocs.org/pdf/tweepy/latest/tweepy.pdf ) will create an API object that you can use to gather Twitter data.


