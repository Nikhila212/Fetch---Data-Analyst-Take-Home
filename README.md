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
### Missing Values
**Users**: 
* **Description**: The dataset contains missing values in several columns. Specifically, 3,675 records are missing birth dates, 4,812 records lack state information, and 5,892 records do not have gender specified. The most significant gap is in the language column, with 30,508 missing values, indicating a substantial portion of users did not provide their preferred language. However, the ID and CREATED_DATE fields are fully populated with no missing values.
* **Impact**: Missing BIRTH_DATE affects age-based segmentation and personalized marketing. Missing STATE may impact regional analysis and targeting. Missing LANGUAGE affects user experience customization, while missing GENDER limits demographic insights.
* **Resolution**: BIRTH_DATE can be estimated from other available data or imputed based on user behavior trends. STATE can be inferred from transaction history or IP-based location data. LANGUAGE defaulting to the most common language or using user activity to infer preference. GENDER can be predicted based on names (if available) or user preferences, or left as "Unknown" if not essential.

**Products:**
* **Description**: The Products dataset has significant missing values across multiple columns. The CATEGORY_1 column has 111 missing values, CATEGORY_2 has 1,424, CATEGORY_3 has 60,566, and CATEGORY_4 has 778,093 missing entries. Additionally, MANUFACTURER and BRAND both have 226,474 and 226,472 missing values, respectively. The BARCODE column also has 4,025 missing entries.
* **Impact**: Missing category data affects product grouping, recommendation systems, and marketing analysis. Missing manufacturer and brand details limit brand-specific insights and supplier evaluations. Missing barcodes disrupt the mapping of transactions to product details.
* **Resolution**: Fill missing CATEGORY values using related product attributes or clustering techniques. Retrieve missing MANUFACTURER and BRAND details from external sources or infer based on product descriptions. Drop rows with excessive missing values if they contribute minimally to overall insights.
  
**Transactions:**
* **Description**: The Transactions dataset has missing values only in the BARCODE column, with 5,762 missing entries. All other columns are complete with no missing values.
* **Impact**: Missing barcodes can lead to challenges in linking transactions with product details, affecting sales analysis and inventory tracking.
* **Resolution**: Cross-referencing with external product databases or previous transactions. Removing rows with missing barcodes if the percentage is negligible and does not impact analysis.
  
### Duplicate Records
**Users**:
* **Description**: No duplicate rows were found in the Users data. This means that each user is unique within the dataset, and there are no repeated entries for the same user.
* **Impact**: Since there are no duplicates, the integrity of the user data is intact, and it can be used for accurate analysis without the concern of redundant records skewing results.

**Products**:
* **Description**: There are 215 duplicate rows in the Products data, which indicates that some product entries have been repeated.
* **Impact**: Duplicate rows can cause overestimation in analyses such as sales forecasting, trend analysis, as each duplicate would be counted more than once. Repeated product entries may lead to inconsistencies in product-related reports and may complicate inventory management. The presence of duplicate rows can slow down data processing and analysis due to larger data sizes.
* **Resolution**: Identify the duplicate records based on a unique identifier and remove the repeated entries. Implement checks during data ingestion or integration processes to prevent duplicate entries in the future.

**Transactions**:
* **Description**: There are 171 duplicate rows in the Transaction data, meaning that some transactions have been recorded more than once.
* **Impact**: Duplicate transactions could result in inflated sales or transaction volume numbers, misleading reports about revenue, transaction counts, or performance metrics. Incorrect transaction data could lead to incorrect resource allocation, impacting operations like inventory restocking or customer support.
* **Resolution**: Remove duplicates by identifying them based on a unique transaction identifier. Apply data validation techniques during data entry or batch processing to detect and eliminate duplicate entries.

