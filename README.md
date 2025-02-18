# Fetch Data Analyst Assessment
For this Assessment I have started by exploring the data for quality issues and any fields that might be challenging to understand. I have examined the structure of each dataset and check for missing values, duplicates, and inconsistencies.
### Exercise 1 - Exploring the Data
#### Review the unstructured csv files and answer the following questions with code that supports your conclusions:
1. Are there any data quality issues present?
2. Are there any fields that are challenging to understand?
#### Step 1: Data Overview
* Products Dataset: Contains product-related information.
* Transactions Dataset: Contains details about the purchases made by the user.
* Users Dataset: Contains users demographics.
#### Step 2: Loading and Reviewing the data
I have inspected the structure of each dataset. I have loaded the datasets into Pandas.
#### Step 3: Identify the Data Quality issues
I have checked for common data quality issues like
* Missing Values
* Duplicate Records
* Incorrect Data types
* Outliers
#### Missing Values
* **Description:** BIRTH_DATE (Users), CATEGORY (Products), FINAL_SALE (Transactions) have missing values.
* **Impact:** Missing birth dates impact age-related insights; missing categories impact product segmentation.
* **Resolution:** Imputation or exclusion based on business rules.
  
