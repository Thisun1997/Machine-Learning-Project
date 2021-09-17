# Machine-Learning-Project
This repository contains the codes submitted to the <b>Pump it Up: Data Mining the Water Table</b> competition.
<br>The submissions that I was able to get a higher accuracy compared to previouse submissions are available in the repository. The approach followed in each of the submissions except for the best submission are given in the following table.

| Submission | Approch |
| --- | --- |
| [Submission 1](XGBoost_sub1.ipynb) | Remove duplicates. Impute missing values by modes. Cluster the longitude and latitudes. Drop some categorical columns based on theil's u correlation. Extract year and month data from date_recorded column. Target encode using leave-one-out encoder.Balance class distribution. Train XGBoostClassifier model. |
| [Submission 2](XGBoost_sub2.ipynb) | Same preprocessing and feature engineering steps in the final submission (explained below) were done to train and test set seperately (without joining them) and without gps_height imputation and log normalization steps. Drop some categorical columns based on theil's u correlation. Target encode using leave-one-out encoder.Balance class distribution.Train XGBoostClassifier model. |
| [Submission 4](OneVsRest_XGBoost_sub4.ipynb) | Same steps in submission 2 were followed before training an OneVsRestClassifier with XGBoostClassifier. |
| [Submission 7](XGBoost_sub7.ipynb) | Same steps in submission 2 were followed for preprocessing without dropping columns, target encoding and class balancing. A pipeline as explained below was used for final stage and training. |
| [Submission 8](CatBoost_sub8.ipynb) | Same preprocessing and feature engineering steps in the final submission (explained below) were done, but mean was used instead of median for imputing longitude and latitude values. Train a Catboost classifier. |

A brief discription of the approach followed in the best submission ([Submission 10](XGBoost_sub10.ipynb)) is explained below.

## Preprocessing
1. Removed the duplicates in training data.
2. Both train and test featuers were combined and following processings steps were done.
   * Missing value imputation.
     * ```funder```-replace by 'other'.
     * ```installer```-replace by 'other'.
     * ```subvillage``` - using mode of subvillages grouped by region_code wise.
     * ```public_meeting``` - using median.
     * ```scheme managment``` - using mode of scheme_managment grouped by region wise.
     * ```scheme name``` - using mode of scheme_name grouped by region wise.
     * ```permit``` - using median.
   * Rows with ```logitude```=0 and ```latitude```=0 values were replaced by the median logitude and latitude of the respective ```region_code```.
   * Rows with ```gps_height``` = 0 value were imputed with mean gps_height of the respective ```region_code```.
   * log normalize ```population``` column.

## Feature Engineering
1. A new feature ```Cluster``` was created by clustering longitudes and latitude into 8 clusters based on ```population``` using k-means clustering.
2. ```date_recorded``` column was seperated into 2 featuers, ```year``` and ```month``` by extracting year and month from the values in date_recorded column.

## Pipeline
Preprocessed and featuer engineered data was fed into a pipeline. The pieline performs following steps.
1. Convert all categorical columns to string.
2. OneHot encoded all the categorical columns.
3. All the numerical columns were scaled using standard scalar.
4. Trained the data using OneVsRest Classifier with XGBoostClassifier.

## Proof of submission
### Final rank
![rank_20211709_1506](https://user-images.githubusercontent.com/47599759/133763439-ccc43bb2-6438-4c40-9cb3-2b9081ca1ec2.PNG)
<br>(As of 17/09/2021 03:00 p.m.)

### submissions
![submissions](https://user-images.githubusercontent.com/47599759/133367787-da2d2fd1-fcb8-46f5-9678-d44d6cd4a42c.PNG)
