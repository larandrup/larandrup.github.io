# Predicting Recidivism

### Background

Recent works in the Machine Learning community has raised concerns about the risk of unintentional bias in Algorithmic Decision-Making systems, affecting individuals unfairly. This project is inspired by COMPAS (Correctional Offender Management Profiling for Alternative Sanctions) which is a popular commercial algorithm used by judges and parole officers for scoring criminal defendant’s likelihood of reoffending (recidivism). It has been shown that the algorithm is biased in favor of white defendants, and against black inmates. In this project we intend to analyze the same data that ProPublica, a nonprofit organization, used for analysing COMPAS and investigate how bias occurs by creating machine learning models that predict recidivism and analyzing their disparity ratio.


### Problem Statement:

   In this project, we are conducting analysis on behalf of the Department of Justice to investigate the validity of recidivism prediction models. Specifically, we are interested in pinpointing where racial bias occurs. To this end, we will make recommendations to the Department on whether or not they should continue using recidivism models such as COMPAS.



   ### Description of data
Our data was sourced from Propublica who conducted their own analysis on the COMPAS model. This data is information collected from inmates in Broward County, Florida from 2013-2014. We kept columns containing demographic information such as age, sex, race, marital status, etc, columns containing information about prior offenses, including juvenile charges, and columns containing information about the offense(s) they are currently arrested for. We are interested in whether or not they reoffend after this arrest.

 [Source](https://github.com/propublica/compas-analysis/)




### Data Dictionary:

The final processed data ready for modeling that includes features only from unique inmates and aggregated charges for each inmate.


   * DataFrame

   | Feature      | Description | Data Type |
   | :---        |    :----:   |          ---: |
   | id      | Inmate identification number |  int |
   |sex | Inmate’s gender | Encoded: 0 for male; 1 for female | int |
   | race| Ethnic group or race of the inmate | str |
   | age | Inmate’s age|     int |
   |juv_fel_count | Inmate’s juvenile felony count  |  int |
   | juv_misd_count | Inmate’s juvenile misdemeanor count |     int |
   |  juv_other_count| Inmate’s other juvenile offense count |  int |
   | priors_count | Inmate’s previous offenses | int |
   |  hours_in_custody | Inmate’s total number of hours in custody |  float |
   |  charge_degree | Inmate’s charge/s. See encoding data dictionary below for more information | int  |
   |  is_recid | Yes or No answer if the inmate’s a re-offender or not |  int  |
   |  custody_status |  If prisoner is in custody, in probation, a pretrial inmate, a residential program, or on parole|  str |
   |  marital_status | Inmate’s marital status |  str |


   * Charge Degree Encoding

|encoding|charge degree|description|degree|
|--------|-------------|-----------|------|
|13|F10|(felony) 10th level|1st|
|12|F9|(felony) 9th level|1st|
|11|F8|(felony) 8th level|1st|
|10|F7|(felony) 7th level|1st|
|9|F6|(felony) 6th level|2nd|
|8|F5|(felony) 5th level|2nd|
|7|F4|(felony) 4th level|2nd|
|6|F3|(felony) 3rd level|3rd|
|5|F2|(felony) 2nd level|3rd|
|4|F1|(felony) 1st level|3rd|
|3|M1|(misdemeanor) 1st degree||
|2|M2|(misdemeanor) 2nd degree||
|1|O|other||

# Modelling
We tried the following 13 different models with their default hyperparameters to serve as baselines for future training. From there we chose to make further adjustments to 3 models to try and improve our accuracy score. These models were Decision Tree, Random Forest, and XGBoost. From there, based on testing scores, we picked a Random Forest Classifier as our final model to make predictions.

|model|train|test|
|--------|------|-----|
|Bernoulli NB| 0.7550 | 0.7564|
|Gaussian NB|0.6972|0.6955|
|Decision Tree|0.7733|0.7722|
|KNN|0.8445|0.7205|
|Logistic Regression|0.7313|0.7409|
|Random Forest | 0.6913|0.6985|
|AdaBoost |0.7689 |0.7691 |
|Gradient Boosting | 0.7747|0.7679 |
|Multilayer Perceptron |0.7702 |0.7718 |
|Quadradic Discrimination |0.6524 |0.6491 |
|XGBoost |0.8045 |0.7656 |




 ### Next steps / Conclusions

There are many more things that can be done in order to increase the validity of recidivism prediction models.  In our case, collecting better data, gathering more data from undersampled populations, and using over/undersampling techniques could be explored further.  One glaring issue is how to account for the many proxies of race (and thus systemic racism)?  Weighting or thresholding values based on race could possibly help.  Ultimately, the root problem lies within the bulk of data reflecting the fact that African-Americans and other minority groups are far more likely to be arrested and prosecuted than Caucasians.  Any model that uses this data to make predictions will be perpetuating this problem.

Due to all of these issues, we do not recommend the Department of Justice to heavily rely on an algorithm to aid decisions in sentencing based on predicted recidivism.
