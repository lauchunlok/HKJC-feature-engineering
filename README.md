# HKJC-feature-engineering

### Tips for merge
#### Most of the feature engineering are performed in __form record__. Yet, there are 3 things needed to be merged from race_result and sectional time to form record
#### 1) Number of partcipating horses (for normalization)
#### 2) Prize money
#### 3) Section time

##### PS, Some races or even race day could be skipped when crawling. Not sure if because my computer do not have enough ram or whatever other reasons (e.g. the website is blocking).
##### Some steps I took might help ensure the completeness of the data.

### Analysis
#### The final goal is to make a database that contains all the apperance for houses that involved in races on 20150101 and onward
- As time-lag features is important for predicting horse performance in the future
- That means I will crawl all the historical record of houses that have appeared in the interested period (20150101 - Present)
- So form record will be larger and a race result complement will be crawled for form record normailzation

#### It is a project built for profit. Therefore, leakage and overfitting are the first thing to avoid which makes this project a good project for portfolio demonstration as well.
