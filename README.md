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

Bayesian linear regression extends traditional linear regression by treating model parameters as probability distributions rather than fixed values. 

We implements Bayesian linear regression using PyMC to provide full probability distributions rather than just point estimates.

**Model Architecture**

The model follows a Bayesian framework with:

- Prior Distributions: Initial beliefs about model parameters

a. Intercept (α) ~ Normal(0, 1)

b. Coefficients (β) ~ Normal(0, 1)

c. Error term (σ) ~ HalfNormal(1)
![image](https://github.com/user-attachments/assets/39eb6005-2dbc-44b3-80d2-3775ead8a7da)

- Likelihood: How the data is generated given the parameters

Observations follow a normal distribution around the predicted values
y ~ Normal(α + Xβ, σ)
![image](https://github.com/user-attachments/assets/89702b4a-6b4f-4ea9-97ec-5a000879e6b3)


- Posterior: Updated beliefs after observing data, obtained through MCMC sampling
![image](https://github.com/user-attachments/assets/9504e7b2-2d67-4906-a51f-bb1df333772e)

**Model Performance**

RMSE Test: 0.9432375826569617

R^2 Test: 0.12356540029771512

RMSE Training: 0.9092801630996732

R^2 Training: 0.17004178873982456

![image](https://github.com/user-attachments/assets/00518d18-6ca4-4ff9-9f58-3cf9949a1bed)




### BNN ()

**Model Architecture**
The Bayesian Neural Network consists of:

- Input layer matching the feature dimensions
- First hidden layer with 32 neurons and ReLU activation
- MC Dropout layer (p=0.2) for uncertainty estimation
- Second hidden layer with 16 neurons and ReLU activation
- Another MC Dropout layer (p=0.2)
- Output layer with a single neuron

The model uses L2 regularization (0.0001) to prevent overfitting and the Adam optimizer with a learning rate of 0.01. Mean Absolute Error (MAE) is used as the loss function.

**Training Process**
The model was trained with the following callbacks:

- EarlyStopping: Monitoring validation loss with patience of 15 epochs
- ReduceLROnPlateau: Reducing learning rate by a factor of 0.3 with patience of 10 epochs

![Image](https://github.com/user-attachments/assets/df0d50eb-fdf4-43be-8d3d-329eedd84821)

**Uncertainty Estimation**
Uncertainty is estimated using Monte Carlo Dropout with 100 forward passes during inference. This provides both the mean prediction and standard deviation for each sample.

![Image](https://github.com/user-attachments/assets/28513fe7-ab15-41a9-afb4-fd07041f9408)

**Model Performance**
Performance metrics on the test set (original scale - days):

- MSE: 0.2780 days²
- RMSE: 0.5272 days
- MAE: 0.2950 days
- R-squared: 0.7060

![Image](https://github.com/user-attachments/assets/21efa533-9858-42a8-b731-b3410e89c596)

Our Bayesian Neural Network shows that longer hospital stays are harder to predict accurately. The model's overall is moderately good performance (R-squared: 0.706). Despite this, the BNN's result still very useful for doctors because it shows not just how long a patient might stay, but also how confident we are in that prediction.

### Challenges and Model Comparison(1.5mins)

## Next Step(1min)
 Try different models(ie  non-bayesian ones)
 try different prior distribution
 try different prior distributions
 Get more data from the MIMIC III and IV

 Based on the uncertainty of the result, we can propose other suggestions
 
 









