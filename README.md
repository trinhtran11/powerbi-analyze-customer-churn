# powerbi-analyze-customer-churn
## Overview about the project
### Objective
The case study focuses on analyzing the churn rates of a telecom company called Databel, figuring out the reason(s) why customers are churning at the rate they are, and proposing recommendation(s).
### Data
The dataset is provided in the Power BI interactive course offered by DataCamp using a real-world problem. The dataset includes information about customers, churn status, demographics, and detailed subscription information (products and services used, contract type, and payment).
Refer to link https://app.datacamp.com/learn/courses/case-study-analyzing-customer-churn-in-power-bi
#### Meta data information
<img width="732" alt="Screenshot 2024-05-14 at 15 46 23" src="https://github.com/trinhtran11/powerbi-analyze-customer-churn/assets/167527643/9c16e8e3-8854-44a3-a1d6-7743e5551809">

### Definition
"Customer churn, also known as customer attrition, is when someone chooses to stop using your products or services. In effect, it’s when a customer ceases to be a customer.
Customer churn is measured using customer churn rate. That’s the number of people who stopped being customers during a set period of time, such as a year, a month, or a financial quarter." (https://www.qualtrics.com/uk/experience-management/customer/customer-churn/)

### Process for my work and the layout for this article
Perform data check to see if the data is clean.
Explore the data and create the necessary initial measures and columns for further calculation.
Analyse the data based on features.
Create dashboards to present the insight from the analysis to solve the defined problem.

## Data check
To check if there is any duplicate records of same customerID in the dataset, I create two measure count number of customerIDs and count distinct number of customerIDs.

    Number of customers = COUNT('Databel - Data'[Customer ID])
    Number of unique customers = DISTINCTCOUNT('Databel - Data'[Customer ID])

The value of two measures are the same.
Meanwhile, no action needed to clean the data at this stage.

## Exploratory Analysis
### Churn rate calculation
I can convert the value on the Churn Label column into numeric values so that the total number of churned customers can be calculated based on this column.

    Churned = IF('Data'[Churn Label] = "Yes", 1, 0)
    Number of churned customers = SUM('Data'[Churned])

Then, the churn rate is calculated by the following formula:<br>

    Churn Rate = Number of churned customers/ Number of customers
    
The result shows the churn rate is 26.86%.

### Churn reason
