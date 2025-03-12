# Bayesian ML Project
Team: Hidden-Layer-Heroes 

## Overview & Problem Statement

The aim of this project is to develop a model that utilizes Bayesian methods to predict a patient's length of stay (los) in the Intensive Care Unit (ICU) using de-identified public in-patient datasets, MIMIC-III and MIMIC-IV. Current literature has explored the application of Bayesian methods for predicting various outcomes related to disease severity and ICU stays. However, most studies have focused on specific diagnoses. Therefore, in this project, we aim to investigate the effect of infection-causing bacteria on a patient’s LOS in the ICU.

Bayesian modeling is particularly well-suited for investigating this problem as Bayesian methods are most effective when uncertainty is high and prior data can help refine future outcomes. By applying different Bayesian approaches that account for uncertainty, we aim to utilize and incorporate microbiological culture data and patient demographics to refine ICU LOS predictions. This, in turn, can aid clinicians develop more targeted and personalized treatment plans for patients with serious and/or multiple infections, given that the precise impact of specific bacteria on LOS is not yet well understood.


## Dataset 

Data for this project was obtained from the MIMIC-III and MIMIC-IV demo datasets. MIMIC is a database comprising de-identified patient data from critical care units at Beth Israel Deaconess Medical Center. MIMIC-III includes data from 2001 to 2012, while MIMIC-IV contains data for patients admitted between 2011 and 2016. Both datasets consist of over 26 tables. The demo datasets used in this project contain records for 100 patients from each of MIMIC-III and MIMIC-IV, randomly selected from the full dataset.

MIMIC-III: https://physionet.org/content/mimic-iii-clinical-database/1.4/

MIMIC-IV: https://physionet.org/content/mimic-iv/1.0/

This project aims to predict LOS in the ICU using the MIMIC-III and MIMIC-IV datasets, with a focus on infections and demographics. Therefore, both the ICU dataset and hospital dataset were obtained and utilized in this project. Microbiology data, which includes information on patient cultures, test results, and the names of infection-causing organisms was used. Since factors beyond bacterial infections can affect LOS, demographic variables such as age, gender, marital status, and insurance type were also considered.


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
| Microbio_group  | Category of microbio infections (microbio_group_gram_negative_rods, microbio_group_gram_positive_cocci, microbio_group_gram_positive_rods, microbio_group_mixed_flora, microbio_group_fungi_yeasts   |



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
We decided to use PC9 as the threshold to explain at least 95% variance from our data

![image](https://github.com/user-attachments/assets/44acc8a1-426d-49ca-98d9-609e0c4f6e9d)


## Models(5min)

### Model Selection

#### Bayesian Linear Regression  



specify independent/ dependent variables (ie PC1-9 as X and los as y)
intro of BLS
why we do linear regression and why bayesian is better( provide more information etc)
specify prior and posterior distribution -> the posterior prediction distribution
interpretation of result

### BNN (brief introduction 30 sec)

intro of BNN
1.Build BNN( MC drop ou)
2.l2 vs l1 regulation (MSE vs MAE)
3.BNN result and visualization
4.result interpretation

### Challenges and Model Comparison(1.5mins)

## Next Step(1min)
 Try different models(ie  non-bayesian ones)
 try different prior distribution
 try different prior distributions
 Get more data from the MIMIC III and IV

 Based on the uncertainty of the result, we can propose other suggestions
 
 









