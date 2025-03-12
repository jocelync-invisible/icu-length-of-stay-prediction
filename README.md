**ADSP 32014: Bayesian Machine Learning with Generative AI Applications: Final Project**

Team: Hidden-Layer-Heroes 

Alexa Kung, Feby Hadayani, Qing Chen, Sara Chaker

# Bayesian Modeling of ICU Length of Stay: Investigating the Impact of Infection-Causing Bacteria

## Overview & Problem Statement

The aim of this project is to develop a model that utilizes Bayesian methods to predict a patient's length of stay (los) in the Intensive Care Unit (ICU) using de-identified public in-patient datasets, MIMIC-III and MIMIC-IV. Current literature has explored the application of Bayesian methods for predicting various outcomes related to disease severity and ICU stays. However, most studies have focused on specific diagnoses. Therefore, in this project, we aim to investigate the effect of infection-causing bacteria on a patient’s LOS in the ICU.

Bayesian modeling is particularly well-suited for investigating this problem as Bayesian methods are most effective when uncertainty is high and prior data can help refine future outcomes. By applying different Bayesian approaches that account for uncertainty, we aim to utilize and incorporate microbiological culture data and patient demographics to refine ICU LOS predictions. This, in turn, can aid clinicians develop more targeted and personalized treatment plans for patients with serious and/or multiple infections, given that the precise impact of specific bacteria on LOS is not yet well understood.


## Dataset 

Data for this project was obtained from the MIMIC-III and MIMIC-IV demo datasets. MIMIC is a database comprising de-identified patient data from critical care units at Beth Israel Deaconess Medical Center. MIMIC-III includes data from 2001 to 2012, while MIMIC-IV contains data for patients admitted between 2011 and 2016. Both datasets consist of over 26 tables. The demo datasets used in this project contain records for 100 patients from each of MIMIC-III and MIMIC-IV, randomly selected from the full dataset.

MIMIC-III: https://physionet.org/content/mimic-iii-clinical-database/1.4/

MIMIC-IV: https://physionet.org/content/mimic-iv/1.0/

This project aims to predict LOS in the ICU using the MIMIC-III and MIMIC-IV datasets, with a focus on infections and demographics. Therefore, both the ICU dataset and hospital dataset were obtained and utilized in this project. Microbiology data, which includes information on patient cultures, test results, and the names of infection-causing organisms was used. Since factors beyond bacterial infections can affect LOS, demographic variables such as age, gender, marital status, and insurance type were also considered.


## Data Preprocessing 

### Merging Tables

To build a comprehensive dataset for predicting Length of Stay (LOS) in the ICU, we merged the following tables: 

- "admissions": gives information regarding a patient’s admission to the hospital, includes demographic information. The unique identifier is hadm_id
  - Columns used: subject_id, hadm_id, insurance, marital_status
        <p align="center">
      <img src="https://github.com/user-attachments/assets/3e0ee544-6e55-46ec-8377-015fbdc01283" width="370">
    </p>

- "patients": information about gender and age identified by subject_id
  - Columns used: subject_id, gender, age
    <p align="center">
      <img src="https://github.com/user-attachments/assets/f2865c69-d60f-4ae5-9109-3d2ffa0f5cde" width="250">
    </p>

- "icustay": defines each ICU stay in the database using STAY_ID, including admission, discharge, and length of stay
  - Columns used: subject_id, hadm_id, stay_id, los
    <p align="center">
      <img src="https://github.com/user-attachments/assets/f5be437b-8062-4f17-931b-9318ce798839" width="320">
    </p>

- "microbiologyevents": contains infectious growth from blood sample
  - Columns used: subject_id, hadm_id, org_name (list of infections)
    <p align="center">
      <img src="https://github.com/user-attachments/assets/b76ebc77-f3ae-4de6-bd35-cf3e293380fd" width="500">
    </p>

    There are 61 unique microorganism infections. We categorized them into 5 groups based on gram staining characteristics and morphological types: gram_negative_rods, gram_positive_cocci, gram_positive_rods, mixed_flora, and fungi_yeasts.


#### Merging process:
  1. Join patients and admissions table on subject_id
  2. Join the above table to icustays table on subject_id and hadm_id
  3. Join the above table to the microbiology events table on subject_id and hadm_id


#### Final Dataset:
  <p align="center">
      <img src="https://github.com/user-attachments/assets/2ad09f49-41a4-4679-a3ac-ac1f057ab19c" width="800">
    </p>


#### Variables Lists

| Variables  | Description |
| ------------- | ------------- |
| Los  | Length of ICU stay (in days)  |
| Age  | Patient age at admission  |
| Gender  | Patient gender (1: Male, 0: Female)  |
| Insurance  | Binary variable of insurance on admission (1: Medicare, Medicaid; 0: Private)  |
| Marital_status  | Patient age on the admission (in years) |
| Positive_culture  | Binary variable of bacterial infections (1: infected, 0: not infected)  |
| Marital_status  | Marital status of patient on admission (1: Married, 0: Single, Widowed, Divorced)  |
| Microbio_group  | Category of bacterial infections (microbio_group_gram_negative_rods, microbio_group_gram_positive_cocci, microbio_group_gram_positive_rods, microbio_group_mixed_flora, microbio_group_fungi_yeasts)   |



## Exploratory Data Analysis

**Descriptive Statistics**
<p align="center">
      <img src="https://github.com/user-attachments/assets/7ca129a7-ae2b-45e7-a845-847b6703f302" width="700">
    </p>
There are 2731 rows from our data. LOS ranges from 0-31 days.
</p>

**Data Overview by Positive Culture**
<p align="center">
      <img src="https://github.com/user-attachments/assets/e07108e1-32f2-4c97-877a-403ab527db1b" width="400">
    </p>
There is data imbalance between positive and non-positive culture. The average los for positive culture is lower from the non-positive culture.
</p>

**Top 10 Microorganisms by Number of Stays**
<p align="center">
      <img src="https://github.com/user-attachments/assets/18286dab-ccc0-48a1-9bca-9439d1d1c014" width="500">
    </p>
Yeast, Staph Aureus Coag, and Escherichia Coli are the top 3 microorganisms by highest number of stays.
</p>

**Correlation Heatmap**
<p align="center">
      <img src="https://github.com/user-attachments/assets/58b82849-f7b8-4408-82b7-5ebdfa6121d7" width="500">
    </p>
Generally, there are weak negative relationship among los and demographic and microbio group
</p>

**LOS Distribution Comparison Between Positive and Non-Positive Culture**
<p align="center">
      <img src="https://github.com/user-attachments/assets/765e9919-1b24-47be-9a8a-20b0fe25cdf9" width="700">
    </p>
Los distribution for both culture is positively skewed, there is higher observations with shorter los for positive culture, but it might be affected by data imbalance as well
</p>

**PCA**
<p align="center">
      <img src="https://github.com/user-attachments/assets/e91e9ac2-ec92-42ea-ab8b-efc43ab0d151" width="500">
    </p>
We decided to use PC7 as the threshold to explain at least 95% variance from our data
</p>

## Model Selection

### 1. Bayesian Linear Regression  

Bayesian linear regression extends traditional linear regression by incorporating prior beliefs regarding the parameters, allowing for more stable and interpretable results. The method is particularly useful in cases with limited data or high uncertainty as it combines prior distributions with observed data to update beliefs and obtain a posterior probability distribution. Compared to a traditional linear regression which assumes homoscedasticity, no multicollinearity, and normally distributed residuals—assumptions that may not hold in real-world clinical data. By incorporating prior information, providing a full posterior distribution, and capturing uncertainty more effectively, Bayesian regression is the most appropriate approach for this project’s objectives.

In this analysis, the independent variables (X) are the principal components (PC1–PC9), which were derived through Principal Component Analysis (PCA) to reduce dimensionality and mitigate collinearity among the original predictors. The dependent variable (Y) is LOS.


#### Model Architecture

The model follows a Bayesian framework with:

- Prior Distributions: Initial beliefs about model parameters

  a. Intercept (α) ~ Normal(0, 1)
  
  b. Coefficients (β) ~ Normal(0, 1)
  
  c. Error term (σ) ~ HalfNormal(1)
<p align="center">
      <img src="https://github.com/user-attachments/assets/39eb6005-2dbc-44b3-80d2-3775ead8a7da" width="600">
    </p>
    

- Likelihood: How the data is generated given the parameters

  Observations follow a normal distribution around the predicted values
  y ~ Normal(α + Xβ, σ)
<p align="center">
      <img src="https://github.com/user-attachments/assets/89702b4a-6b4f-4ea9-97ec-5a000879e6b3" width="600">
    </p>


- Posterior: Updated beliefs after observing data, obtained through MCMC sampling

<p align="center">
      <img src="https://github.com/user-attachments/assets/9504e7b2-2d67-4906-a51f-bb1df333772e" width="600">
    </p>


* Full probability distributions were obtained using PyMC

#### Model Performance

- RMSE Test: 0.9432375826569617

- R^2 Test: 0.12356540029771512

- RMSE Training: 0.9092801630996732

- R^2 Training: 0.17004178873982456

<p align="center">
      <img src="https://github.com/user-attachments/assets/00518d18-6ca4-4ff9-9f58-3cf9949a1bed" width="700">
    </p>
  



### 2. Bayesian Neural Network (BNN)

Bayesian Neural Networks (BNNs) are a type of neural network that applies Bayesian inference to learn a probability distribution over its weights. Unlike traditional neural networks, which rely on fixed point estimates, BNNs account for uncertainty in its parameters and produces probabilistic predictions. This allows for a more robust predictions, specifically in cases with small datasets or noisy data. 

For this analysis, we chose to implement a BNN in addition to a Bayesian linear regression to enhance the robustness of our ICU LOS predictions. Given the limited size of our dataset, a BNN offers a solution by mitigating overfitting, improving generalization, and providing meaningful uncertainty estimates, making it a suitable choice for this predictive modeling task.

#### Model Architecture

The Bayesian Neural Network consists of:

- Input layer matching the feature dimensions
- First hidden layer with 32 neurons and ReLU activation
- MC Dropout layer (p=0.2) for uncertainty estimation
- Second hidden layer with 16 neurons and ReLU activation
- Another MC Dropout layer (p=0.2)
- Output layer with a single neuron

The model uses L2 regularization (0.0001) to prevent overfitting and the Adam optimizer with a learning rate of 0.01. Mean Absolute Error (MAE) is used as the loss function.

#### Training Process 

The model was trained with the following callbacks:

- EarlyStopping: Monitoring validation loss with patience of 15 epochs
- ReduceLROnPlateau: Reducing learning rate by a factor of 0.3 with patience of 10 epochs

<p align="center">
      <img src="https://github.com/user-attachments/assets/df0d50eb-fdf4-43be-8d3d-329eedd84821" width="700">
    </p>


#### Uncertainty Estimation

Uncertainty is estimated using Monte Carlo Dropout with 100 forward passes during inference. This provides both the mean prediction and standard deviation for each sample.

<p align="center">
      <img src="https://github.com/user-attachments/assets/28513fe7-ab15-41a9-afb4-fd07041f9408" width="700">
    </p>


#### Model Performance

Performance metrics on the test set (original scale - days):

- MSE: 0.2780 days²
- RMSE: 0.5272 days
- MAE: 0.2950 days
- R-squared: 0.7060

<p align="center">
      <img src="https://github.com/user-attachments/assets/21efa533-9858-42a8-b731-b3410e89c596" width="700">
    </p>


Our Bayesian Neural Network shows that longer hospital stays are harder to predict accurately. The model's overall is moderately good performance (R-squared: 0.706). Despite this, the BNN's result still very useful for doctors because it shows not just how long a patient might stay, but also how confident we are in that prediction.




## Model Comparison and Reflections/Lessons Learned 


### Bayesian Neural Network Outperforms All Other Tested Models

Comparing the two models we ran, the Bayesian Neural Network (BNN) outperformed the Bayesian linear regression substantially. The R^2 for the BNN was nearly four times larger than the R^2 for the Bayesian linear regression, indicating that the BNN was able to explain a significantly larger proportion of the variance in our data.

This result aligns with our initial hypothesis when selecting models for this project, as we anticipated that the BNN’s capacity for capturing complex, non-linear relationships would lead to superior predictive performance compared to a Bayesian linear regression. 

However, while the performance difference is clear, it is important to note the trade-offs associated with each approach. With a Bayesian linear regression, despite its lower R^2, offers greater interpretability, lower computational cost, and robustness in scenarios with limited data. In contrast, the BNN, while more powerful, requires significantly more computational resources, hyperparameter tuning, and training time.


### Reflection on Modeling Approach & Lessons Learned

#### 1. Data-Related Challenges

  **Importance of Feature Selection**

  Deciding on the most relevant features took a substantial amount of time as we were unsure out of the many parameters available, which would be the most relevant to the prediction. Additionally, the use of Principal Component Analysis (PCA) was a crucial preprocessing step that we initially did not include. Applying a PCA to reduce the dimensionality of the features substantially helped our models as the predictive accuracy increased pre- and post-PCA.

  **Limited Dataset Size**

  One of the major challenges in our analysis was the relatively small sample size of the dataset. Given the complexity of ICU LOS prediction, having more data would have been beneficial for improving generalization and model stability. The small dataset increased the risk of overfitting, particularly for our Bayesian Neural Network (BNN), which typically requires more data to fully capture complex patterns. Notably, when we incorporated additional data from MIMIC-IV, we observed significant improvements in model performance compared to using only MIMIC-III. 


#### 2. Model-Related Challenges

  **Unknown Prior Distribution**
  A notable limitation in this project was the uncertainty surrounding the choice of prior distributions, specifically in the Bayesian linear regression model. Bayesian methods rely on prior beliefs regarding the parameters before observing the data. In this study, we chose to use a normal distribution as the prior for the coefficients in our regression model. While this is a standard choice, it is unclear whether this truly reflects the underlying distribution. If the real-world distribution of the parameters deviates from the assumed normal prior, then the model''s estimates and predications may be suboptimal or an inapplicable. 


#### 3. Lessons Learned

  **Modeling ICU LOS is Complex**

  Predicting ICU length of stay involves multiple factors beyond what our dataset captured. Patient outcomes are influenced by numerous variables, including treatment protocols, comorbidities, and hospital-specific factors that were not included in our dataset. This limitation highlighted the importance of integrating clinical expertise into our analysis.



## Next Steps and Future Directions

### Expanding the Dataset 

A key limitation of our study was the dataset size. Future research could involve collecting the complete MIMIC-III and IV dataset to improve model robustness. More data would allow for better generalization and enable more complex modeling techniques without the risk of overfitting. Additionally, the most recent data used in this project was from 2016, therefore incorporating more recent data could further improve the generalizability of the findings.

### Explore Other Bayesian Models

While we used Bayesian Linear Regression and Bayesian Neural Networks, other probabilistic models could also be explored. For example, hierarchical Bayesian models could capture patient-level variations, and Gaussian processes could provide a non-parametric Bayesian approach for modeling ICU LOS. 

Additionally, our current models assume a linear relationship between principal components and LOS, but real-world clinical data often exhibits non-linearity. Exploring Bayesian non-linear models, such as Bayesian splines or tree-based methods like Bayesian Additive Regression Trees (BART), could potentially yield better predictive performance.

### Bridging the Gap Between Predictions and Clinical Expertise for Greater Applicability

While some of us have prior experience in the healthcare field, our feature selection and modeling process would have benefitted from deeper collaboration with clinicians. Incorporating additional clinical variables—such as treatment interventions or lab results could provide a more comprehensive picture of factors influencing ICU LOS for infections. 

Clinical input is essential to ensure that the model’s predictions align with real-world decision-making. Without incorporating expert domain knowledge, even the most sophisticated model risks producing results that lack practical relevance. Future iterations of this project should prioritize collaborations with healthcare professionals to refine model inputs and ensure its applicability in a clinical setting.

 









