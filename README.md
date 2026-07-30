# CUSTOMER CHURN ANALYSIS: IDENTIFYING HIGH-RISK SEGMENTS TO REDUCE REVENUE LOSS

**Table of Contents**

1. [Project Abstract](#1-project-abstract)
2. [Stages](#2-stages)
   - [I. Requirement gathering](#i-requirement-gathering)
     - [i. Objectives](#i-objectives)
     - [ii. Business Problem](#ii-business-problem)
     - [iii. Questions Asked](#iii-questions-asked)
     - [iv. Solution](#iv-solution)
     - [v. Users](#v-users)
     - [vi. Data Source](#vi-data-source)
     - [vii. Data Dictionary](#vii-data-dictionary)
     - [viii. Column Categorization](#viii-column-categorization)
     - [ix. Tools used](#ix-tools-used)
   - [II. Development (Cleaning and Visualisation)](#ii-development-cleaning-and-visualisation)
     - [a. Loading dataset into sql (MySQL)](#a-loading-dataset-into-sql-mysql)
     - [b. Checking for missing(null) values](#b-checking-for-missingnull-values)
     - [c. Checking for duplicates](#c-checking-for-duplicates)
     - [d. Outliers check](#d-outliers-check)
     - [e. Data type check](#e-data-type-check)
     - [f. Creating a view](#f-creating-a-view)
     - [g. Visualisation](#g-visualisation)
   - [III. Analysis](#iii-analysis)
     - [i. Findings documentation and Discovery](#i-findings-documentation-and-discovery)
3. [Recommendations](#3-recommendations)
4. [Conclusion](#4-conclusion)

---

**1. PROJECT ABSTRACT**

This project analyzes customer churn for a telecom company using the IBM Telco Customer Churn dataset. The goal is to identify key drivers of churn across four main segments: Contract type, Tenure, Monthly Charges, and Internet Service. The analysis involves data cleaning and transformation using MySQL, followed by visualization in Power BI. The final dashboard provides actionable insights to reduce churn and revenue loss by targeting high-risk customer segments.

---

**2. STAGES**

**I. Requirement Gathering**

**i. OBJECTIVES**

To analyze customer churn drivers by evaluating Contract, tenure, Monthly Charges, and Internet Service to identify high-risk segments. Provide actionable insights to reduce churn and revenue loss.

**ii. BUSINESS PROBLEM**

The telecom company does not know if Contract, tenure, Monthly Charges, or Internet Service are causing higher churn, leading to wasted retention spending and revenue loss.

**iii. QUESTIONS ASKED**

1. What is the overall churn rate ?
2. Does Contract type (Month-to-month, One year, Two year) affect churn rate?
3. Does Tenure (Trial, Regular, Committed) affect churn rate?
4. Do Monthly Charges (High vs Low) affect churn rate?
5. Does Internet Service type (DSL, Fiber optic, No internet) affect churn rate?
6. How much revenue is lost to churn?
7. Which segment (Contract, Tenure, Monthly Charges, Internet Service) has the highest churn rate?

**iv. SOLUTION**

1. Build a Power BI dashboard that visualizes churn rate across four key segments; Contract, Tenure, Monthly Charges, Internet Service with KPI cards showing total customers, overall churn rate, and revenue lost. The dashboard will enable the retention team to quickly identify high-risk segments and take targeted action.

2. Recommend possible course of action to be taken to solve the problem.

**v. USERS**

Retention Manager and Marketing Team will use the dashboard to identify high-risk customer segments and launch targeted retention campaigns to reduce churn and revenue loss.

**vi. DATA SOURCE**

The dataset was obtained from Kaggle. The dataset link is below;

DATASET LINK: https://www.kaggle.com/datasets/blastchar/telco-customer-churn

**vii. DATA DICTIONARY**

| Column Name | Data Type | Description |
|-------------|-----------|-------------|
| customerID | Categorical | Unique identifier for each customer |
| Contract | Categorical | Type of subscription contract |
| tenure | Numerical (Discrete) | Number of months customer has stayed with the company |
| Monthly Charges | Numerical (continuous) | Monthly amount charged to customer ($) |
| Internet Service | Categorical (Nominal) | Type of internet service customer subscribes to |
| Churn | Categorical (binary) | Whether customer canceled subscription |
| Total Charges | Numerical (continuous) | Total amount charged over entire tenure ($) |

**viii. VARIABLE CATEGORIZATION**

**Contract** represents the type of subscription agreement a customer has with the company. It consists of three distinct categories: Month-to-month (no long-term commitment, renews monthly), One year (12-month contract), and Two year (24-month contract).

**Tenure** represents the length of time a customer has been with the company and has been grouped into three distinct segments; Trial (0-12 months), Regular (13-24 months), and Committed (25+ months).

**Monthly Charges** represents the amount a customer pays per month. It has been grouped into two segments: High-Charges (≥70) and Low-Charges (<70).

**Internet Service** represents the type of internet connection a customer subscribes to. It consists of three categories: DSL (digital subscriber line), Fiber optic (high-speed fiber connection), and No (no internet service).

**ix. TOOLS USED**

MySQL - For cleaning and data manipulation

Power BI - For visualization

Excel - For documenting discovery analysis

---

**II. DEVELOPMENT (Cleaning and Visualisation)**

**a. Loading dataset into sql (MySQL)**

The dataset was imported into MySQL Workbench using the Table Data Import Wizard. The database schema was named churn, and the raw data was loaded into a table called customer_churn. A preliminary SELECT * FROM customer_churn LIMIT 5 query confirmed that all 7,043 rows and 21 columns were successfully loaded into the database with correct structure.

![Loading dataset into MySQL](image1.png)

**b. Checking for missing(null) values**

A NULL check was performed on the seven variables of interest (CustomerID, Contract, tenure, MonthlyCharges, InternetService, Churn, TotalCharges). The query returned no rows, confirming that no missing values exist in the core analytical variables. This ensures data completeness for analysis.

![Missing values check](image2.png)

**c. Checking for duplicates**

A duplicate check was performed by grouping all seven variables of interest and counting occurrences. The query returned no results, confirming that there are no duplicate records in the dataset. Each customer is unique.

![Duplicate check](image3.png)

**d. Outliers check**

Outlier detection was performed on the Monthly Charges variable using the Interquartile Range (IQR) method. The query calculated Q1 (25th percentile), Q3 (75th percentile), and IQR, then identified values outside the lower fence (Q1 - 1.5 × IQR) and upper fence (Q3 + 1.5 × IQR). The query returned no rows, confirming no outliers exist in Monthly Charges.

![Outliers check 1](image4.png)
![Outliers check 2](image5.png)
![Outliers check result](image6.png)

**e. Data type check**

The data type was checked to verify that all columns had appropriate data types. All variables of interest are in the correct data type, requiring no conversion.

![Data type check](image7.png)

**f. Creating a view**

A view named FINAL_CUSTOMER_CHURN was created to extract variables of interest for analysis and visualization.

![Creating view](image8.png)

**g. Visualisation**

The cleaned and transformed data was imported into Power BI for visualization. An interactive dashboard was designed with three KPI cards at the top displaying Total Customers (7,032), Overall Churn Rate (27%), and Revenue Lost (18%). Below the KPIs, four main visuals were built to answer the business questions: a stacked bar chart showing churn rate by Contract (Month-to-month at 43%, One year at 11%, Two year at 3%), a bar chart for Tenure (Trial at 48%, Regular at 29%, Committed at 14%), a column chart for Monthly Charges (High-Charges at 35%, Low-Charges at 17%), and a pie chart for Internet Service (Fiber optic at 61%, DSL at 28%, No at 11%).

The dashboard clearly identifies that Month-to-month contracts and Trial tenure customers are the highest risk segments, while Fiber optic users contribute the most to overall churn.

![Power BI Dashboard](image9.png)

---

**III. ANALYSIS**

**i. FINDINGS DOCUMENTATION AND DISCOVERY**

**CHURN RATE BY MONTHLY CHARGES ANALYSIS**

High-Charges customers (>$70) churn at 35%, while Low-Charges customers (≤$70) churn at 17%. This suggests that customers paying more are more likely to cancel, possibly due to higher expectations or price sensitivity.

![Monthly Charges Analysis](image10.png)

**CHURN RATE BY CONTRACT ANALYSIS**

Month-to-month customers have the highest churn rate at 43%, significantly higher than One year (11%) and Two year (3%). This indicates that customers without long-term commitments are far more likely to leave, suggesting that contract length is a strong retention driver.

![Contract Analysis](image11.png)

**CHURN RATE BY TENURE ANALYSIS**

Trial customers (0-12 months) show the highest churn at 48%, followed by Regular (13-24 months) at 29%, and Committed (25+ months) at 14%. This shows that newer customers are most at risk, and retention efforts should focus on the first year.

![Tenure Analysis](image12.png)

**CHURN RATE BY INTERNET SERVICE ANALYSIS**

Fiber optic customers have the highest churn rate at 61%, compared to DSL (28%) and No internet (11%). This is the highest churn rate across all segments, indicating a potential issue with fiber optic service quality, pricing, or competition.

![Internet Service Analysis](image13.png)

**OVERALL REVENUE LOST**

The Revenue Lost KPI shows **18%**, indicating that 18% of the company's total revenue (calculated from the variables of interest: Contract, tenure, MonthlyCharges, InternetService) is attributed to customers who have churned. This means that for every $100 in revenue captured from the selected variables, $18 is lost to customer cancellations.

![Revenue Lost KPI](image14.png)

**OVERALL CHURN**

The overall churn rate for the company is **27%**. This means that out of 7,032 total customers, approximately 1,899 customers have churned. This rate is significantly high for a telecom company, indicating a critical need for intervention to prevent further revenue loss.

![Overall Churn KPI](image14.png)

---

**3. RECOMMENDATIONS**

1. **Target Month-to-Month Customers** - With a churn rate of 43%, the company should offer incentives such as discounts or free upgrades to encourage these customers to switch to annual contracts.

2. **Prioritize Trial Tenure Customers** - Trial customers (0-12 months) show the highest churn at 48%. A dedicated onboarding program with proactive check-ins and personalized offers during the first 3-6 months can reduce early-stage churn.

3. **Review Fiber Optic Service** - Fiber optic customers have the highest churn rate at 61%. The company should investigate service quality, pricing, and competition to address underlying issues driving this segment to leave.

4. **Address High-Charges Customer Concerns** - Customers paying above $70 churn at 35%. The company should evaluate service value and customer satisfaction among this group to justify premium pricing.

5. **Focus Retention Efforts on Segments with Highest Churn Probability** - Prioritize Fiber optic (61%), Trial (48%), Month-to-month (43%), and High-Charges (35%) as the highest-risk segments.

---

**4. CONCLUSION**

The churn rate analysis identifies that Fiber optic customers have the highest probability of churning at 61%, followed by Trial tenure at 48%, Month-to-month contracts at 43%, and High-Charges customers at 35%. These four segments represent the greatest churn risk and should be the primary focus of retention strategies. By addressing the specific needs and pain points of these high-risk groups, the company can reduce overall churn from 27% and improve customer retention.
