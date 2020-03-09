# Mod-5-Project

The goal of this project is to use pipelines and GridSearchCV to optimize a number of supervised learning classification models to predict whether or not diabetic patients would be readmitted in the future following an hospital inpatient encounter.

## The Data
The dataset selected for this project come from the Center for Clinical and Translational Research at Virginia Commonwealth University. Data was sourced from the UC Irvine Machine Learning Repository and can be found here: https://archive.ics.uci.edu/ml/datasets/Diabetes+130-US+hospitals+for+years+1999-2008. The data represent 10 years (1999 - 2008) of clinical care at 130 US hospitals and integrated delivery networks. It includes over 50 features representing patient and hospital outcomes. The data exhibit encounters that satisfy the following criteria:

- It is an inpatient encounter (a hospital admission).
- It is a diabetic encounter, that is, one during which any kind of diabetes was entered to the system as a diagnosis.
- The length of stay was at least 1 day and at most 14 days.
- Laboratory tests were performed during the encounter.
- Medications were administered during the encounter.

A full list of feature descriptions can be found here: https://drive.google.com/file/d/1SSeT_sWLBoluq-24teF5BQ4lwMkWxWHU/view?usp=sharing

Value ID mapping for the variables admission_type_id, discharge_disposition_id, and admission_source_id can be found here: https://drive.google.com/file/d/19amgd_HmmsoUIr2TCmSpnkD9fWQqVOTE/view?usp=sharing

After cleaning the data, the following features were selected:
The final data set contains 59,408 instances and 13 variables/25 features that we are left with include the following:
- time_in_hospital (continuous): a range from 1 to 14 days, measuring the length of the inpatient stay
- num_lab_procedures (continuous): the number of lab tests performed for the patient during the encounter
- num_medications (continuous): the number of distinct generic name medicines administered during the encounter
- number_outpatient (continuous): the number of outpatient visits the patient had in the year preceding the encounter
- number_emergency (continuous): the number of emergency room visits the patient had in the year preceding the encounter
- number inpatient (continuous): the number of inpatient visits the patient had in the year preceding the encounter
- drugchange (continuous): a generated variable that counts the number of changes to any of 24 medications
- age1 (continuous): a generated random age for the patient - a random integer was selected from a 10-year range provided by the original categorical bin from the data set
- race (categorical): a dummy variable for one of Asian, Caucasian, Hispanic, Other; African American was the dropped dummy variable
- admission_type_id (categorical): a dummy variable where the option is either '3', representing 'Elective' admission, or not, which would identify the encounter as an 'Emergency' admission
- discharge_disposition_id (categorical): a dummy variable for either 3, 4, 5, 6; 2 was the dropped dummy variable. 2-6 represent 'Continued Care', 'Expired', 'No additional care', 'Short term care', and 'Hospice' respectively
- A1Cresults (categorical): a dummy variable for test results that show whether a patient's levels of blood glucose over the past 3 months has not changed, remained normal, increased >8%, or increased >7%
- Insulin (categorical): a dummy variable to indicate whether insulin was not prescribed, or whether it was held steady, increased, or decreased

The target variable will be 'readmitted', which classifies whether the patient was readmitted or there was no record of readmission.

## Modeling
Following a Logistic Regression model, following the application of Principal Component Analysis for feature reduction, the GridSearch Cross Validataion process was used to optimize parameters for a number of models including a singular Decision Tree, a Bagging Classifier (bagged decision tree), a Random Forest, an Adaptive Boosted forest, and an XG Boosted forest.

Because the cost of a false negative has a different cost than a false positive, I scored the models on their 'ROC_AUC' score and selected the final model on the highest class-weighted F1 score.

![alt text](https://github.com/zazuetaz/Mod-5-Project/blob/master/xgbroc.png)
