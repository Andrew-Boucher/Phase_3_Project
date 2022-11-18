[logo of a blue water droplet made of hands with Africa in the middle, next to the words "the water project"](./images/The_Water_Project.png)
\
\
## Overview

[The Water Project](https://thewaterproject.org/how-we-work) is a non-profit organization which helps to reduce water scarcity in sub-Saharan Africa by providing the necessary resources for water well construction. Our team is helping The Water Project by using machine learning models to predict the functionality of wells throughout Tanzania. More specifically, we aim to identify wells that are in working condition but are in need of repair to guide The Water Project's future work in this region. This allows them to maximize water access while allocating resources in the most efficient way.

## Data Understanding

The source of our data was [Taarifa](http://taarifa.org/) organization and the [Tanzanian Ministry of Water](http://maji.go.tz/). The dataset contained over 59000 rows of 40 feature columns describing waterpoints in the region installed between the years 1960 and 2013. It was hosted at [drivendata.org](https://www.drivendata.org/competitions/7/pump-it-up-data-mining-the-water-table/page/23/) as a data analysis competition. If you want descriptions of each feature, you can find them [here](https://www.drivendata.org/competitions/7/pump-it-up-data-mining-the-water-table/page/25/).
[A map of the administrative districts in Tanzania](./images/TanzaniaAdministrativeDivisions.png)

## Data Preparation

Once the data was imported, we analyzed it for nulls and missing values, as well as inspected each column for relevancy to our project.

## Model Selection

We split our data into training and test sets, then transformed and scaled numerical data and transformed and binary encoded our categorical data.
Since our target column, the functionality of the well, showed a significant class imbalance, we created synthetic data to oversample the "functional needs repair" class, in order to run unbiased predictive models on it.
We then created a baseline dummy model to compare our results to.

We used three different modeling algorithms, K-Nearest Neighbors, Random Forest Classifier, and Logistic Regression. These were all from the Scikit-Learn library.
To select the best model, we ran a series of grid searches for hyperparameter tuning. See [our final notebook](./Final%20Notebook.ipynb) for details and results of each step of the process.

## Results

We found the model that returned the highest recall score for the "functional needs repair" class of water pumps was the best model from our second logistic regression grid search.
The optimal hyperparameters for this model were shown to be.

Final model parameters:\
C: 10\
class_weight: balanced\
penalty: l1\
solver: saga

Below is a graph of the results of our model compared to the baseline, showing a recall score .7 for our model vs .07 of the baseline. Looking at the class of interest, "functional needs repair," our model showed a recall score of .79 vs the baseline of 0.07
[stacked bar graph with three bars, one for each graph, showing our model significantly outperforming the baseline by around 10x](Model_Prediction_Stack_Bar.png)

The most important features that affected the target prediction the most are shown in this graph.
[A bar graph of the feature importances for every column listed in the source dataframe](./images/pumpfeatsplot.png)\
This suggest that the critical features influencing the functionality of the waterpoint were 1) the type of the pump, 2) how much water is available, and 3) who is operating the waterpoint.


