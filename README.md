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
  - Columns used: subject_id, hadm_id, insurance, marital_status
    
    ![image](https://github.com/user-attachments/assets/3e0ee544-6e55-46ec-8377-015fbdc01283)

- patients: information about gender and age identified by subject_id
  - Columns used: subject_id, gender, age
    
    ![image](https://github.com/user-attachments/assets/f2865c69-d60f-4ae5-9109-3d2ffa0f5cde)

- icustay: defines each ICU stay in the database using STAY_ID, including admission, discharge, and length of stay
  - Columns used: subject_id, hadm_id, stay_id, los
    
    ![image](https://github.com/user-attachments/assets/f5be437b-8062-4f17-931b-9318ce798839)

- microbiologyevents: contains infectious growth from blood sample
  - Columns used: subject_id, hadm_id, org_name (list of infections)
    
    ![image](https://github.com/user-attachments/assets/b76ebc77-f3ae-4de6-bd35-cf3e293380fd)

- Merging process:
  1. Join patients and admissions table on subject_id
  2. Join the above table to icustays table on subject_id and hadm_id
  3. Join the above table to microbiology events table on subject_id and hadm_id

- Final Dataset:
  
  ![image](https://github.com/user-attachments/assets/2ad09f49-41a4-4679-a3ac-ac1f057ab19c)

Variables Lists

| Variables  | Description |
| ------------- | ------------- |
| Los  | Length of ICU stay (in days)  |
| Age  | Patient age on the admission  |
| Gender  | Patient gender (1: Male, 0: Female)  |
| Insurance  | Binary variable of insurance on admission (1: Medicacare, Medicaid; 0: Private  |
| Marital_status  | Patient age on the admission (in years) |
| Positive_culture  | Binary variable of microbio ifections (1: infected, 0: not infected)  |
| Marital_status  | Marital status of patient on admission (1: Married, 0: Single, Widowed, Divorced)  |




### EDA steps:(2.5mins)
Data Overview by Positive Culture

![image](https://github.com/user-attachments/assets/b7623b9d-935f-4039-8d6b-237b63f6d4b3)


Top 10 Microorganism by Number of Stays

![image](https://github.com/user-attachments/assets/788a99ff-98b9-485f-8f99-7ea00278968d)


Correlation Heatmap


![image](https://github.com/user-attachments/assets/da98a098-5d18-4201-aad9-f438d164764b)

LOS Distribution Comparison Between Positive and Non Positive Culture

![image](https://github.com/user-attachments/assets/06f4eb16-01ac-4711-bbf5-ebb223f44d38)


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
 
 









