# Bayesian ML Project
Team: Hidden-Layer-Heroes 

## Overview/ problem statemnt (1min)
(explain why los   and infectionss, inocation(litureature review shows most people focusing on using diagonosis data)
This project focuses on predicting Length of Stay (LOS) in the ICU using MIMIC-III and MIMIC-IV datasets, with a focus on infections and demographics. Infections, identified through microbiology cultures, are potentially important factors influencing ICU stay duration, although their exact impact on LOS is still being explored.

In addition to microbiology data, demographic factors such as age, gender, marital status, and insurance type are considered, as they may also play a role in predicting ICU outcomes.

By applying Bayesian modeling, we aim to integrate both microbiology culture and demographic data, accounting for uncertainty in the results. This approach will help refine predictions of ICU LOS, supporting healthcare professionals in making more informed decisions about resource allocation and patient care.

## Dataset 
In this project, we gather information from the MIMIC-III and MIMIC-IV demo datasets. MIMIC is a database comprising deidentified health-related data with patients who stayed in critical care units of the Beth Israel Deaconess Medical Center. MIMIC III contains data between 2001 and 2012, while MIMIC IV contains data for anchor age group 2011-2013 or 2014-2016. Both datasets consist of over 26 tables. The demo datasets used for this project contain records for 100 patients from each MIMIC-III and MIMIC-IV, that are selected randomly. 

MIMIC-III: https://physionet.org/content/mimic-iii-clinical-database/1.4/

MIMIC-IV: https://physionet.org/content/mimic-iv/1.0/




## EDA(2.5mins)

### Merging Tables:

To build a comprehensive dataset for predicting Length of Stay (LOS) in the ICU, we merged the following tables: 
- admissions: gives information regarding a patient’s admission to the hospital, includes demographic information. The unique identifier is hadm_id
  - Selected columns: 
- patients: information about gender and age identified by subject_id
  - Selected columns
- icustay: defines each ICU stay in the database using STAY_ID, including admission and discharge info
  - Columns used: 
- microbiologyevents: contains infectious growth from blood sample
  - Columns used: 

- , patients and icustay.
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
 
 









