# powerbi-analyze-customer-churn
## Overview about the project
### Objective
The case study focuses on analyzing the churn rates of a telecom company called Databel, figuring out the reason(s) why customers are churning at the rate they are, and proposing recommendation(s).
### Data
The dataset is provided in the Power BI interactive course offered by DataCamp using a real-world problem. The dataset includes information about customers, churn status, demographics, detailed subscription information (contract type, and payment) and products and services used.
[Link to course](https://app.datacamp.com/learn/courses/case-study-analyzing-customer-churn-in-power-bi)
#### Meta data information
<img width="732" alt="Screenshot 2024-05-14 at 15 46 23" src="https://github.com/trinhtran11/powerbi-analyze-customer-churn/assets/167527643/9c16e8e3-8854-44a3-a1d6-7743e5551809">

### Definition of customer churn
>"Customer churn, also known as customer attrition, is when someone chooses to stop using your products or services. In effect, it’s when a customer ceases to be a customer.
Customer churn is measured using customer churn rate. That’s the number of people who stopped being customers during a set period of time, such as a year, a month, or a financial quarter." [Reference source](https://www.qualtrics.com/uk/experience-management/customer/customer-churn/)

### Process for my work and the layout for this article
* Perform data check to see if the data is clean.<br>
* Explore the data and create the necessary initial measures and columns for further calculation.
* Analyse the data based on features.
* Create dashboards to present the insight from the analysis to solve the defined problem.

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

### Churn reasons
<img width="833" alt="Screenshot 2024-05-15 at 16 14 07" src="https://github.com/trinhtran11/powerbi-analyze-customer-churn/assets/167527643/2ef7615b-88fa-45ea-b1c1-db29ac4a28f0">
The tree map shows main categories of churn, competition stands out as the primary reason customers are leaving, dominant with 44.82%, followed by attitude, dissatisfaction and price. Each factors listed above occupies from 11% to 15% in total churned customers.<br>

Specificially,
* Regarding competition: More than 16% of churned customers leave because competitors provide either more attractive offers or better devices. Other competitive advantages of competitors are more data offering and higher download speed make up to more than 11% in total churned customers.
* Regarding attitude: About 11% customers leaving as they did not receive support from the support team and approximately 5% of customers churned because of attitude of the service provider.
* Regarding dissactifaction: Around 3% to 5% in total churned customers express their dissatisfaction on each factor including product, network reliability and service.
* Regarding price: More than 11% of churned customers feel like the price is too high, and unsatisfied with long distance and extra data charges.
<br>
Based on these findings, I decide to dive deeper into the demographics of churned customers to know who they are, product and services used, price they are charged and the support they need.

### Churn rate by demographics
To have an overview of churned customers and identify any useful pattern, I group the customers into age groups using the information in column "Under 30" and "Senior" and into gender groups.<br>

        Demographics = 
            IF(
                'Data'[Under 30] = "Yes",
                "Under 30",
                IF(
                    'Data'[Senior] = "Yes",
                    "Senior",
                    "Other"
                )
            )
<img width="1229" alt="Screenshot 2024-05-15 at 16 56 31" src="https://github.com/trinhtran11/powerbi-analyze-customer-churn/assets/167527643/245fd911-fce1-4388-ae62-53732ee39c05">
* Churn rates among all gender groups are quite similar.
* The majority of Databel's customers' are at 25 to 65 years old. Only a few customers are above 80 or less than 20.
* Meanwhile, the tree map clearly illustrates that the churn rate in senior age group higher by about 15% than figures in other groups. Also, the line and clustered column chart confirms the similar pattern: the average churn rate moves upwards from the age of 60, starts at about 26% and reaches at more than 50% at the age of 85.

### Churn rate by location
<img width="1211" alt="Screenshot 2024-05-15 at 19 48 59" src="https://github.com/trinhtran11/powerbi-analyze-customer-churn/assets/167527643/eef66ab2-39b2-42f9-a44d-76eded99dbd7">
I use the geographic information in the dataset to understand where customers live and where record abnormal figures. The table shows the number of customers, churned customers and churn rate by state. <br>
California stands out with a churn rate of 63.24%, much higher than the average at 26.86% of the whole company.

### Churn rate by subscription information



