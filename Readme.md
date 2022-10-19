# Predicting Coronavirus Vaccine Hesitancy and Uptake  

### Background & Objectives  

This project aims to use two waves of online survey data collected from UK adults during the pandemic, to understand and predict UK individuals’ willingness to take, and actual uptake of the COVID vaccine.  
  
The study aims to answer the following questions:  
* Can we predict willingness to take the vaccine based on a set of demographic and attitudinal information?
* To what extent can these predictions be generalized to future data?
* Can further information be added to the model to improve its predictions?
* To what extent can these willingness predictions be used to predict actual uptake:
    - I.e. Do responses to the willingness questions appear to materially impact uptake predictions?
    
### Production Process  
An outline of the production process can be found below. Detailed information can be found within each section.
1. Initial data cleaning of wave 1 & wave 2 datasets
2. Exploratory Data Analysis
3. Modelling:
    - Modelling self-reported willingness to take a vaccine using Wave 1 data.
    - Applying the wave 1 willingness model to wave 2 data to understand the model's generalizability
    - Retraining the wave 1 willingness model on wave 2, with extra features
    - Using the wave 2 willingness model to further model actual uptake
4. Powerpoint Summary presentation of results
5. Further analysis and verification:
    - Neural network modelling & SMOTE under/oversampling
All code is stored in Jupyter notebooks. Packages used are:
    - Python
    - Pandas, Numpy, Sklearn, imblearn
    - Scikitplot, matplotlib, seaborn,
    - Joblib
A full outline of the survey questions, and data dictionary can be found in the initial data cleaning section (include link). Raw CSV data is available upon request.

### Summary of Findings  
**Can we predict willingness to take the vaccine based on a set of demographic and attitudinal information?**
Despite a significant imbalance in target classes, the initial wave 1 'willingness to take the COVID vaccine' model (fit on an unbalanced target sample) had some success in predicting the two 'extreme' classes - those who definitely will take the vaccine, or who definitely won't.  
**To what extent can these predictions be generalized to future data?**
Initial model generalises relatively poorly on wave 2 data, and even retraining the model on a wave 2 training data set using the same parameters and features fails to significantly improve results  
**Can further information be added to the model to improve its predictions?**
Retraining the model using extra feature information only present in the wave 2 data set does improve the model's performance in maximising the recall of classes 1, 3 and 4. However, class 2 precision and recall is low.  
**To what extent can these willingness predictions be used to predict actual uptake**
The generated 'willingness' score does emerge as an important predictor variable, with those reporting to be less willing to take the vaccine also less likely to have followed through with the behaviour.  
