
# ICU Length of Stay Prediction Model Comparison

## Performance Metrics

| Model                       | MSE    | RMSE   | MAE    | R²     | Data Source  | Type      |
|-----------------------------|--------|--------|--------|--------|--------------|-----------|
| Linear Regression           | 25.736 | 5.073  | 4.325  | 0.089  | MIMIC III & IV | Linear    |
| Bayesian Linear Regression  | 27.563 | 5.250  | 4.560  | 0.026  | MIMIC III & IV | Linear    |
| BNN                         | 30.498 | 5.523  | 4.482  | -0.080 | MIMIC III & IV | Linear    |
| BNN w/PCA                   | 23.335 | 4.831  | 3.313  | 0.049  | MIMIC III & IV | Linear    |
| Linear Regression w/PCA     | 28.373 | 5.327  | 3.750  | 0.118  | MIMIC III & IV | Linear    |
| Bayesian Linear w/PCA       | 28.390 | 5.328  | 3.749  | 0.170  | MIMIC III & IV | Linear    |
| DecisionTreeRegressor       | 0.501  | 0.708  | 0.397  | 0.471  | MIMIC III & IV | Non-Linear |
| SVR                         | 0.819  | 0.746  | 0.905  | 0.412  | MIMIC III & IV | Non-Linear |
| RandomForestRegressor       | 0.286  | 0.535  | 0.342  | 0.795  | MIMIC III & IV | Non-Linear |

## Updated Model Results

### BNN w/PCA
- MAE: 2.2285 days
- RMSE: 4.2889 days
- R-squared: 0.5848
- MSE: 18.3950 days²

### Linear Regression w/PCA
- MAE: 5.0161
- RMSE: 6.3485
- R²: 0.1245
- MSE: 40.3034

### Bayesian Linear w/PCA (Sara's)
- MAE: 5.0159
- RMSE: 6.3483
- R²: 0.1246
- MSE: 40.3008

