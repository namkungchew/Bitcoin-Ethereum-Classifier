# Project 3: 
# Bitcoin - Ethereum Post Classifier

## Table of Contents:

1. Background
1. Problem Statement
1. Executive Summary
1. Data Cleaning
1. Models
    1. Preprocessing
    1. Different Combinations of Vectorizers and Classifiers
    1. Fine tuning and selecting final model
    1. Final Choosen Model: CountVectorizer with MultinomialNB
1. Conclusion and Recommendations
1. References and Data Sources

## 1. Background
Our stalkholder is a cryto exchange platform which offer trading for Bitcoin and Ethereum. They are interested to monitor the posts on their user discussion forum and divide the posts into Bitcoin / Ethereum posts so as to identify which crytocurrency is generating greater interest.

---
## 2. Problem Statement
We are tasked with building a model to identify and classify the posts into Bitcoin or Ethereum posts. We decided to train our model using posts on Reddit on the subtopics Bitcoin and Ethereum.

---
## 3. Executive Summary

---
## Data Dictionary

---
## 6. Conclusion and Recommendations
|             | CountVectorizer with MultinomialNB | Tfidf Vectorizer with Logistic Regression | CountVectorizer with RandomForestClassifier |
|-------------|------------------------------------|-------------------------------------------|---------------------------------------------|
| Params      | 'cvec__max_df': 0.2                |  'tfidf__max_df': 0.2                     | 'cvec__max_features': 1000                  |
|             | cvec__max_features': 1000          | 'tfidf__max_features': 1000               |  'cvec__ngram_range': (1, 2)                |
|             | cvec__min_df': 2                   | tfidf__min_df': 3                         | rt__max_depth': 35                          |
|             | cvec__ngram_range': (1, 1)         | 'tfidf__ngram_range': (1, 2)              | 'rt__min_samples_leaf': 1                   |
|             | nb__alpha': 0.4                    | ''lr__C': 1,                              |                                             |
| Train Score | 0.881                              | 0.901                                     | 0.897                                       |
| Test Score  | 0.845                              | 0.823                                     | 0.795                                       |

Recap: We tried various models. Logistic Regression produce pretty consisent accuracy. Multinominal Naive Bayes worked the best. K Nearest Neighbours Classifier doesn't seem to perform well. Random Forest Classifier is around the same accuracy as Logistic Regression but still not better than Multinominal Naive Bayes. HashingVectorizer doesn't give much benefit and have more disadvantages for this dataset. We tried to fine tune 3 model: Model 2: MultinominalNB with CountVectorizer, Model 4: LogisticRegression with TfidfVectorizer and Model 10: Random Forest with CountVectorizer.

One of the challenges we face during the course of this project is that our models overfit most of the times and we have to find ways and trying different hyperparameters to prevent the model from overfitting without sacrificing accuracy. For our final 3 models, we discover that Multinominal respond best to our efforts to prevent overfitting. It was able to increase accuracy of the test score while minimizing the difference between our train and test score to around 4% and improving our cross val score. We find it hard to prevent overfitting on the Random Forest model as once we limit the max depth or increase the minimum sample leaf, our test score dropped drastically from 0.82 to 0.795. For the Logistic Regression model, we managed to reduce to 8% difference between the train and test score and still achieve 0.82 test score.

We choose Multinominal Naive Bayes with CountVectorizer as our final model as it is the model that still maintain its highest accuracy score and also is not overfitted. Also it is the fastest to tune and compute over GridSearchCV. Our best params are the following: 'cvec__max_df': 0.2, 'cvec__max_features': 1000, 'cvec__min_df': 2, 'cvec__ngram_range': (1, 1), 'nb__alpha': 0.4

We are satisfied with our results that it 84.5% accurate which beat the baseline accuracy by 24.8% and is better than the other models by 2-3%. Also the train score and test score are not significantly different thus not overfitting. This meet our goal of being able to differentiate and classify posts into Bitcoins posts and Ethereum posts reasonably well. We also resonate with the most important features in this model and they are similar with the most important features in other models as well. A look at the posts which are misclassified show these posts mainly outliers which are either spam or didn't belong to either classes which we cannot differentiate with our human brains either. 

Going forward, since most of our models show overfitting due to the larger number of features to our dataset, we can improve our accuracy by gathering more data given time and refitting it to our model and relaxing some of the hyperparameters used to control the overfitting.
