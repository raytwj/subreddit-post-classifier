![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png)
# Project 3: Application Programming Interface, Natural Language Processing, & Classification Modelling

### DSI-23: Ray Tan

### Executive Summary

A cryptocurrency is a digital currency that is secured by cryptography. Bitcoin and Ethereum are the two largest cryptocurrencies by market capitalization as of this moment. While the top two coins share some similarities, they are also different in many ways. Investors and traders who wish to know more about these two top cryptocurrencies may find it difficult to grasp the many terminologies and jargons used in this field. A natural language processing classifier will be trained on posts from the two respective subreddits. It will learn to identify keywords that are more commonly associated with or are unique to each coin. This will be used to help businesses and enterprises develop an efficient and sophisticated query-answering and routing algorithm for their online chatbot to help handle the large number of enquiries. A total of 6 vectorizer-model combinations were evaluated. The vectorizers considered were Count Vectorizer and Tfidf Vectorizer. The models considered were Multinomial Naive Bayes, K-Nearest Neighbours, and Logistic Regression. Each combination was placed in a pipeline and then passed into a grid search cv. Evaluation of the combinations was conducted using 2 metrics: accuracy and receiver operating characteristic area under curve. All in all, Tfidf Vectorizer-Logistic Regression performed the best. Just on the testing dataset alone, it scored the highest accuracy (0.884) and receiver operating characteristic area under curve (0.950). The top 3 words that predicted a post to be from the Bitcoin subreddit were ‘bitcoin’, ‘btc’, and ‘lightning’. The top 3 words that predicted a post to be from the Ethereum subreddit were ‘ethereum’, ‘eth’, and ‘gas’. With the top words that the classifier has found for each subreddit, a minimum viable product can be designed. In its implementation, this chatbot will pick up on the keywords in a user-submitted message and try to identify whether the query pertains to Bitcoin or Ethereum. It will then give a suitable answer or route the message to the right customer service representative for further management.

### Problem Statement

This project aims to help businesses and enterprises in the cryptocurrency space (e.g. news provider, brokerage platforms, coin vaults, mining pools) develop an efficient and sophisticated query-answering and routing algorithm for their online chatbot to help handle the large number of enquiries received from site visitors on a daily basis and reduce the burden on customer service operatives. The goal is to empower the chatbot to be able to accurately determine the nature of the enquiry and return an appropriate answer; where it is unable to do so, it will categorise the class of the enquiry and route to the relevant operative. For this to happen, the chatbot needs to (for a start) know how to recognise keywords from two well-known cryptocurrencies (Bitcoin and Ethereum) with the help of a natural language processing classifier trained on posts from the two respective subreddits.

### Background & Research

A cryptocurrency is a digital currency that is secured by cryptography. It can be transferred between users or, in certain permitted situations, be exchanged for goods and services. These online transactions are verified and recorded on an online ledger, known as a blockchain, that is enforced by a decentralised network of computers.
([source](https://www.investopedia.com/terms/c/cryptocurrency.asp)) Bitcoin and Ethereum are the two largest cryptocurrencies by market capitalization as of this moment. ([source](https://www.nerdwallet.com/article/investing/cryptocurrency-7-things-to-know)) Bitcoin has been around since 2009 whereas Ethereum was first introduced into circulation in 2015. ([source](https://bernardmarr.com/what-is-the-difference-between-bitcoin-and-ethereum/)) Interest in cryptocurrencies has skyrocketed in recent years, with total fund inflows into cryptocurrency products hitting USD 5.6 billion in 2020, a jump of more than 600% compared to 2019. ([source](https://www.reuters.com/article/us-crypto-currencies-flows-idUSKBN28V2OE)) Most who are new to cryptocurrency would have heard of Bitcoin and Ethereum, as shown by the first question asked in this consumer insights survey on crypto assets. ([source](https://www.oecd.org/financial/education/consumer-insights-survey-on-cryptoassets.pdf)) While the top two coins share some similarities, they are also different in many ways. ([source](https://www.bloomberg.com/news/articles/2021-05-09/bitcoin-and-ethereum-how-are-they-different-quicktake)) Investors and traders who wish to know more about these two top cryptocurrencies may find it difficult to grasp the many terminologies and jargons used in this field. A natural language processing classifier will be used to learn and identify keywords that are more commonly associated with or are unique to each coin so as to lend clarity on the distinctions between the two.

### Data Sources

The following data sources were used:

* [`btc_posts.csv`](../data/btc_posts.csv): Bitcoin Subreddit Posts Dataset

> This dataset contains the attributes of the 5000 most recent posts (as of 22 July 2021) from the bitcoin subreddit [here](https://www.reddit.com/r/Bitcoin/).

* [`eth_posts.csv`](../data/eth_posts.csv): Ethereum Subreddit Posts Dataset

> This dataset contains the attributes of the 10000 most recent posts (as of 22 July 2021) from the ethereum subreddit [here](https://www.reddit.com/r/ethereum/).

### Data Dictionary

A description of the variables seen in the cleaned datasets for analysis is given below:

* [`btc_posts_clean.csv`](../data/btc_posts_clean.csv): Cleaned Bitcoin Subreddit Posts Dataset

| Variable      | Type    | Dataset              | Description                          |
|:--------------|:--------|:---------------------|:-------------------------------------|
| subreddit     | object  | btc_posts_clean.csv  | Subreddit which the post belongs to  |
| post_title    | object  | btc_posts_clean.csv  | Title of the post                    |
| post_content  | object  | btc_posts_clean.csv  | Content of the post                  |

* [`eth_posts_clean.csv`](../data/eth_posts_clean.csv): Cleaned Ethereum Subreddit Posts Dataset

| Variable      | Type    | Dataset              | Description                          |
|:--------------|:--------|:---------------------|:-------------------------------------|
| subreddit     | object  | eth_posts_clean.csv  | Subreddit which the post belongs to  |
| post_title    | object  | eth_posts_clean.csv  | Title of the post                    |
| post_content  | object  | eth_posts_clean.csv  | Content of the post                  |

### Results & Analysis

A total of 6 vectorizer-model combinations were evaluated. The vectorizers considered were Count Vectorizer and Tfidf Vectorizer. The models considered were Multinomial Naive Bayes, K-Nearest Neighbours, and Logistic Regression. Each combination was placed in a pipeline and then passed into a grid search cv to find the optimal collection of hyperparameters. Evaluation of the combinations was conducted using 2 metrics: accuracy and receiver operating characteristic area under curve.

First, cross validation was done on the training dataset for all 6 combinations. Logistic Regression performed the best, followed by Multinomial Naïve Bayes, and then K-Nearest Neighbours. There is no clear winner between a Count-Vectorized model and a Tfidf-Vectorized model.

Next, all 6 combinations were fitted on the training dataset. After grid search cv had found for them the best set of hyperparameters, their performance scores on the training and testing datasets were determined. On both datasets, Logistic Regression was once again the best performer, followed by Multinomial Naïve Bayes, and then K-Nearest Neighbours. However, when the difference between the training and testing accuracy was calculated, K-Nearest Neighbour had the smallest difference, followed by Multinomial Naïve Bayes, and then Logistic Regression. Conversely, the difference between the training and testing receiver operating characteristic area under curve was smallest for Logistic Regression, followed by Multinomial Naïve Bayes, and then K-Nearest Neighbours. There is no clear distinction in performance between a Count-Vectorized model and a Tfidf-Vectorized model on the training and testing datasets.

All in all, Tfidf Vectorizer-Logistic Regression is the combination of choice as it performed the best generally across all the measures of performance. Just on the testing dataset alone, it scored the highest accuracy (0.884) and cross-validated receiver operating characteristic area under curve (0.950).

The top 3 words that predicted a post to be from the Bitcoin subreddit were ‘bitcoin’, ‘btc’, and ‘lightning’. The word ‘bitcoin’ alone had a log odds of 7.53 (i.e. an increase in the word count of ‘bitcoin’ by 1 in the post makes it 1863 times as likely for the post to be from the Bitcoin subreddit than the Ethereum subreddit). This is followed by ‘btc’ which had a log odds of 4.16 (64 times) and ‘lightning’ which had a log odds of 1.52 (4 times). The top 3 words that predicted a post to be from the Ethereum subreddit were ‘ethereum’, ‘eth’, and ‘gas’. The word ‘ethereum’ alone had a log odds of -7.36 (i.e. an increase in the word count of ‘ethereum’ by 1 in the post makes it 6.36e-5 times as likely for the post to be from the Bitcoin subreddit than the Ethereum subreddit). This is followed by ‘eth’ which had a log odds of -6.88 (1.02e-3 times) and ‘gas’ which had a log odds of -2.32 (9.82e-2 times).

### Recommendations & Conclusions

With the top words that the natural language processing classifier has found for each subreddit, a minimum viable product (i.e. a pilot version of the chatbot) can be designed. In its implementation, this chatbot will pick up on the keywords in a user-submitted message and try to identify whether the query pertains to Bitcoin or Ethereum. It will then give a suitable answer or route the message to the right customer service representative for further management.

Outside of the classifier’s ability to be used in the design of a chatbot, the results from this project can also be applied to other domains of cryptocurrency such as in tagging published articles, making search recommendations, auto-correcting or auto-completing terminologies and jargons, and measuring market sentiments of the two coins.

In conclusion, a natural language processing classifier could be trained to accurately distinguish posts from the subreddits of two cryptocurrencies (Bitcoin and Ethereum) that have been chosen for this project. Moving forward, the machine learning could be expanded to include other cryptocurrencies so that organisations will be able to extend support to other coins or tokens and provide a better customer experience. So far, only text data has been analysed. In future, there might also be value in analysing other forms of unstructured data that are not text-based (e.g. pictures, videos, audios) which may also convey powerful predictive clues during a classification task.

### References

https://www.investopedia.com/terms/c/cryptocurrency.asp
https://www.nerdwallet.com/article/investing/cryptocurrency-7-things-to-know
https://bernardmarr.com/what-is-the-difference-between-bitcoin-and-ethereum/
https://www.reuters.com/article/us-crypto-currencies-flows-idUSKBN28V2OE
https://www.oecd.org/financial/education/consumer-insights-survey-on-cryptoassets.pdf
https://www.bloomberg.com/news/articles/2021-05-09/bitcoin-and-ethereum-how-are-they-different-quicktake