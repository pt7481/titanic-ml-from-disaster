# 🚢 Titanic: Machine Learning from Disaster

## Project Summary

The sinking of the Titanic is one of the most infamous shipwrecks in history.  On April 15, 1912, during her maiden voyage, the widely considered “unsinkable” RMS Titanic sank after colliding with an iceberg. Unfortunately, there weren’t enough lifeboats for everyone onboard, resulting in the death of 1502 out of 2224 passengers and crew.  While there was some element of luck involved in surviving, it seems some groups of people were more likely to survive than others.  In this challenge, Kaggle asked us to build a predictive model that answers the question: **“What sorts of people were more likely to survive?”** using passenger data (e.g. name, age, gender, socio-economic class, etc).

---

### What I Did

* Designed a multi-stage strategy for optimizing model bias, variance, and generalizability to unseen data (see Figure 1).
* Split training data set into separate training and holdout sets to enable optimizing bias/variance and evaluate model generalizability prior to test prediction submission to Kaggle (see Figure 2).
* Defined model evaluation metric priority to evaluate the most meaningful metrics while accounting for imbalanced survival classes in the training data (see Figure 3).
* Selected Logistic Regression model type to maximize interpretability of model outputs and explainability to non-technical audiences.
* Performed data preparation tasks such as exploratory data analysis (EDA), missing value imputation, and feature engineering in order to support model development.
* Implemented reusable model evaluation framework consisting of metrics reporting, confusion matrices, precision-recall curve and SHAP visualizations.
* Integrated MLflow in order to track model optimization experiment results and log final model artifacts for future deployment.
* Integrated Optuna in order to identify optimal model hyperparameters during each cross-validation iteration.
* Summarized current model performance in terms of key evaluation metrics and demonstrated tactics for improving performance by engineering new features based on model mis-prediction EDA.

![Model Development Stages, Goals, and Techniques](https://thoughtswork-co.s3.us-east-2.amazonaws.com/TitanicModelDevelopmentStages_Thoughtswork.jpg)
**Figure 1:** Model Development Stages, Goals, and Techniques

![Data Set Strategy](https://thoughtswork-co.s3.us-east-2.amazonaws.com/TitanicDataSetStrategy_Thoughtswork.jpg)
**Figure 2:** Data Set Strategy

![Model Evaluation Metric Priority](https://thoughtswork-co.s3.us-east-2.amazonaws.com/TitanicEvaluationMetricPriority_Thoughtswork.jpg)
**Figure 3:** Model Evaluation Metric Priority

---

### What I Learned

* With regards to answering the question **"What sorts of people were more likely to survive?"**, the model currently identifies 2 subgroups as being more likely to survive and 20+ subgroups as being less likely to survive. 
    * The imbalance towards subgroups predicting non-survival is likely due to the training data set mostly consisting of non-survivors (38% survived, 62% perished).
    * Analysis of model mis-predictions identified 8+ subgroups that unpredicted survival, warranting further feature engineering (see Next Steps section).
* Summary of Subgroup Insights:
    * **Groups More Likely to Survive:**
        * 1st and 2nd Class Females
        * Passengers aged less than 10 years
        * Passengers traveling with 3-4 family members
    * **Examples of Groups Less Likely to Survive:**
        * All males across 1st, 2nd, and 3rd Class tickets 
        * Passengers aged 55 years and older
        * Passengers not assigned Cabin or Deck designations 
        * 3rd class passengers who embarked from Southampton, England
* The following **metrics** were observed when evaluating the model's predictions of an **unseen portion of Kaggle's _training_ data** (179 passengers):
    * **Accuracy:** **81%** of the passengers were predicted correctly.
    * **Precision:** Of the passengers the model predicted to survive, **80%** of the passengers actually survived.
    * **Recall:** Of the passengers that acutally survived, **79%** of the passengers were predicted to survive.
    * Additional metrics used to optimize model performance were **Log Loss, PR-AUC, and F1.**
* Each of the metrics above were **approximately 3-4% lower than baseline** suggesting unseen production data is more likely to perform worse if distribution shifts occur.  
    * This **performance degradation was observed** when evaluating the model's prediction of **Kaggle's _test_ data set**, where Kaggle reported the model predicting test passenger survival with **77% accuracy.**
---

### Next Steps

* **3-4% variance in model prediction performance of unseen training data indicate further model optimization is needed to improve model's performance with unseen test data.**
* Initial investigation into model's mis-predictions ("mistakes") identified features warranted to improve survival recognition (recall) of the following groups: 
    * 3rd class passengers from Southampton
    * 3rd and 2nd class males
    * Passengers without Cabin/Deck info
    * Passengers with 5 or more family members
* Once model performance variance between seen and unseen training data is reduced to 2 pp or less, **feature distribution shifts between training and test data should be investigated** if Kaggle submission accuracy does not increase to satisfactory levels.
    * Tactics to experiment with include:
        * Model prediction calibration to improve Logistic Regression model prediction probabilities
        * Group-based stratification to ensure training set feature distribution closely matches test set feature distribution
        * Sample reweighting to instruct model to emphasize input samples closely resembling test distribution
        * Experimenting with tree-based and other model types, balancing tradeoff between model complexity and interpretability
