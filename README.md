# Fetch Data Analyst Assessment
For this Assessment I have started by exploring the data for quality issues and any fields that might be challenging to understand. I have examined the structure of each dataset and check for missing values, duplicates, and inconsistencies.
### Contents
* **Cleaned Files:** Includes the datasets that have been processed and cleaned
* **Unstructured Data Files:** These files contain raw, unprocessed data in CSV format.
* **Fetch Assessment.ipynb:** This Jupyter Notebook contains the entire data analysis process.
* **Stakeholder Email pdf:** This PDF file contains a communication or email sent to the stakeholders.
* **assessment.db:** This is an SQLite database file containing the raw transactional or user data used for analysis.
### Technologies
* **Python/Pandas:** Used for data manipulation and analysis, handling large datasets efficiently.
* **Python/NumPy:** Provides support for numerical operations and array handling.
* **Python/Matplotlib:** Used for creating static visualizations such as charts and graphs.
* **Python/Seaborn:** Enhances Matplotlib for advanced statistical visualizations.
* **SqLite3:** Lightweight database for querying and storing data in a relational format.
* **GIT:** Version Control System for managing the repository.

### Data Exploration
#### Review the unstructured csv files and answer the following questions with code that supports your conclusions:
1. Are there any data quality issues present?
2. Are there any fields that are challenging to understand?
### Step 1: Data Overview
* Products Dataset: Contains product-related information.
* Transactions Dataset: Contains details about the purchases made by the user.
* Users Dataset: Contains users demographics.
### Step 2: Loading and Reviewing the data
I have inspected the structure of each dataset. I have loaded the datasets into Pandas. I have established the SQLite connection for database operations.
### Step 3: Identify the Data Quality issues
I have checked for common data quality issues like
* **Missing Values:** Several fields contain missing values, indicating potential gaps in data collection. Addressing these gaps is necessary for reliable analysis.
* **Duplicate Records:** I have identified duplicate records across the datasets. Duplicate data can lead to inaccuracies and should be removed or handled appropriately.
* **Incorrect Data types:** Some fields may have incorrect data types (e.g., numerical values stored as objects) when the data is loaded into a Pandas DataFrame, typically from CSV files. The data types need to be checked and corrected, as they could vary depending on the source (CSV, database, etc.). It is essential to verify the data types when querying data from the database to ensure accurate analysis and calculations.
### Step 4: Data Cleaning
* **Duplicate Removal:** Eliminated duplicate records from the Products and Transactions datasets to prevent data inconsistencies.
* **Date Fixes:** Converted date fields to proper formats and removed timezone information for consistency. In this case, the timezone has been removed using Pandas for analysis to ensure consistency across the dataset. But when working with databases, it is important to check the timezone settings, as the data might have timezone information that needs to be handled appropriately. 
* **Logical Date Corrections:** Removed invalid user records where birth dates were after account creation and fixed transactions where scan dates were before purchase dates.
* **Data Type Standardization:** Converted barcodes to strings and sales/quantity fields to numeric types for accurate calculations.
* **Invalid Records Removal:** Entries where Final quantity > 0 but Final sale was missing were flagged for further review.
* **Quantity Adjustment:** Rounded Final quantity to the nearest integer to maintain data accuracy.
### Step 5: Visualizations
To better understand the data, we performed several visualizations:

### User Data Visualizations

**Age Distribution:**
* A histogram was used to show the distribution of users' ages.
* This helps identify the age groups most represented in the dataset.

**Top 10 States by User Count:**
* A bar chart displayed the states with the highest number of users.
* Missing state values were replaced with “Unknown” for clarity.

### Product Data Visualizations

**Top 10 Most Frequent Brands:**
* A bar chart highlighted the most common product brands.
* This helps in understanding which brands dominate the dataset.

**Top 5 Product Categories by Count:**
* A bar chart was created to display the most common product categories.
* This helps in understanding which types of products are most frequently available.

### Transaction Data Visualizations

**Sales Amount Distribution:**
* A histogram was used to show the distribution of sales amounts.
* A logarithmic scale was applied to handle skewed data, making it easier to interpret trends.

**Top 10 Stores by Transaction Volume:**
* A bar chart highlighted stores with the highest number of transactions.
* This helps in identifying key locations where purchases are most frequent.

### Step 6: Challenging FIelds
* Some product entries like CATEGORY_1, CATEGORY_2, CATEGORY_3, and CATEGORY_4 lacked clear descriptions, making it hard to analyze product performance without additional reference data. 
* These generic names can create confusion, as they do not clearly indicate what kind of categorical data they represent. 
* Without proper documentation or domain knowledge, it is unclear whether these fields refer to product classifications, industry sectors, material types, or some other form of hierarchical categorization. 
* By adopting more descriptive names, the dataset becomes more user-friendly and reduces ambiguity when performing analysis, reporting, and decision-making.
