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
* Potential Anomalies
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

### Inconsistent Datatypes
**Users**:

**CREATED_DATE(Object) & BIRTH_DATE(Object):**
* **Description**: This field stores the date and time the user was created, but it is stored as an object type.
* **Impact**: Without proper date formatting, it can cause issues when performing date-based operations, such as sorting, filtering, or calculating age or duration.
* **Resolution**: Convert CREATED_DATE and BIRTH_DATE to a datetime type using pandas' pd.to_datetime().

**Transactions**:

**RECEIPT_ID(Object):**
* **Description**: This field stores the unique identifier for each transaction.
* **Impact**: The object type is fine for alphanumeric receipt IDs. However, if they are strictly numeric, converting them to int64 or string could improve performance.
* **Resolution**: If alphanumeric, keep as object. If numeric, convert to string or int64 based on the ID format.

**PURCHASE_DATE(Object) & SCAN_DATE(Object):**
* **Description**: This field stores the date when a transaction occurred but is in object format.
* **Impact**: Date-related operations, such as sorting or calculating purchase frequency, will not be efficient.
* **Resolution**: Convert PURCHASE_DATE AND SCAN_DATE to a datetime type using pd.to_datetime().

**BARCODE (float64):**
* **Description**: This field represents the barcode of a product, but it is stored as a float64, which is typically not correct for barcode numbers.
* **Impact**: Storing as float64 may introduce rounding issues and lead to incorrect values, especially if barcodes have leading zeros or are alphanumeric.
* **Resolution**: Convert BARCODE to string (object) type to preserve the full barcode accurately without any rounding.

**FINAL_QUANTITY (object):**
* **Description**: This field stores the quantity of products purchased, but it’s stored as an object type.
* **Impact**: If the data is numeric, it will be difficult to perform arithmetic operations on the quantities stored as objects.
* **Resolution**: Convert FINAL_QUANTITY to an appropriate numeric type, like int64 or float64, depending on the data.

**FINAL_SALE (object):**
* **Description**: This field stores the final sale amount, but it is stored as an object type.
* **Impact**: Similar to FINAL_QUANTITY, performing calculations on FINAL_SALE will be difficult if it remains as an object type.

**Products:**

**BARCODE (float64):**
* **Description**: This field stores the product's barcode.
* **Impact**: Like in the Transactions Data, storing the barcode as float64 can result in rounding errors, particularly if barcodes have leading zeros or non-numeric characters.
* **Resolution**: Convert BARCODE to a string type to preserve the barcode accurately.
* **Resolution**: Convert FINAL_SALE to a numeric type (float64 or decimal) for accurate calculations.

### Outlier Detection in Final Sales
**Description**: The box plot visualization presented in this project aims to detect outliers in the Final Sale Amounts dataset. Outlier detection is crucial for identifying anomalies that may impact data analysis, or business decision-making.
**Interpretation of the Box Plot**: The box plot follows the Interquartile Range (IQR) method to identify potential outliers:

**1. Box (Interquartile Range - IQR)**
* The box represents the middle 50% of data (Q1 to Q3).
* The line inside the box denotes the median (Q2, 50th percentile).
* The whiskers extend up to 1.5 times the IQR from Q1 and Q3.

**2. Outliers Identification**
* Any data points beyond the whiskers are considered outliers.
* In this plot, several black circular points outside the whiskers indicate the presence of outliers.
* Most outliers are clustered around higher values of Final Sale Amounts.
* A few extreme outliers extend beyond 200, 300, and even 400.

**Conclusion**: The Final Sale Amounts dataset contains multiple outliers, as evident from the presence of several points beyond the upper whisker. These extreme values might require further investigation to determine if they are due to data entry errors, special cases, or genuine high-value transactions.

### Potential Anomalies
**Users:**

**GENDER (11 anomalies):**
* **Description**: The GENDER field likely contains unexpected values beyond the predefined categories (e.g., Male = 1, Female = 2, Other = 3).
* **Impact**: Skews demographic analysis and marketing segmentation.
* **Resolution**: Standardize values to predefined categories and flag inconsistencies for manual review.

**Transactions:**

**SCAN_DATE (24,440 anomalies):**
* **Description**: This could indicate duplicate, missing, or incorrect timestamps related to scanned receipts.
* **Impact**: Affects time-based sales analysis, fraud detection, and promotional campaign effectiveness.
* **Resolution**: Cross-verify SCAN_DATE with PURCHASE_DATE, ensuring logical consistency (e.g., SCAN_DATE should not be before PURCHASE_DATE).

**Products:**

**BARCODE (841,342 anomalies):**
* **Description**: This high count suggests missing, duplicated, or invalid barcodes.
* **Impact**: Affects inventory management, sales tracking, and recommendation systems.
* **Resolution**: Implement barcode validation rules and remove duplicates while ensuring missing values are handled appropriately.

#### Step 4: Data Cleaning
The process involves handling missing values, removing duplicates, managing inconsistent data types, detecting and removing outliers, addressing potential anomalies, and saving the cleaned data to CSV files. Below is an outline of the steps followed during the data cleaning process.

**Overview**
The data cleaning process is essential for ensuring that datasets are accurate, consistent, and ready for analysis. The following datasets are handled in this script:
* users_df – Contains user details, including demographic information.
* transaction_df – Contains transaction records, including dates, quantities, and sale amounts.
* products_df – Contains product details, including categories and barcodes.

**Steps**

**1. Handling Missing Values**
**Users**:
* Missing birth dates are filled with the median year as a placeholder, ensuring consistency in the dataset. The BIRTH_DATE column is populated with a date of format YYYY-01-01.

**Transactions**:
* Missing PURCHASE_DATE and SCAN_DATE are filled with the most frequent (mode) date in each column, ensuring that these essential dates are present for analysis.
* The FINAL_QUANTITY column, which contains numeric values, has any non-numeric entries converted to NaN. Missing numeric values in FINAL_QUANTITY and FINAL_SALE are filled with the respective column's median.
* Missing barcodes in the BARCODE column are replaced with the most frequent barcode value.

**Products**:
* Missing barcodes in the BARCODE column are replaced with the most frequent barcode value.

**2. Removing Duplicates**

* In the transaction_df, duplicate entries based on the BARCODE are removed, retaining the first occurrence.
* In the products_df, duplicates are removed based on a combination of columns: CATEGORY_1, CATEGORY_2, CATEGORY_3, CATEGORY_4, MANUFACTURER, BRAND, and BARCODE. The first occurrence is kept.

**3. Handling Inconsistent Data Types**
**Users**:
* The BIRTH_DATE and CREATED_DATE columns are converted to the appropriate datetime format.

**Transactions**:
* Columns such as RECEIPT_ID and BARCODE are converted to string format.
* Date columns PURCHASE_DATE and SCAN_DATE are converted to datetime format.
* Numeric columns FINAL_QUANTITY and FINAL_SALE are converted to appropriate numeric types.

**Products**:
* The BARCODE column is converted to string format to maintain consistency.

**4. Handling Outliers**

The FINAL_SALE column in the transaction_df is analyzed for outliers using the Interquartile Range (IQR) method. Values outside the range defined by 1.5 times the IQR above the third quartile or below the first quartile are considered outliers and removed from the dataset.

**5. Handling Potential Anomalies**

**Gender Data:**
* Gender anomalies are addressed by standardizing various non-binary and undefined gender categories (e.g., 'non-binary', 'prefer_not_to_say') into the value OTHER.
* All gender values are converted to lowercase to ensure case consistency.
* Missing gender values are filled with UNKNOWN.

**Date and Barcode Anomalies:**
* Both SCAN_DATE and PURCHASE_DATE are converted to timezone-naive datetime format to ensure consistency.
* Entries where the SCAN_DATE is earlier than the PURCHASE_DATE are removed.
* Transactions with missing or invalid barcodes are removed from the dataset.

**Product Barcode Anomalies:**
* Products with missing or invalid barcodes are removed from the dataset.

**6. Saving Cleaned Data**
The cleaned data is saved to the following CSV files:
* CLEANED_USER_TAKEHOME.csv: Contains the cleaned user data.
* CLEANED_TRANSACTION_TAKEHOME.csv: Contains the cleaned transaction data.
* CLEANED_PRODUCTS_TAKEHOME.csv: Contains the cleaned product data.

These files are saved to the specified path for further analysis or reporting.

#### Step 5: Challenging FIelds

In the Products dataset, there are certain fields named CATEGORY_1, CATEGORY_2, CATEGORY_3, and CATEGORY_4. These generic names can create confusion, as they do not clearly indicate what kind of categorical data they represent. Without proper documentation or domain knowledge, it is unclear whether these fields refer to product classifications, industry sectors, material types, or some other form of hierarchical categorization. 
By adopting more descriptive names, the dataset becomes more user-friendly and reduces ambiguity when performing analysis, reporting, and decision-making.
