# Predicting Coronavirus Vaccine Hesitancy and Uptake  

## Background & Objectives  

This project aims to use two waves of online survey data collected from UK adults during the pandemic, to understand and predict UK individuals’ willingness to take, and actual uptake of the COVID vaccine.  
  
The study aims to answer the following questions:  
* Can we predict willingness to take the vaccine based on a set of demographic and attitudinal information?
* To what extent can these predictions be generalized to future data?
* Can further information be added to the model to improve its predictions?
* To what extent can these willingness predictions be used to predict actual uptake:
    - I.e. Do responses to the willingness questions appear to materially impact uptake predictions?
    
## Production Process  
An outline of the production process can be found below. Detailed information can be found within each section.
1. Initial data cleaning of wave 1 & wave 2 datasets
2. Exploratory Data Analysis
3. Modelling
4. Powerpoint Summary presentation of results
5. Further analysis and verification:
    - Neural network modelling & SMOTE under/oversampling
All code is stored in Jupyter notebooks. Packages used are:
    - Python
    - Pandas, Numpy, Sklearn, imblearn
    - Scikitplot, matplotlib, seaborn,
    - Joblib  
    
A full outline of the survey questions, and data dictionary can be found in the initial data cleaning section. Raw CSV data is available upon request.

## Summary of Modelling Process & Findings  

### Summary of Modelling Process  

**Modelling stages**
The modelling process was divided into the following stages:
    - Modelling self-reported willingness to take a vaccine using wave 1 data.
    - Applying the wave 1 willingness model to wave 2 data to understand the model's generalizability.
    - Retraining the wave 1 willingness model to wave 2 data, with extra features.
    - Using the wave 2 willingness model to further model actual uptake.

**Preprocessing**
In order to address significant class imbalance in the target variable, SMOTE resampling was used to equalize classes. Meanwhile, Principal Component Analysis & Elasticnet regularization was used to simplify predictors and minimize the impact of any potential multicollinearity. All predictor data was standardized to ensure any differences in predictor scales would not impact feature coefficients. Data was split into train and test splits, with test data representing 20% of the total sample size.  

**Modelling**
Each modelling stage followed a series of iterative sub-processes, such that at each stage of the modelling, steps were taken to minimize the impact of potential issues (e.g. unbalanced classes, multicollinearity), and model performance could be directly compared at each stage of the process.  

At each modelling stage, the following process was followed:
* Running any necessary data preprocessing (Standardisation, Principal Components Analysis, SMOTE resampling).
* Running a variety of different classification methodologies to evaluate the best classification approach (including K Nearest Neighbours, Logistic regression, Decision Tree & Random Forest approach).
* Running an ADA booster on the preferred classifier to assess the extent to which running an ensemble model can minimize a base estimator’s misclassification.
* Running a grid search of parameters to optimize the preferred classifier’s parameters and assess any improvements in model performance.  

Models were evaluated primarily based on the recall scores of the priority classes of interest – those people ‘unsure, but leaning towards no’, and those ‘definitely unwilling’ to take the vaccine.  

Across almost all stages of modelling, logistic models performed better than the other methodologies tested. Non-parametric models showed clear signs of overfitting, as test data accuracy and ROCAUC scores fell far below the corresponding training scores. Ada boosted models meanwhile did not appear to cause any improvement in results.  

### Summary of Findings

**Can we predict willingness to take the vaccine based on a set of demographic and attitudinal information?**  
Despite a significant imbalance in target classes, the initial wave 1 'willingness to take the COVID vaccine' model (fit on an unbalanced target sample) had some success in predicting the two 'extreme' classes - those who definitely will take the vaccine, or who definitely won't.  

**To what extent can these predictions be generalized to future data?**  
The initial model generalises relatively poorly on wave 2 data, and even retraining the model on a wave 2 training data set using the same parameters and features fails to significantly improve results  

**Can further information be added to the model to improve its predictions?**  
Retraining the model using extra feature information only present in the wave 2 data set does improve the model's performance in maximising the recall of 3 classes (Those 'Definitely Willing to take the vaccine', 'Unsure but leaning towards no', 'Definitely Unwilling to take the vaccine'). However, the model's ability to predict those 'Unsure but leaning towards yes' is low.  

**To what extent can these willingness predictions be used to predict actual uptake**  
The generated 'willingness' score does emerge as an important predictor variable, with those reporting to be less willing to take the vaccine also less likely to have followed through with the behaviour.  
