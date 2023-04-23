# SC1015: Data Science Mini Project - Phishing URL Detection
School of Computer Science and Engineering
Nanyang Technological University
Lab: B135
Group: 9

Members:
1. Ng Yoon Yik (@Hungr-yy)
2. Karen Lee Sze Suen (@leekaren580)
3. Chee Zheng Rong （@sheeshzr)

This repository contains all the Jupyter Notebooks, datasets, images, video presentations, and the source materials/references used and created as part of the Mini Project for SC1015: Introduction to Data Science and AI. The project undertaken is the detection of Phishing URLs.

This README outlines what we have accomplished in this project. If you want a more detailed explanation, please refer to the the Jupyter Notebooks in this repository in tandem with this README and the video. They contain more in-depth descriptions and smaller details which are not mentioned here in the README. For convenience, we have divided the notebooks into 5 parts which broadly relate to the 5 main sections of this project.

## Table of Contents:
1. Problem Formulation
2. Data Preparation and Cleaning
3. Exploratory Data Analysis
4. Models 1
5. Model 2
6. Model 3
7. Model 4
8. Model 5
9. Data Driven Insights and Conclusion
10. References

## 1. Problem Formulation
**Question:** Can we detect phishing websites from benign ones using their respective URLs?

**Datasets:**
1. [Phishtank (retrieved on 17-4-23)](https://phishtank.org/developer_info.php)
2. [Hannousse, Abdelhakim; Yahiouche, Salima (2021), “Web page phishing detection”, Mendeley Data, V3](https://data.mendeley.com/datasets/c2gw7fy2j4/3)
3. [The Majestic Million (retrieved on 10-4-23)](https://majestic.com/reports/majestic-million)
4. [Phishing site URLs Dataset on Kaggle](https://www.kaggle.com/datasets/taruntiwarihp/phishing-site-urls)
5. [JPCERT Coordination Center (Directly downloaded due to some antviruses removing it as a threat)](https://github.com/JPCERTCC/phishurl-list)
6. [Malicious URLs Dataset on Kaggle](https://www.kaggle.com/datasets/sid321axn/malicious-urls-dataset)

**Rationale**: As the amount of money lost by scam victims in Singapore have increased, and phishing scam are the most common method of attack, we believe that this project is relevant to everyone in Singapore. Our project targets the analysis of the website solely from the features of its URL. By learning the kinds of features of URLs that indicate a possible phishing website, we might be able to form insight into a more accessible way for potential scam victims to identify phishing URLs without the need for any technology, and empower them to protect themselves.

## 2. Data Preparation, Cleaning, Feature Engineering

In this section of our project we prepared, cleaned and combined our 6 datasets to help us in data analysis and for the purpose of machine learning in the later sections.

We performed the following:
1. **Merging of datasets:** We removed features not relevant to our project, labelled them as Phishing/Benign URLs and merged the 6 datasets together.
2. **Feature Engineering:**  We also employed feature engineering to find out what interesting features a URL has that might differ between benign and phishing URLs.

## 3. Exploratory Data Analysis

We explore our variables both categorical (`4` in total) and numerical (`13` in total) that are related to the features of each website's URL. What is their relationship with respect to variable phish(whether or not a URL is a phishing URL or benign). Are there any patterns we can notice? What is the underlying relationship between them? Can we make any inferences for our question through EDA? This is will help us in the later sections of our project and answer the question posed.

1. **Class Analysis:** We observed the distribution of Phishing and Benign URLs and observed that out dataset is relatively balanced.
2. **Exploratory Analysis of Numerical Variables:** We found out that the top 3 numerical variables are `count.`, `count_dir` and `hostname_length`, as they have features that differ between phishing and benign URLs.
3.**Categorical Variables:** We used observed that based n bar graphs and using Chi-squared test values, `uses-http` and `uses-https` have features that differ between phshing and benign URL and might be useful for our models later on.

## 4. Model 1

We chose to use Decision Trees as our model to classify the phishing/benign URLs.

We performed the following:
1. **K-fold Cross Validation:** We explored the impact of decision trees on our individual features. One interesting observation was that the variables highlighted to be potentially useful during our EDA process also had the highest cross validation scores. We also showed that a combination of our features gave a better score than the individual features w.r.t. using decision trees.
2. **Decision Tree Model:** We fit our data into our decision tree model and obtained an accuracy of `0.8547` and F1 Score of `0.85`

## 5. Model 2

We then chose to use Random Forest, following our successes in utilizing decision trees.

We performed the following:
1. **Random Forest Model:** We fit our data into our decision tree model and obtained an accuracy of `0.8513` and F1 Score of `0.85`
2. **Parameter Tuning:** We used K-fold cross-validation and randomizedsearch in order to tune our parameters for Random Forest. Our modified Random forest model yielded an accuracy of `0.8593` and F1 Score of `0.86`

In conclusion, we managed to improve our Random Forest model by tuning its parameters, and subsequently outperformed our Decision Tree Model

## 6. Model 3

We then decided to explore a different model, Logistic Regression, in order to distinguish between Phishing/Benign URLs

1.**Cross Validation Score:** We performed k-fold cross validation to estimate the average performance of the model and got a mean score of `0.81`.
2.**Logistic Regression Model:** We fit our data into our Logistic regression model and obtained an accuracy of 0.8166 and F1 score of `0.81` This significantly lower performance discourages us to go further with the model.

To conclude, although there is no indication of overfitting (as train and test accuracy is similar, the model might perform better with other variables (or combination of). A remedy to model performance would be to test other combinations of variables.

## 7. Model 4.

We thus continued to progress with models related to decision trees and thus we chose XGBoost as our 4th model.

We performed the following:
1. **XGBoost Model:** We fit our data into our  model and obtained an accuracy of `0.8588`
2. **Parameter Tuning:** We used K-fold cross-validation and randomizedsearch in order to tune our parameters for Random Forest. Our modified Random forest model yielded an accuracy of `0.8592` and F1 Score of `0.86`

## Data-Driven Insights and Conclusion
* Interestingly, features such as  `count.`, `count_dir`, `hostname_length`, `uses-http` and `uses-https` might be used to identify phishing URLs
* Surprisingly, `url_entropy`, `short_url` were not useful
    * Both phishing and benign URLs can be just as complicated/random-looking
    * Both phishing and benign URLs are just as likely to use shorterning services

* Out of all the models, our parameter-tuned Random Forest performed the best. However as addressed in the Jupyter notebook, and reiterated here again, in the context of cybersecurity, our accuracy is too low for real-world applications, as 15% of links are misidentified. From even our best model, the false negative rate and false positive rate means that with a large volume, not only will phishing URLs be mis-identified as benign, but benign URLs might be errorneously flagged as phishing, disrupting the user from work unnecessarily.

* To further improve our models we could use a combination of different features, not just the top 5 identified during our EDA process, to possibly get a better results from our models. Another way we could have done better is to use Grid Search Cross-Validation instead of Random Search. Additionally, we could explore even more parameters, not just the one we tested through. Due to the very large dataset, this would have needed to use a lot of computing power, and might not have been viable for this project.

* Despite this, we can still suggest that a user might use the presence of `https` in addition to counting the number of directories and periods to raise their own suspiscion levels to mitigate phishing URLs

# 10. References
1. https://www.phishtank.com/developer_info.php  
2. https://www.kaggle.com/datasets/shashwatwork/web-page-phishing-detection-dataset/code  
3. https://majestic.com/reports/majestic-million  
4. https://www.projectpro.io/recipes/use-xgboost-classifier-and-regressor-in-python  
5. https://towardsdatascience.com/tuning-with-hdbscan-149865ac2970
