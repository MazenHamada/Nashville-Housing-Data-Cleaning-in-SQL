# 🏘️ Data Cleaning in SQL: Nashville Housing Market

## 📋 Project Overview
This project focuses on taking raw, messy real estate data and transforming it into a clean, usable format for further analysis or visualization. All data cleaning and transformation was performed using **Microsoft SQL Server (T-SQL)**. 

The dataset contains information about housing sales in Nashville, including property addresses, sale prices, sale dates, and owner details.

## 🛠️ Skills & Techniques Demonstrated
* **Data Type Conversion:** Standardizing date formats.
* **Handling NULL Values:** Using `ISNULL` and Self-Joins to populate missing reference data.
* **String Manipulation:** Utilizing `SUBSTRING`, `CHARINDEX`, `PARSENAME`, and `REPLACE` to split complex strings into distinct columns.
* **Data Standardization:** Using `CASE` statements to ensure uniform categorical data.
* **Advanced SQL:** Employing **Common Table Expressions (CTEs)** and **Window Functions** (`ROW_NUMBER()`, `PARTITION BY`) to identify and remove duplicate records.

## 🚀 Step-by-Step Data Cleaning Process

### 1. Standardizing Date Formats
The original `SaleDate` column contained unnecessary time data. I converted this into a standard `YYYY-MM-DD` Date format for cleaner time-series analysis.

### 2. Populating Missing Property Addresses
Some records were missing the `PropertyAddress` but shared a `ParcelID` with other records. I used a **Self-Join** to identify these instances and populated the `NULL` values using the address from the matching `ParcelID`.

### 3. Breaking Out Addresses into Individual Columns
The raw data combined the street address, city, and state into single strings. 
* **Property Address:** Split into `Address` and `City` using `SUBSTRING` and `CHARINDEX`.
* **Owner Address:** Split into `Address`, `City`, and `State` using a creative approach with `PARSENAME` and `REPLACE`.

### 4. Standardizing "Sold as Vacant" Field
The `SoldAsVacant` column contained inconsistent entries ('Y', 'N', 'Yes', 'No'). I used a `CASE` statement to standardize all entries to 'Yes' and 'No' for accurate aggregations.

### 5. Removing Duplicates
To ensure data integrity, I wrote a **CTE** alongside the `ROW_NUMBER()` window function. By partitioning the data by unique identifiers (ParcelID, PropertyAddress, SalePrice, SaleDate, LegalReference), I was able to isolate and remove duplicate rows.

### 6. Dropping Unused Columns
To optimize the database and remove redundancy, I dropped columns that were no longer needed after the splitting and standardizing process (e.g., the original un-split address columns).

## 🗂️ Files in this Repository
* `Data Cleaning Queries.sql` : The complete SQL script containing all the queries used for this project.
* `NashvilleHousing.xlsx` : The Dataset.
