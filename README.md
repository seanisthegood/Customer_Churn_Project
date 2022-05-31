# Customer Churn Project

This is a project to build a classifier for customer churn for SyriaTel - its an example of the process of building a binary classifier using multiple iteratoins of models with an eye on cross-validation, hyperparameter tuning, and selecting the relevent metris. 

## Customer Churn

Customer churn is a problem affecting any subsriber-based entity, identifying customers that will leave a service can mitigate the cost finding new users. A successful model can help predict who leave the service and potentially identify problem areas. 

## Project Data

For this data I used a dataset of 3300 entries that included relevent information for each customer including minutes usage, charges, and plan status including international plan status and voicemail plan status. The dataset also included location information which through modeling I deemed not as relevent or useful for modeling. The dataset was clean and did not require very much in the way of cleaning.

![Histograms of Features
](https://github.com/seanisthegood/Customer_Churn_Project/blob/main/Images/HISTOGRAMS.png)

## Customer Charges

The following charts give an idea of the average charge per customer for the dataset. The data is divided into day charges, night charges, evening charges, and international chargres. The feature total charges and these charts reflect that feature. 

![Customer Charges](https://github.com/seanisthegood/Customer_Churn_Project/blob/main/Images/Churned%20vs%20Retained%20Price.png)

## Model Pipeline

I used a model Pipeline with a package called Skippa that returns a dataframe from the pipeline. The pipeline helped to prevent data leakage when as the pipeline was using to scale data during cross-validation. 

## Model Selection

I used a variety of models in pursuit of the best model - Logisitic Regression, KNN, and Tree Based Models. Tree Based models scored best and the Boosted versions showed the best scores on the data. 


## Cross-Validation and Hyper-Parameter Tuning

I used crossCV and a Bayesian Search with CV and optimized the searches to find the best hyperparameters for the models using a beta-2 scorer than weighted towards recall score. I then used the best estimator from the searches and attempted another search. I repeated this process for the various models.

## Feature Importance
![Screen Shot 2022-05-19 at 3 23 02 PM](https://user-images.githubusercontent.com/80093912/169386296-714c209f-01e8-4584-b3f3-b4c840c9f72b.png)

With improved scores from the Decision Trees, Bagged Tree Models, and Random Forrest, I took a look into the feature importances and saw the location features were unimportant to the models. I then dropped those features from the training and test data. I trained the XGBOOST model on the data without those features.

## Final Model Selection

After taking a look at a dataframe with the all the models I opted to go with the XGBOOST model. Yes, the training scores were high, but I looked to the cross-val scores in making my decision, the average for the CV scores were the highest with the lowest standard deviation of the recall scores, my belief being it would perform best on the holdout test dated which I am treating as unseen data in the final metrics.
![Screen Shot 2022-05-19 at 3 20 26 PM](https://user-images.githubusercontent.com/80093912/169385957-b236b477-dfec-4d66-aa8c-254a12623756.png)

![crossval_df](https://user-images.githubusercontent.com/80093912/169385055-ed6c0243-0ad8-4220-8afc-57cc67d264f3.png)

## Final Test Score

I went with the XGBOOST model, but other models performed almost equally well on cross-validation. The XGBOOST model showed the highest recall score with the lowest standard deviation on the cross-validation on the Bayesian HyperParameter Search. The model performed better on the holdout test data than the cross-validation, but that could be the randomness of the test data.
![Confusino Matrix for README](https://user-images.githubusercontent.com/80093912/169385336-44bb2be8-413a-4e84-a7f1-449b0522e14f.png)

## Post Modeling Reccomendations

Looking at the Shapley Scores from the Model revealed a few insights -
* Internatinoal Plan greatly contributed to the prediction of a churn for the final model
* At higher dollar amounts churn rate increased
* Customer Service calls were a high indicator of potential Churn

![Shapley Feature Importance](https://github.com/seanisthegood/Customer_Churn_Project/blob/main/Images/Feature%20Importances%20-%20Shap.png)

The following chart shows the churn rate per a binned charge group with international customers compared to non-internatinoal customers-

![ChargeGroupsIntvsNonInt](https://github.com/seanisthegood/Customer_Churn_Project/blob/main/Images/Customer%20Charge%20Groups.png)

## Further Modeling

A further project would like to do see some better location information, and information on data useage. Location infomration had an inconsistency of area codes and states which was confusing. Phones have primarily become used for texting, internet, and app useage since this data set was recorded, so that would be more helpful to see. 
