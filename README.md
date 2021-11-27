# Udemy_Enron_Fraud_POI_Identification

1. The goal of the project was to identify Enron Employees responsible for the fraud based on the Enron financial and email dataset using a machine learning algorithm. Machine learning helps us learn from previously available data and to predict the outcome of the new data. It is useful to identify the features which are critical and need to be monitored.
The dataset available has in total 146 data points. The data is in the form of a dictionary with the keys corresponding to each person. Out of which the 18 people are identified POI ['HANNON KEVIN P', 'COLWELL WESLEY', 'RIEKER PAULA H', 'KOPPER MICHAEL J', 'SHELBY REX', 'DELAINEY DAVID W', 'LAY KENNETH L', 'BOWEN JR RAYMOND M', 'BELDEN TIMOTHY N', 'FASTOW ANDREW S', 'CALGER CHRISTOPHER F', 'RICE KENNETH D', 'SKILLING JEFFREY K', 'YEAGER F SCOTT', 'HIRKO JOSEPH', 'KOENIG MARK E', 'CAUSEY RICHARD A', 'GLISAN JR BEN F']
There were a few outliers in the data, one was the data set named 'TOTAL' which was the sum of all the data points and needed to be removed. A few outliers were identified on the basis of lack of information available about them.

2. The features which I ended up using are:
['poi', 'salary', 'to_messages', 'total_payments', 'exercised_stock_options', 'bonus', restricted_stock', 'shared_receipt_with_poi', 'expenses', 'from_messages', 'other', 'long_term_incentive']
The total number of available features were 21, out of which 14 were financial features, 6 were e-mail features and one was the 'poi' flag. A 'poi' or person of interest is a person highly likely to be guilty for the enron fraud case.two new features 'ratio_1' : the ratio of number of direct mails to poi from this person to the number of total outgoing mails, and 'ratio_2' : the ratio of direct mails from poi to this person to the number of total incoming mails.An automated feature selection function SelectKBest was used using GridSearchCV to find the optimum number of features required which came out to be 8 before introduction of new features and 10 after introduction of new features. The F1 score improved from .3625 to .5277 on introduction of new features.The features were selected on the basis of importance criterion using the .feature_importances_ command to list down the features.The features were arranged and then the k_best features were selected.I used the MinMaxScaler() using the Pipeline along with the classifier. Scaling is used to take care of the effect of ranges of different features and to bring them down to the same scale.

3. I ended up using the sklearn.ensemble.AdaBoostClassifier. I tried to work with the DecisionTreeClassifier along with GridSearchCV to tune the 'criterion', 'max_depth' and 'max_features', it gave good precision but the recall was not upto the mark. I also tried AdaBoostClassifier tuning 'algorithm' and 'n_estimators' but the results were not satisfactory. The RandomForest ensemble classifier took a lot of time to run and did not give me accurate results, I did not try to tune the parameters for it.

4. Tuning the parameters means to optimize the parameters that impact the model in order to enable the algorithm to perform the best. The tuning i performed is given in Ans3

5. In machine learning, model validation is referred to as the process where a trained model is evaluated with a testing data set. The testing data set is a separate portion of the same data set from which the training set is derived.
The mistake we can make is overfitting to the training data, which would give us very good accuracy for that set of data but if we test it on different data the accuracy may deteriorate. The validation was done by splitting our data into sets of training data and testing data using StratifiedShuffleSplit. StratifiedShuffleSplit is useful here because the number of values belonging to each class are unbalanced. With this we ensure that that training and test sets have the same class proportions as the whole dataset. It helps to predict the class with fewer number of points in our case the poi label with better performance.

6. Two of the evaluation metrics are:
Precision - It is the value for (Ture positive)/(True Positive + False Positive), Good precision would imply whenever any person is flagged poi, we have high confidence he is real poi but it may skip detecting some person who is actually a poi.
Recall - It is the value for (Ture positive)/(True Positive + False negative), Good recall would imply we will find most poi's but also there may be a lot of false positives.
