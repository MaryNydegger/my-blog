---
Layout: post
Title: "Movie Review Wording"
Author: Mary Nydegger
Description: Sentiment Analysis of Movie Reviews 
image: "/assets/images/MovieReview.png"

date: 2023-12-18 10:00:00
---

### Table of Contents
- [Synopsis](#synopsis)
- [My Experiment](#My-Experiment)
- [Key Findings](#Key-Findings)
    - [Wording](#Wording)
    - [Logistic Regression Model](#Logistic-Regression-Model)
    - [Random Forest Model](#Random-Forest-Model)
- [Implications and Learnings](#Implications-and-Learnings)
- [Looking Ahead](#Looking-Ahead)
- [Ethical Considerations](#ethical-considerations)

## Synopsis
In machine learning, optimizing model performance often involves tweaking various knobs and analyzing data from different angles. I recently did a prohect diving into the impact of hyperparameter tuning and sentiment analysis on predictive models. Here is a peek into what I discovered and the implications it holds. 

## My Experiment 

I focused on using two popular supervised models: Logistic Regression and Random Forest. I wanted to understand how these models responded to hyperparameter tuning and the incorporation of sentiment analysis scores. I found a dataset of a ton of movie reviews - both positive and negative. I did the sentiment analysis from this dataset.

## Key Findings

### Wording
I first looked at the components that made up a negative or positive review, and it was very interesting because the words that were most commonly used in both reviews did not differ very much. This first graph shows the 10 most used words in both reviews (removing the common stop words), and they are practically the same. 

![WordingPositive]({{site.url}}/{{site.baseurl}}/assets/images/WordingBars.png)
![WordingNegative]({{site.url}}/{{site.baseurl}}/assets/images/WordingBarsNegative.png)

Moving further into the analysis, I used dimension reduction to view these components more and see if there were further patterns or clusters. Surprisingly there wasn't.

![DimensionReduction]({{site.url}}/{{site.baseurl}}/assets/images/DimensionReduction.png)

In viewing this graph, you simply want to see if the colors cluster into different groupings or not. Each color supports the different components of positive vs. negative sentiment. There is a lot of overlap between the yellow and purple dots and not any specific clusters. 

Both of these visualizations support each other. There are plenty of separate positive and negative reviews, but the main types of wording in both of them don't differ substantially. 

### Logistic Regression Model
The logistic regression model is known for its simplicity. When looking at how it performed, it showed consistent accuracy even when subjected to hyperparameter tuning. 

Both of these chunks of code outputted a validation accuracy of **0.8764**

``` py
logistic = LogisticRegression()
logistic.fit(X_train, y_train)
logistic_val_pred = logistic.predict(X_val)
accuracy_logistic = accuracy_score(y_val, logistic_val_pred)

print("Logistic Regression - Validation Accuracy:", accuracy_logistic)
```

``` py
logistic_params = {'C': [0.1, 1, 10], 'solver': ['liblinear', 'lbfgs']}
logistic = LogisticRegression()
logistic_grid = GridSearchCV(logistic, logistic_params, cv=5, scoring='accuracy')
logistic_grid.fit(X_train, y_train)
best_logistic_params = logistic_grid.best_params_
best_logistic_score = logistic_grid.best_score_
logistic_best = logistic_grid.best_estimator_
logistic_val_pred = logistic_best.predict(X_val)
accuracy_logistic = accuracy_score(y_val, logistic_val_pred)
```

Introducing the sentiment analysis scores also showed a minor impact on the model. This showed the limited influence of sentiment in the specific context of our study.

### Random Forest Model
Performing differently than the logistic regression model, the random forest model shwoed more of a leap in accuracy post-tuning, hinting at its sensitivity to parameter adjustments. 

This first chunk of code (without hyperparameter tuning) outputted an accuracy of **0.8376**

``` py
random_forest = RandomForestClassifier()
random_forest.fit(X_train, y_train)
random_forest_val_pred = random_forest.predict(X_val)
accuracy_rf = accuracy_score(y_val, random_forest_val_pred)

print("Random Forest - Validation Accuracy:", accuracy_rf)
```

And this chunk of code (with hyperparameter tuning) outputted an accuracy of **0.8444**

``` py
rf_model = RandomForestClassifier()
rf_params = {'n_estimators': [100, 200, 300]}
rf_grid = GridSearchCV(rf_model, rf_params, cv=5)
rf_grid.fit(X_train, y_train)
best_rf_model = rf_grid.best_estimator_
rf_accuracy = best_rf_model.score(X_val, y_val)

best_rf_params = rf_grid.best_params_
best_rf_score = rf_grid.best_score_
random_forest_best = rf_grid.best_estimator_
random_forest_val_pred = random_forest_best.predict(X_val)
accuracy_rf = accuracy_score(y_val, random_forest_val_pred)
```

## Implications and Learnings
The consistent performance of the logistic regression model hinted at its robustbess to hyperparameter changes while the improved accuracy of random forest post-tuning highlighted its potential for better performance with careful parameter selection. 

However, limitations such as dataset size, assumptions in preprocessing, and the nuances of sentiment analysis shouldn't be overlooked. Understanding these constraints is super important when looking at future research and enhancing model robustness.

## Looking Ahead
In moving ahead with this project and further analysis, I am looking into collecting more diverse data to enhance model generalizations, diving into more advanced sentiment analysis techniques for deeper insights, and exploring more sophisticated models for heightened predictive power. 

This project helped me to see the relationships between model behavior and tuning, emphasizing the importance of thoughtful model selection, feature engineering, and understanding the context for effeective problem solving in the realm of machine learning. 

I would be interested to webscrape from other websites of movie reviews and running it through this code in a similar way to see if the results would mirror these results. I would hope and expect that there would be a difference in the wording of the positive and negative reviews as well as further insights from the sentiment analysis.


### Ethical Considerations

All data used was publicly made available. My dataset was made available from Stanford - where they posted a large dataset of both positive and negative reviews so anyone could run a sentiment analysis on it. 

* *Dataset source*: [https://ai.stanford.edu/~amaas/data/sentiment/]
* *Citing*: @InProceedings{maas-EtAl:2011:ACL-HLT2011,
  author    = {Maas, Andrew L.  and  Daly, Raymond E.  and  Pham, Peter T.  and  Huang, Dan  and  Ng, Andrew Y.  and  Potts, Christopher},
  title     = {Learning Word Vectors for Sentiment Analysis},
  booktitle = {Proceedings of the 49th Annual Meeting of the Association for Computational Linguistics: Human Language Technologies},
  month     = {June},
  year      = {2011},
  address   = {Portland, Oregon, USA},
  publisher = {Association for Computational Linguistics},
  pages     = {142--150},
  url       = {http://www.aclweb.org/anthology/P11-1015}
}



If you are interested in checking out my code and the data I used, you can find it in my [github repository](https://github.com/MaryNydegger/486-SemesterProject.git) .
