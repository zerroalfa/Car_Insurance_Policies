# Car_Insurance_Policies
this is my 3rd project with Quantum Analytics

## Table of Contents

- [Project Overview](#project-overview)
- [Data Sources](#data-sources)
- [Recommendations](#recommendations)

### Project Overview
---

**Project Overview: Car Insurance Analysis**  

This project focuses on analyzing a **Car Insurance Dataset** that contains detailed information about customers and their car insurance details. The dataset includes columns such as customer demographics, car attributes, insurance claims, and financial information. With these data points, the project aims to uncover insights into customer behavior, claim trends, and potential risk factors that can inform decision-making for insurance providers.  

### Objectives:  
1. **Demographic Analysis of Car Usage**: Explore how car usage varies based on gender, the presence of kids driving, and marital status.  
2. **Claim Trends by Car Attributes**: Identify the most frequently claimed car makes and models and analyze the average claim amounts to uncover safety or reliability trends.  
3. **Educational and Financial Correlations**: Examine how education level and household income relate to claim frequency and claim amounts to identify demographic risk factors.  
4. **Impact of Car Color and Coverage Zones**: Assess whether car color or coverage zones correlate with claim frequency and severity, offering insights into risk evaluation.  

### Key Questions to Explore:  
1. **Car Usage Patterns**: What is the distribution of car usage based on gender and the presence of kids driving?  
2. **Claim Trends by Car Make and Model**: Which car makes and models are most frequently involved in insurance claims, and what is the average claim amount for each?  
3. **Demographics and Claims**: Is there a correlation between education level and claim frequency or claim amount? How does household income relate to these metrics?  
4. **Car Attributes and Risk**: How does car color correlate with claim frequency and claim amount?  
5. **Regional Claim Analysis**: What is the average claim amount across different coverage zones?  

### Value of the Analysis:  
This project provides valuable insights for:  
- **Insurance Providers**: To refine risk assessment models, adjust premiums, and design targeted marketing strategies.  
- **Automotive Industry**: To identify car makes and models with high claim frequencies, potentially influencing safety improvements or marketing strategies.  
- **Data Enthusiasts**: Offering an opportunity to perform exploratory data analysis, create visualizations, and apply machine learning techniques.  

### Potential Use Cases:  
1. **Risk Profiling**: Develop risk profiles for customer segments based on demographics, car attributes, and claim history.  
2. **Predictive Modeling**: Use historical data to predict claim frequency and amounts, enhancing underwriting processes.  
3. **Visualization Dashboards**: Create interactive dashboards to showcase insights such as regional claim trends and car usage patterns.  
4. **Insurance Policy Optimization**: Tailor insurance policies and pricing strategies based on identified trends and correlations.  

This project will deliver actionable insights into customer behavior, claim trends, and demographic risk factors, enabling insurance companies to optimize their operations and improve customer satisfaction.


![Dashboard]![3 Car Insurance Policies](https://github.com/user-attachments/assets/3e15ee82-7b20-4a4c-bb32-9cbb4044022b)



### Data Sources

Car Insurance Policies dataset: The primary dataset used for this analysis is the "Car Insurance Policies.xlsx" file, containing detailed information about Car Insurance Policies.

### Tools

- Excel - Data Cleaning
  - [Download here](https://microsoft.com)
- SQL Server - Data Analysis
- PowerBI - Creating reports


### Data Cleaning/Preparation

In the initial data preparation phase, we performed the following tasks:
1. Data loading and inspection.
2. Handling missing values.
3. Data cleaning and formatting.

### Exploratory Data Analysis

EDA involved exploring the sales data to answer key questions, such as:

- What is the overall sales trend?
- Which products are top sellers?
- What are the peak sales periods?

### Data Analysis

Include some interesting code/features worked with

**Total Number of Claims**
```sql
SELECT SUM(claim_freq) AS total_claims
FROM insurance_policies;
```
**Distribution of Claim Amount by Gender and Marital Status**
```sql
SELECT 
    gender,
    marital_status,
    SUM(claim_amt) AS total_claim_amount,
    COUNT(*) AS total_customers
FROM insurance_policies
GROUP BY gender, marital_status;
```
**Distribution of Car Usage by Gender and Kids Driving**
``sql
SELECT 
    gender,
    kids_driving,
    car_use,
    COUNT(*) AS count
FROM insurance_policies
GROUP BY gender, kids_driving, car_use;
```

**Most Frequently Claimed Car Model**
``sql
SELECT 
    car_model,
    COUNT(*) AS claim_count
FROM insurance_policies
WHERE claim_freq > 0
GROUP BY car_model
ORDER BY claim_count DESC
LIMIT 1;
```

**Claim Frequency & Amount by Car Color**
``sql
SELECT 
    car_color,
    SUM(claim_freq) AS total_claims,
    SUM(claim_amt) AS total_claim_amount
FROM insurance_policies
GROUP BY car_color
ORDER BY total_claims DESC;
```

**Correlation Between Education Level and Claim Frequency**
``sql
SELECT CORR(CASE 
                WHEN education = 'High School' THEN 1
                WHEN education = 'Bachelors' THEN 2
                WHEN education = 'Masters' THEN 3
                ELSE NULL
            END, claim_freq) AS correlation
FROM insurance_policies;
```

**Average Claim Amount by Car Make**
``sql
SELECT 
    carmaker,
    AVG(claim_amt) AS average_claim_amount
FROM insurance_policies
GROUP BY carmaker
ORDER BY average_claim_amount DESC;
```

**Total Claims, Average Claim Amount, Private Car Use %, Commercial Car Use %, Male Customer %, Female Customer %, and Total Claim Amount**
``sql
SELECT 
    SUM(claim_freq) AS total_claims,
    AVG(claim_amt) AS average_claim_amount,
    ROUND(SUM(CASE WHEN car_use = 'Private' THEN 1 ELSE 0 END) * 100.0 / COUNT(*), 2) AS private_car_use_percentage,
    ROUND(SUM(CASE WHEN car_use = 'Commercial' THEN 1 ELSE 0 END) * 100.0 / COUNT(*), 2) AS commercial_car_use_percentage,
    ROUND(SUM(CASE WHEN gender = 'Male' THEN 1 ELSE 0 END) * 100.0 / COUNT(*), 2) AS male_customer_percentage,
    ROUND(SUM(CASE WHEN gender = 'Female' THEN 1 ELSE 0 END) * 100.0 / COUNT(*), 2) AS female_customer_percentage,
    SUM(claim_amt) AS total_claim_amount
FROM insurance_policies;
```

### Results/Findings

The analysis results are summarized as follows:
**Total Number of Claims:**
The sum of the claim_freq column represents the total claims made.
Distribution of Claim Amount by Gender & Marital Status: The claims are distributed across different combinations of gender and marital status, with insights on which groups claim more frequently or with higher amounts.

**Car Usage Distribution:**
Private vs. commercial usage is categorized by gender and the number of kids driving.
Male drivers with more kids tend to use cars more commercially.
Most Frequently Claimed Car Model: The car model with the highest claim_freq indicates popular vehicles for claims.
Claim Frequency & Amount by Car Color: Certain car colors may show higher claims, hinting at preferences or risks associated with those vehicles.
Correlation Between Education Level & Claim Frequency: Education level likely influences claim behavior (e.g., higher education may correlate with fewer claims).
Average Claim Amount by Car Make: Some car brands show higher average claim amounts due to luxury, repair costs, or demographics.

**Key Percentages:**
Private vs. Commercial Use: Insight into how the fleet is utilized.
Male vs. Female Customers: Demographic split of the customer base.
Total Claims & Claim Amounts: Overall financial claims impact.
### Recommendations

Based on the analysis, we recommend the following actions:
**Target High-Risk Segments:**
Use insights from car colors, car makes, and demographics to identify high-risk groups for focused policies.
Premium Adjustments:
Adjust premiums based on education, car model, and usage type (e.g., commercial vehicles may need higher premiums).
Promote Safer Cars:
Highlight models and colors with fewer claims in advertising or customer communication.
Encourage Family-Oriented Policies:
Offer family-friendly discounts for private use cars to appeal to families with kids driving.
Education-Based Awareness:
Initiate awareness campaigns targeting education levels associated with higher claims.
### Limitations

**Dataset Completeness:**
While the dataset has no missing values, additional context like driving history, accident details, or geographic data could enhance the analysis.
Static Nature:
Data reflects a single snapshot or period without tracking trends over time.
Generalization Risks:
Correlation analysis may not imply causation (e.g., education level influencing claims directly).
Unmeasured Factors:
External factors (e.g., weather, road conditions) are unaccounted for, which could impact claim patterns.

### References

`column_1`

**bold**

*italic*
