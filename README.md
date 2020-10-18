# Predicting Food Insecurity 

## Table of Contents
- [Objective](#Objective)
- [Data](#Data)
- [Executive Summary](#Executive-Summary)
- [Requirements](#Requirements)
- [Next Steps](#Next-Steps)


## Objective

[The Bok Choy Project](https://change-today.org/wp-content/uploads/2020/07/The-Bok-Choy-Project-Shauntrice-Martin-1.pdf) started by Shauntrice Rice, Root Cause Research Center, and Nichole Funk here in Louisville, KY highlights the impact that food insecurity has on the local community and who is affected by it most in Louisville. To example this, The Bok Choy Project went around town to various Kroger's and documented the amount of and quality of produce offered at the different Kroger's. In low-income communities and communities that are majority BIPOC, the Kroger had a ton of empty shelves, limited tropical produce, and no bok choy (hence, the name of the project). The Bok Choy project, the fact that [13.7 million households](https://www.ers.usda.gov/topics/food-nutrition-assistance/food-security-in-the-us/key-statistics-graphics.aspx) experienced food insecurity in 2019, and about [$161 billion worth of food](https://www.rts.com/resources/guides/food-waste-america/) is wasted each year inspired me to try and build a model that would predict food insecurity so that policy makers, federal and local government officials, etc, can all be proactive in the fight to end food insecurity. No one should go hungry no matter their income, job status, disability status, or what have you considering the amount of food thrown out each year.

## Data 

For this project I used the [Food Security Data for 2019](https://www.census.gov/data/datasets/time-series/demo/cps/cps-supp_cps-repwgt/cps-food-security.html) from the Census Current Population Survey Food Security file. A detailed data dictionary for the original data set can be found [here](https://www2.census.gov/programs-surveys/cps/techdocs/cpsdec19.pdf).

## Executive Summary

The data set I had chosen was from the Census so I knew there would be a lot of data cleaning involved. All of the columns were labeled with identifying codes for each question and all responses were labeled with inentifying codes. With extensive reading of the data dictionary, I was able to drop any columns that were different variations of the same question while keeping the main question, converted all values back to their original values, as well as renamed some columns for easier readability. The data frame started out with over 500 columns and over 138,000 rows. I made the decision for modeling to drop and person that was under the age of 16 as well as multiple people questioned from the same household. I felt this was a good decision for my specific model since I was looking out food insecurity and the factors that correlate with the issue at hand. By keeping in the family income, number of persons in household, and the main person questioned from each household I knew that dropping duplicated households would not affect my model too much.

Extensive exploratory data analysis was conducted on the data set to help me fully understand the data in hand. First, I did an analysis based on location categories which included regions, states, and if the person lived in a metropolitan area or not. There was a pretty even split across the board given the different population sizes of cities and states for folks who had experienced food insecurity at any point in the year of 2019. Next an aga analysis was performed to see if any age group fared worse than another and again, it was pretty even across the board given that most folks interviewed as main person in household were in the age range of 20-70 years old. Next, I explored the household make-up and found that a majority of the folks interviewed were from a 1 or 2 person households as well as family incomes of $100,000-$150,000 made up the majority of family income for folks interviewed. In addition, a majority of folks interviewed (82% to be exact) were white. These findings were interesting to me because it told me that this data set is not all that diverse or a good representation of the population.

The modeling process began with the question of can I predict whether or not someone will be food insecure based on the data. To answer this question, multiple classification models were ran which included Logistic Regression, Decision Trees, Bagged Decision trees, Random Forest, Support Vector Machines, a Histogram Gradient Boosting Classifier, as well as Principal Component Analysis (PCA). Before running the models I did the preprocessing steps on target encoding with a function based off of [this article](https://maxhalford.github.io/blog/target-encoding/) by Max Halford and then scaled the data for the models that would require the use of scaled data. All of the models performed relatively well by using a grid search with scores over 90% and minimal overfitting/underfitting occurring with the exception of a Logistic Regression that was run with PCA which scored around 80%. Though a lot of my models scored well, due to this being a classification problem, I wanted to look for the model that minimized the false negatives to the best of its ability and still have a decent score. The random forest model fit this criteria with a modeling score of 0.967 and 0.952 for training and testing data respectively, 610 misclassified as being food secure but were food insecure, 161 misclassified as being food insecure but were food secure, and an f-1 score of 0.97 for food security and 0.85 for food insecurity. 

## Requirements

- Python 3.8.3
- To do Target Encoding without a function:
```
pip install category_encoders
```
``` python
from category_encoders import TargetEncoder
```
- To do the histogram gradient boosting classifier:
``` python
from sklearn.experimental import enable_hist_gradient_boositng

from sklearn.ensemble import HistGradientBoostingClassifier
```

## Next Steps

The next steps I would take for this project would be to find more diverse data from 2019 to plug into the model, gather data from 2020 to see the difference between food security and food insecurity from the 2 years, and then deploy the model so that policy makers could get future predictions in order to proactively fight to end food insecurity and bridge the meal gap.