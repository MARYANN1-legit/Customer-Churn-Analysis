# Customer-Churn-Analysis
Customer churn refers to the phenomenon where customers discontinue their relationship or subscription with a company or service provider. It represents the rate at which customers stop using a company's products or services within a specific period.  over here, we'll be analyzing the factors for the  churn and we'll be proffering solutions 

### DATA SOURCE
Dataset from kaggle

### Tool used
-Excel : Data Cleaning
-SQL Server : Data Analysis
-Power BI : Data Visualization

### Data Cleaning
Data cleaning and pre-processing were carried out at the initial stage to ensure the quality of data
The 
- Data loading and inspection
- Replacing blank spaces with N/A
- fixing the un-standardized date format
- Changing the formats of some columns
- Removing foerign letters using find and Replace



### Exploratory data analysis (EDA)
The EDA process involves understanding data, identifying patterns and detecting anomalies to inform futher analysis(like answering key questions)
1. -- Customer segementation by age group?
2. -- Churn count trend( how has the churn rate change over time)?
3. --  Which sucription type has the highest churn rate?
4. -- Gender with highest churn rate?
5. -- Average age of customers who churn and those who do not?
6. -- How does payment delay affecct churn?
7. --Are customers who make support call more or less likely to churn?

### DATA Analysis
Data analysis was done in SQL

~~~
--q1 customer segementation by age group
select case
when Age>= 18 and age <=28
then '18-28'
when Age >= 29 and Age <= 38
then '29-38'
when Age >=39 and Age <= 48
then '39-48'
when Age >= 49 and Age <= 58
then '49-58'
when Age >=59 then '67+'
else 'unknown'
end as age_group,
COUNT(*) as customer_count
from [churn 1]
group by case

when Age>= 18 and age <=28
then '18-28'
when Age >= 29 and Age <= 38
then '29-38'
when Age >=39 and Age <= 48
then '39-48'
when Age >= 49 and Age <= 58
then '49-58'
when Age >=59 then '67+'
else 'unknown'
end
order by age_group

--q2 churn count trend( how has the churn rate change over time)
select contract_length, round(count(case when churn = 1
then Customer_ID end) * 100/ count (Customer_ID),2) as churn_rate
from [churn 1]
group by Contract_Length
order by Contract_Length;


--q3 which sucription type has the highest churn rate
select [Subscription_Type],
sum(case when churn =1. then 1 end) as churn_count
from  [churn 1]
group by [Subscription_Type];


--q4 gender with highest churn rate
select [Gender], count(case when churn =1. then 1 end) as churn_rate
from  [churn 1]
where churn=1
group by gender
order by churn_rate DESC 
--q5 average age of customers who churn and those who do not
SELECT AVG(AGE) AS Avg_churn_rate
from [churn 1]
where churn =1;
select avg(age) as avg_not_churn_age
from [churn 1]
where churn = 0

--q6 how does payment delay affecct churn

select [Payment_Delay],
sum(case when churn = 1. then 1 end) as churn_count
from [churn 1]
group by Payment_Delay

--q7 are customers who make support call more or less likely to churn
select support_calls, count (case when churn =1. then 1 end)  as churn_count
from [churn 1]
group by support_calls
order by support_calls;
~~~

### Results/Findings

