Electric Vehicle Dataset (USA) – Full Data Cleaning Documentation

This document reconstructs and documents all cleaning, validation, and modeling work performed on the raw dataset, based on a direct comparison between the raw dataset and the final cleaned dataset.

0️⃣ Raw Dataset Overview
Source: U.S. Electric Vehicle Population Data

Initial Shape: 269,673 rows × 17 columnn

Key Issues Observed in Raw Data

Large number of missing values in critical columns

Incorrect data types (identifiers stored as numbers)

Logically inconsistent values (e.g., BEVs with zero electric range)

Unvalidated model years

Redundant or low-value columns

No enforced geographic bounds

1️⃣ Column Standardization

Actions Taken

Renamed columns to snake_case

Ensured descriptive and readable column names

Why This Matters

Improves readability

Enables consistent programmatic access


2️⃣ Missing Value Handling

Raw State

Several columns contained missing or placeholder values

Missing values present in location, eligibility, and range-related fields

Actions Taken

Removed rows with missing critical information

Avoided arbitrary imputation to preserve real-world integrity

Result

Final dataset contains 0 missing values


3️⃣ Logical Consistency Enforcement

Major Issue Found

Battery Electric Vehicles (BEV) with electric_range = 0

Actions Taken

Identified BEVs where electric range was logically impossible

Removed invalid rows instead of imputing

Additional Rules

PHEVs allowed zero electric range

Electric range preserved only when logically valid

Impact

Prevents analytical and ML distortion


4️⃣ Data Type Corrections 

Raw Problems

postal_code stored as integer

census_tract_2020 stored as numeric

Actions Taken

Converted identifier columns to string

Why This Matters

Prevents leading-zero loss

Correct semantic meaning

5️⃣ Model Year Validation 

Raw Issue

Presence of future or unrealistic model years

Actions Taken

Restricted model years to 1999–2025

Result

Dataset reflects realistic vehicle population

6️⃣ Geographic Validation

Raw State

Coordinates not explicitly validated

Actions Taken

Enforced latitude and longitude bounds for Washington State

Removed rows with invalid or corrupted coordinates

Result

Clean, reliable geospatial data

7️⃣ Deduplication & Structural Cleanup

Actions Taken

Removed duplicate rows

Dropped redundant or low-value columns


Result:::

Final dataset: 259,237 rows × 16 columns

8️⃣ Final Validation & Quality Assurance

Final Checks

No missing values

No duplicates

Correct data types

Logical and geographic integrity

Final Dataset Status

Analysis-ready

Machine-learning-ready

Production-quality



NOTE !!! :::

Dataset Claim on Kaggle


The dataset was labeled as "cleaned" on Kaggle. However, a detailed inspection of the raw file reveals that the cleaning performed was structural rather than analytical.

This section documents:


Why the Kaggle version is partially cleaned

What issues remained unresolved

What additional work was performed to make the dataset truly analysis-ready


Evaluation of Kaggle-Provided Dataset:::::

1️⃣ Missing Values (Kaggle Limitation)


Several columns contained extremely high missing-value ratios (in some cases >99%)


No explanation or treatment of missingness was provided


Missing values were neither imputed nor filtered



🔴 Issue: Leaving missing values untreated is not considered proper cleaning for analytics or ML

2️⃣ Logical Inconsistencies

Critical Issue Identified:

Battery Electric Vehicles (BEVs) with electric_range = 0


🔴 This violates domain logic, as BEVs must have a non-zero electric range

Kaggle Status: Not addressed


3️⃣ Incorrect Semantic Data Types


Column	Kaggle Type	Correct Type	Reason

postal_code	Integer	String	Identifier, not numeric

census_tract_2020	Numeric	String	Geographic identifier

🔴 Kaggle treated identifiers as quantities, risking data corruption in broader use cases

4️⃣ Lack of Validation Rules

Kaggle dataset did not apply:

Model year range validation

Geographic coordinate bounds checking

VIN prefix length or format validation


5️⃣ Documentation Gaps

No definition of what "cleaned" means

No stated assumptions

No explanation of unresolved anomalies


🚀 My Additional Cleaning & Validation Work

✔ Logical Corrections

Removed BEVs with zero electric range

Preserved PHEVs where zero range is valid

✔ Missing Value Strategy

Removed rows with missing critical information

Avoided arbitrary imputation to maintain data integrity

✔ Semantic Data Modeling

Converted identifier columns to string

Ensured numeric columns represent measurable quantities only


✔ Model Year Validation

Restricted values to realistic range (1999–2025)

✔ Geographic Validation

Enforced Washington State latitude and longitude bounds

Removed invalid coordinate entries

✔ Structural Integrity

Removed duplicates

Standardized column naming


📈 Quality Improvement Summary



Aspect	                      Kaggle Dataset       Updated Dataset



Missing valueshandled	             ❌	                    ✅


Logical consistency	               ❌	                  ✅


Identifier semantics	             ❌	                    ✅


Geographic validation	             ❌	                    ✅


Documentation	                     ❌	                  ✅


Analysis-ready	                   ❌	                    ✅


