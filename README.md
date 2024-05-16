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

    Churned = IF('Databel - Data'[Churn Label] = "Yes", 1, 0)
    Number of churned customers = SUM('Databel - Data'[Churned])

Then, the churn rate is calculated by the following formula:<br>

    Churn Rate = Number of churned customers/ Number of customers
    
The result shows the churn rate is 26.86%.

### Churn reasons
<img width="833" alt="Screenshot 2024-05-15 at 16 14 07" src="https://github.com/trinhtran11/powerbi-analyze-customer-churn/assets/167527643/2ef7615b-88fa-45ea-b1c1-db29ac4a28f0"><br>
The tree map shows main categories of churn, competition stands out as the primary reason customers are leaving, dominant with 45%, followed by attitude, dissatisfaction and price. Each factors listed above occupies from 11% to 15% in total churned customers.<br>

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
                'Databel - Data'[Under 30] = "Yes",
                "Under 30",
                IF(
                    'Databel - Data'[Senior] = "Yes",
                    "Senior",
                    "Other"
                )
            )
<img width="1229" alt="Screenshot 2024-05-15 at 16 56 31" src="https://github.com/trinhtran11/powerbi-analyze-customer-churn/assets/167527643/245fd911-fce1-4388-ae62-53732ee39c05"><br>
* Churn rates among all gender groups are quite similar.
* The majority of Databel's customers' are at 25 to 65 years old. Only a few customers are above 80 or less than 20.
* Meanwhile, the tree map clearly illustrates that the churn rate in senior age group higher by about 15% than figures in other groups. Also, the line and clustered column chart confirms the similar pattern: the average churn rate moves upwards from the age of 60, starts at about 26% and reaches at more than 50% at the age of 85.

### Churn rate by location
<img width="1211" alt="Screenshot 2024-05-15 at 19 48 59" src="https://github.com/trinhtran11/powerbi-analyze-customer-churn/assets/167527643/eef66ab2-39b2-42f9-a44d-76eded99dbd7">
I use the geographic information in the dataset to understand where customers live and where record abnormal figures. The table shows the number of customers, churned customers and churn rate by state. <br>
California stands out with a churn rate of 63%, much higher than the average at 27% of the whole company.

### Churn rate by subscription information
<img width="1223" alt="Screenshot 2024-05-16 at 12 01 01" src="https://github.com/trinhtran11/powerbi-analyze-customer-churn/assets/167527643/e3567772-8903-443c-ac5b-accd0bf55e93"><br>
 I investigate the churn rates' variation depending on customers' account length, their payment method and contract type.<br>
 * It is noticeable that churn rates decrease over time of the period. It means that the longer customers having been with Databel, the less likely they will churn comparing to new customers.
 * Among three types of payment method used in Databel, Direct debit is dominant and used by more than half of total customers. This type of payment method also records the high churn rate at about 35%. Paper check records the highest churn rate at 39%; however, the number of customers using this payment method is insignificant.
 * Among two types of contract offered by Databel, though the number of customers in each type is quite similar (~3200-3400 customers/type), monthly contract witnesses 40% higher churn ratio than the yearly contract.

### Churn rate by group
<img width="1198" alt="Screenshot 2024-05-16 at 12 20 40" src="https://github.com/trinhtran11/powerbi-analyze-customer-churn/assets/167527643/1d2c32a8-1a2f-4180-9c49-581396c6e4a1"><br>
It is popular that telco company offers group package for family household, which is more cost-efficient for customers. In this step, the churn rate is explored in terms of group contract feature. The hypothesis to validate here is that the larger group customers are sharing in the same contract, the less likely customers will churn.
The chart shows customers' average monthly charge and churn rate based on the number of grouped members in their contracts. <br>
* Customers who are not in the group contract (number of member in group = 0) have to pay about $10 higher in monthly average comparing to those who registered in group contract (number of member in group >= 2).
* Average churn rate of individual customers is 32%, equivalent to more than 4 times the levels of grouped customers, which fluctuate at 6% to 8%.

### Churn rate by data plan
This part explores the relationship between data plan usage and churn behavior of customers. For easier to understand and analyze, I grouped customer data consumption level three clusters.<br>

        Consumption = 
        IF(
            'Databel - Data'[Avg Monthly GB Download]<5
            ,"Less than 5 GB"
            ,IF(
                'Databel - Data'[Avg Monthly GB Download]<10
                ,"Between 5 and 10 GB"
                ,"10 or more GB"
            )
        )
<img width="965" alt="Screenshot 2024-05-16 at 13 43 12" src="https://github.com/trinhtran11/powerbi-analyze-customer-churn/assets/167527643/a3e5a2e6-92b2-4814-b8d4-ed45b3c56158"><br>
The bar chart shows that the clients who have taken unlimited plan has higher churn rate than who did not take it when they consume less than or equal 10GB. For those who consume more than 10GB, there is no difference in the churn rate of customers using and not using data plan.<br>

Dive deeper into the price and data plan usage:<br>
<img width="1216" alt="Screenshot 2024-05-16 at 13 56 04" src="https://github.com/trinhtran11/powerbi-analyze-customer-churn/assets/167527643/b466b10b-5520-40a1-9e13-7454cd30b113"><br>
* It is noticeable that the group with highest churn rate at about 35% is those who have taken the data plan and paid the largest average monthly charge at $37.7 but only use less than 5GB.
* Meanwhile, for customers did not take the data plan but use more than 5GB, have to pay more than $30 for extra data charge, making to monthly bill nearly the same with those have already taken the plan. Also, at this level of consumption, two groups of customer witness relatively similar churn rates.<br>
This insight suggests that there is some adjustment or new price package may need to be created in order to downgrade and adjustment in price for the customers who have already registered the unlimited data plan but not utilize much from it. Also, Databel can approach and offer sales to customers having the demand of consuming large amount of data.


### Churn rate by call behavior
By creating a matrix about information of international plan taken by customers and whether there is any international call, I gather the insights related to churn rate in those groups.<br>
<img width="630" alt="Screenshot 2024-05-16 at 14 37 19" src="https://github.com/trinhtran11/powerbi-analyze-customer-churn/assets/167527643/bae73fee-0cfa-4c14-af5d-02c5b6fe46ba"><br>
From this figure, it is obvious that the churn rate of customers who do not call internationally but have already paid for an international plan is high at about 71%.<br>
Vice versa, the churn rate of group customers who have not paid for an international plan but made international call is the second large at about 40%.<br>
This insight suggests that there is the need for the company to contact these groups of customers to offer more competitive offer that matches their demand (example: downgrade those who registered in international plan but not utilize it, offer international plan for those who used it but may not aware of the product).


### Churn rate by customer service calls
<img width="1048" alt="Screenshot 2024-05-16 at 14 40 34" src="https://github.com/trinhtran11/powerbi-analyze-customer-churn/assets/167527643/2f2a297e-caf1-4ff0-98b3-2224b9566e8c"><br>
The chart shows that the more calls customers make to customer service, the higher rate they tend to churn. For customers who make more than 4 calls to customer services, their churn rate reach 100%.<br>
Investigating customer service calls, contract type and payment method, it is found that there is an average of 1.47 calls per customer for those who are in monthly contract and pay by direct debit. The churn rate for this group is at around 54%.

## Propose recommendations
### Demographics-Based Target:
Customizing marketing and services based on different age groups. For instance, survey to understand the need to offer the service or run specific promotion campaign for seniors (group records highest churn rate).

### Geographic Focus:
Diving deeper into regions with high churn rates, such as California to investigate the issues and exploring competitors in those regions.

### Contract Type:
Focusing on improvement, create incentives to promote group contracts and convert monthly-contract customers to yearly contract to encourage customer retention and long term commitment.

### More competitive pricing and offers:
Researching, staying updated with competitors' offers, services and device quality to have neccessary update.
Approach and offer customers a more suitable package or product that matches their needs with lower extra charges in order to retain these groups. The reason is that there are some findings regarding unlimited data plan and international plan indicate that high churn rates come from customers experiencing mismatch between registered product and their actual demand. 

### Customer Service:
Improving the quality of customer service as many customers left due to their dissatisfaction with the attitude and quality of customer service and support.
Identifying if there is any problem with the direct debit payment methods as the method could be related to many customers' calls for support.

## Building dashboard
The dashboard is built to give audience the overview and reveals the insights through analysis. Also, the audience can interact for further exploration as they need.








