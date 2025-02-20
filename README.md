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
I have inspected the structure of each dataset. I have loaded the datasets into Pandas. I have established the SQLite connection for database operations.
#### Step 3: Identify the Data Quality issues
I have checked for common data quality issues like
* **Missing Values:** Several fields contain missing values, indicating potential gaps in data collection. Addressing these gaps is necessary for reliable analysis.
* **Duplicate Records:** I have identified duplicate records across the datasets. Duplicate data can lead to inaccuracies and should be removed or handled appropriately.
* **Incorrect Data types:** Some fields have incorrect data types (e.g., numerical values stored as object or dates stored inconsistently). These need to be corrected for proper analysis and calculations.
#### Step 4: Data Cleaning
* **Duplicate Removal:** Eliminated duplicate records from the Products and Transactions datasets to prevent data inconsistencies.
* **Date Fixes:** Converted date fields to proper formats and removed timezone information for consistency.
* **Logical Date Corrections:** Removed invalid user records where birth dates were after account creation and fixed transactions where scan dates were before purchase dates.
* **Data Type Standardization:** Converted barcodes to strings and sales/quantity fields to numeric types for accurate calculations.
* **Invalid Records Removal:**
  * Transactions with Final quantity < 1 were dropped to ensure valid purchase data.
  * Entries where Final quantity > 0 but Final sale was missing were flagged for further review.
* **Quantity Adjustment:** Rounded Final quantity to the nearest integer to maintain data accuracy.
#### Step 5: Visualizations
To better understand the data, we performed several visualizations:

**User Data Visualizations**

**Age Distribution:**
* A histogram was used to show the distribution of users' ages.
* This helps identify the age groups most represented in the dataset.

**Top 10 States by User Count:**
* A bar chart displayed the states with the highest number of users.
* Missing state values were replaced with “Unknown” for clarity.

**Product Data Visualizations**

**Top 10 Most Frequent Brands:**
* A bar chart highlighted the most common product brands.
* This helps in understanding which brands dominate the dataset.

**Top 5 Product Categories by Count:**
* A bar chart was created to display the most common product categories.
* This helps in understanding which types of products are most frequently available.

**Transaction Data Visualizations**

**Sales Amount Distribution:**
* A histogram was used to show the distribution of sales amounts.
* A logarithmic scale was applied to handle skewed data, making it easier to interpret trends.

**Top 10 Stores by Transaction Volume:**
* A bar chart highlighted stores with the highest number of transactions.
* This helps in identifying key locations where purchases are most frequent.

#### Step 5: Challenging FIelds
* Some product entries like CATEGORY_1, CATEGORY_2, CATEGORY_3, and CATEGORY_4 lacked clear descriptions, making it hard to analyze product performance without additional reference data. 
* These generic names can create confusion, as they do not clearly indicate what kind of categorical data they represent. 
* Without proper documentation or domain knowledge, it is unclear whether these fields refer to product classifications, industry sectors, material types, or some other form of hierarchical categorization. 
* By adopting more descriptive names, the dataset becomes more user-friendly and reduces ambiguity when performing analysis, reporting, and decision-making.



