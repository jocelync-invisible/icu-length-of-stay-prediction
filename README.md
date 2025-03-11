# Bayesian ML Project
Team: Hidden-Layer-Heroes 

## Overview/ problem statemnt (1min)
(explain why los   and infectionss, inocation(litureature review shows most people focusing on using diagonosis data)
This project focuses on predicting Length of Stay (LOS) in the ICU using MIMIC-III and MIMIC-IV datasets, with a focus on infections and demographics. Infections, identified through microbiology cultures, are potentially important factors influencing ICU stay duration, although their exact impact on LOS is still being explored.

In addition to microbiology data, demographic factors such as age, gender, marital status, and insurance type are considered, as they may also play a role in predicting ICU outcomes.

By applying Bayesian modeling, we aim to integrate both microbiology culture and demographic data, accounting for uncertainty in the results. This approach will help refine predictions of ICU LOS, supporting healthcare professionals in making more informed decisions about resource allocation and patient care.

## Dataset 
In this project, we gather information from the MIMIC-III and MIMIC-IV demo datasets. Both of these datasets contain clinical data from ICU patients. Both datasets contain clinical data from ICU patients, consisting of over 24 tables. The demo datasets used for this project contain records for 100 patients from each MIMIC-III and MIMIC-IV. 

MIMIC-III: https://physionet.org/content/mimic-iii-clinical-database/1.4/

MIMIC-IV: https://physionet.org/content/mimic-iv/1.0/




## EDA(2.5mins)

### Merging Tables:

To build a comprehensive dataset for predicting Length of Stay (LOS) in the ICU, we merged the following tables:

(add codes)

Patients: Demographic information, such as age, gender, marital status, and insurance. These variables play an important role in understanding patient outcomes.

Admissions: Information about the patient's hospital admission, such as admission time.

ICU Stays: Data on the patient's stay in the ICU, such as ICU start and end times, ICU type, and stay duration.

Microbiology Events: Data from microbiology culture results.

We merged the tables based on subject_id, stay_id and hadm_id.  ( note explain them)

### EDA steps:(2.5mins)

los distribution gragh 
infection vs non infection bar chart
PCA


## Models(5min)

### model selction (1min)
#### Baysian linear regression(2min) 

specify independent/ dependent variables (ie PC1-9 as X and los as y)
intro of BLS
why we do linear regression and why baysian is better( provide more information etc)
sepcify prior and postrior distribustion -> the posterior prediction distribution
interpretation of result

### BNN (brief introduction 30 sec)

intro of BNN
1.Build BNN( MC drop ou)
2.l2 vs l1 regulation (MSE vs MAE)
3.BNN result and visualization
4.result interpretation

### Challenges and Model Comparison(1.5mins)

## Next Step(1min)
 Try differnt models(ie  nonnbaysain ones)
 try differnt prior distriburion
 try different prior distributions
 Get more data from the MIMIC III and IV

 Based on the uncertainty of the result, we can proprose otehr suggestions
 
 









