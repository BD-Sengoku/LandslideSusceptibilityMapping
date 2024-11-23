### Project Overview

This project aims to predict geological hazard susceptibility using the LightGBM machine learning model with DEM-related data. The source code is organized into multiple modules and includes example data files.

The GIS data related to this project can be downloaded from [this link](https://drive.google.com/drive/folders/1-BO9I1mhs2RukBnQcUVywytDQx0DJkQv).

------

### Dataset Description

- **1844Points.csv**

  The initial dataset was generated using ArcGIS 10.8, including 922 geological hazard points (label: `target = 1`) and 922 randomly generated non-hazard points (label: `target = 0`). The table contains `FID`, latitude, longitude, 19 features, and a `target` column.

- **TheLocationOfTheStudyArea.csv**

  This dataset includes the latitude and longitude of the center points of 30m × 30m squares within the study area. These points were calculated using ArcGIS 10.8, and features were extracted using the "Extract Multi Values to Points" tool. (The corresponding tif images for features can be downloaded from [this link](https://drive.google.com/drive/folders/1-BO9I1mhs2RukBnQcUVywytDQx0DJkQv)).

------

### Code Module Description

#### 1. Model Training and Saving

This module:

- Loads and preprocesses data.
- Selects features based on the specified feature type and splits the data into training and validation sets.
- Performs classification using the LightGBM model with K-Fold validation.
- Optimizes hyperparameters using Hyperopt to find the best parameter combination.
- Trains the final model using the best parameters, computes evaluation metrics (AUC, accuracy, recall, etc.), and generates feature importance analysis results.
- Saves the model, prediction results, evaluation metrics, and feature importance data to specified files, completing the data analysis and model construction process.

#### 2. Use the Maintained Model to Predict the Entire Study Area

This module:

- Uses the pre-trained LightGBM model (saved in Module 1) for predictions.
- Performs probability predictions for specific study area data and combines the results with geographic location.
- Saves the outputs to a CSV file for further analysis.

#### 3. Perform SHAP Analysis Using the Maintained Model

This module:

- Loads and preprocesses data, splitting it into training and validation sets based on target values.
- Loads the pre-trained LightGBM model, calculates the AUC score, and uses SHAP (SHapley Additive exPlanations) to interpret model predictions.
- Generates feature importance plots and dependency plots to analyze the influence of features such as "Slope" on the model.
