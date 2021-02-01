
# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Project 3: Web Scraping & APIs

### Problem Statement

In this study, I will use Naive Bayes and Random Forest models to classify posts in the Audio Engineering and Songwriting Subreddits, with the goal of helping a beginner songwriter and recordist determine where to find the most relevant and helpful information for their learning process.

With the leaps in accessible audio recording technology over the past decade, more young musicians are starting to both write and record their own music. In my experience, it’s more financially viable to learn to record yourself. However, there’s a steep learning curve, and learning from the experience of decades of recording and songwriting wisdom available online is a huge help.

Success will be evaluated based on my model's accuracy, or rate of correct predictions.


---
### Background Research

I've spent the last 15 years writing, producing, and recording music, and over that time, I came to learn two very important things: first, there's a wealth of valuable information available on the internet; and second, there's a wealth of misleading, not-so-valuable information on the internet. [Reddit](https://www.reddit.com) (and its many Subreddits) is an excellent source for both the valuable information and the not-so-valuable information. As someone who's navigated this tricky territory, I'd love to create a tool to help guide young songwriters and recordists to positive, trustworthy online communities where they can learn and develop their craft.


I chose to explore posts and build my **Multinomial Naive Bayes** and **Random Forest** classification models based on the following Subreddits:
* [r/audioengineering](https://www.reddit.com/r/audioengineering/): A community of audio engineers, technicians, builders, and musicians focused on providing tips and tricks for the amateur-to-professional recordist.
* [r/Songwriting](https://www.reddit.com/r/Songwriting/): A community of songwriters, musicians, and recordists focused on providing tips for writing music and feedback on original music.
---
### Contents
* **Notebook 1** | *01_r_audioengineering_processing*: Audio Engineering dataframe creation and cleaning.
* **Notebook 2** | *02_r_songwriting_processing*: Songwriting dataframe creation and cleaning.
* **Notebook 3** | *03_basic_eda*: EDA on token distribution and sentiment analyses for both Subreddits.
* **Notebook 4** | *04_eda_and_modeling*: Contains merged dataframe comprised of both Subreddits, and all models I created, including multiple iterations of Multinomial Naive Bayes and Random Forest.
* **Notebook 5** | *05_final_model_and_conclusions*: My final, best performing model, accompanied by my problem statement, brief background on the project's scope, and my conclusions.

---
### Analysis Summary

In the course of this project, I scraped 10,000 posts from Reddit - half from the Audio Engineering Subreddit, and half from the Songwriting Subreddit. My scrape focused on both title text and body text, but not comments beneath posts. To make modeling and processing my data easier, I engineered a feature in my dataframes, `full_post`, that amounted to the combined title and body text of each individual post.

Before merging the cleaned dataframes representing each of my Subreddits, I used Natural Language Toolkit's `SentimentIntensityAnalyzer` (which uses the `VADER` lexicon to score the emotion behind text on a scale of -1 to +1) to analyze the general compound sentiment scores of each Subreddit. Both scores suggested that the Subreddit communities I chose are largely positive communities - something essential for any aspiring songwriter or recordist - with mean compound sentiment scores between about 0.3 and 0.5.

After cleaning my individual dataframes for each Subreddit and running sentiment analysis, I merged the two dataframes, binarized my Subreddits, and created a dataframe consisting of my full post text and the corresponding Subreddit. From there, I was able to train-test-split my data, then use `CountVectorizer` and `TfidfVectorizer` transformers to transform my text data for model processing.

I used Multinomial Naive Bayes and Random Forest classification models, along with SciKit-Learn's `Pipeline` and `GridSearchCV` to then pass my tokenized text data through multiple iterations of each model. Taking advantage of pipelines and grid searching allowed me to test and tune multiple hyperparameters of each model simultaneously. Once I'd optimized each model, finding the best values for each parameter, I ran that model on my training and testing data. In Notebook 5, I displayed my best model.

---

### Conclusions & Considerations

- Fundamentally, my Multinomial Naive Bayes model performed quite well on unseen data. Some considerations for scaling this model would be observing posts over a longer span of time, looking at trends in most frequent posters in each community, and examine the level of community interaction generated by each post.
- I was surprised to see how well my model differentiated between the Audio Engineering and Songwriting Subreddits - it correctly predicted which forum the post came from at a rate of 95.6%, well above the 51% baseline accuracy. I assumed there would be much more crossover in terminology, and while there is some, the audiences appear fairly different, at least in how they speak about their respective topics.
- Both forums are, socially speaking, positive communities based on sentiment analysis (Notebook 3). The Audio Engineering Subreddit had a slightly higher compound sentiment score of 0.488 (based on the mean compound sentiment generated with nltk's `SentimentIntensityAnalyzer`). The Songwriting Subreddit also skewed positive, with a mean compound sentiment score of 0.327. Though the `SentimentIntensityAnalyzer` and `VADER` lexicon aren't perfect, these scores do suggest that both communities  post predominantly positive content. Positivity is a huge plus when learning something new, so I'm happy to see these results! Comments on posts were not considered in these scores, though I'd like to in a future version of this project, as I believe they could significantly impact these scores.
- My misclassification rate was very low, based on my confusion matrix in Notebook 5. This is confirmed by my model's accuracy score on unseen data of 95.6%.
- Given more time, I'd like to scrape more posts, including the comments on these posts, and see how that changes my model. While the original posts are all fairly positive, and are generally either seeking help or offering wisdom, I'm sure the comments have a wider range of sentiments, and so, may produce an interesting effect on my model.


**Actions**

- Let's expand this to more Subreddits! The more communities I pull from, the more my model can grow, and the better it can help direct beginners to the best Subreddit for their needs and goals.
- I'd like to scrape, and perform similar analysis on more "official" sources for recording and songwriting, such as [TapeOp](https://tapeop.com/) and [Sound On Sound](https://www.soundonsound.com/).

---

### Sources Cited:
* [r/audioengineering](https://www.reddit.com/r/audioengineering/)
* [r/Songwriting](https://www.reddit.com/r/Songwriting/)
* [TapeOp](https://tapeop.com/)
* [Sound On Sound](https://www.soundonsound.com/)
* [Pushshift API](https://github.com/pushshift/api)
* Riley Dallas on [YouTube](https://www.youtube.com/watch?v=AcrjEWsMi_E&feature=youtu.be)
