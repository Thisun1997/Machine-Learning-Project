# Machine-Learning-Project
This repository contains the codes submitted to the <b>Pump it Up: Data Mining the Water Table</b> competition.
<br>Top 6 submissions are available here. A brief discription of the approach followed in the best submission () is explained below.

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
### submissions
