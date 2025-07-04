# TechStream Solutions

![image](https://github.com/user-attachments/assets/063261b0-8158-4447-be50-d5482a2eabd3)

## I . Introduction

The company is called "TechStream Solutions", and the product is a Software as a Service (SaaS) platform named "Streamline Pro". This platform provides comprehensive project management and collaboration tools for businesses of all sizes.

TechStream Solutions has been operating for several years and has gathered significant data on their costs and revenues. They are now looking to analyze their unit economics to understand the profitability of Streamline Pro on a per-customer basis.

The datasets are in the shared folder on Google Drive: <https://drive.google.com/drive/folders/1qhOW9Y2orRXuzbX-kXEmuJ7TMQiRs2Uv?usp=drive_link>

## II. IMPORT
### 1. Import Libraries and Data
```
import pandas as pd
```

Data `Monthly_expense`
```
google_sheet_id = '10OGbaywwMIqKgnPGy8VDvpBVtjyqln47iYa2lFhI9Mw'
url = 'https://docs.google.com/spreadsheets/d/' + google_sheet_id + '/export?format=xlsx'
month_expense = pd.read_excel(url, sheet_name='Sheet1')
```
Data `payroll`
```
google_sheet_id = '1c_WihqTZCQvNgxzmd-OwhR9i5diwtfxXVLyMn8R-Lp4'
url = 'https://docs.google.com/spreadsheets/d/' + google_sheet_id + '/export?format=xlsx'
pay_roll = pd.read_excel(url, sheet_name='Sheet1')
```
Data `daily_marketing_spending`
```
google_sheet_id = '1AZOIThOV4P-0eYDge53ZwumVkfkHoYPWxst3k3Bv87c'
url = 'https://docs.google.com/spreadsheets/d/' + google_sheet_id + '/export?format=xlsx'
daily_marketing = pd.read_excel(url, sheet_name='Sheet1')
```
Data `customer_lifespan_data`
```
google_sheet_id = '1by8tPHwOnq3uKYK2E7sA9VBUYoPM4p1Rnrm_Ss9cyHI'
url = 'https://docs.google.com/spreadsheets/d/' + google_sheet_id + '/export?format=xlsx'
lifespan = pd.read_excel(url, sheet_name='Sheet1')
```
## III. CALCULATION
### 1.CAC: Customer Acquisition Cost
`CAC = [Total Sales and Marrketing Expenses] / [Number Of New Cusstomers Acquired]`

CAC (Customer Acquisition Cost) is calculated by dividing the total Sales & Marketing expenses—including marketing software costs, salaries, and daily marketing spend—by the number of new customers acquired.

### 1.1 Marketing Software Expense
```
month_expense.sample(5)
```
![image](https://github.com/user-attachments/assets/c318338e-bf9a-4e36-aa4f-1f9d5165cdb7)

```
expense_mar = monthly_expense[monthly_expense['month'] == '2023-03-01']
expense_crm = expense_mar[expense_mar['item'] == 'Salesforce']['amount'].sum()
```
> The cost of the Marketing Software Expense is $1,700.
> In March 2023, we extracted the Marketing Software Expense by filtering for the item "Salesforce", which totaled $5,950. This amount is included in the total marketing cost used to calculate the Customer Acquisition Cost (CAC).

### 1.2 Sales & Marketing Salaries
```
pay_roll.sample(5)
```
![image](https://github.com/user-attachments/assets/b9efe5ec-f922-44d1-b29d-c10be8793404)
```
pay_roll_202303 = pay_roll[pay_roll['month'] == '2023-03-01']
sale_marketing_salary = pay_roll_202303[
    (pay_roll['department'] == 'Sales') |
    (pay_roll['department'] == 'Marketing')
]['paid'].sum()
```
> The cost of Sales & Marketing Salaries is $5,950.
> In March 2023, the total amount paid to employees in the Sales and Marketing departments was $5,950. This value represents the Sales & Marketing Salaries, and is included in the total expense used to calculate Customer Acquisition Cost (CAC).

### 1.3 Daily Marketing Expense
```
daily_marketing.sample(5)
```
![image](https://github.com/user-attachments/assets/017335a9-31aa-4fcc-a607-b6270c0df0ca)

```
daily_marketing_202303 = daily_marketing[(daily_marketing['date'] >= '2023-03-01') & (daily_marketing['date'] <= '2023-03-31')]
daily_marketing_expense = daily_marketing_202303['spending'].sum()
```
> The cost of the Daily Marketing Expense is $68,830.
> In March 2023, the total Daily Marketing Expense amounted to $68,830. This value is included in the total marketing cost for calculating the Customer Acquisition Cost (CAC).

### 1.4 Number of New Customer
```
customer_recepts.sample(5)
```
![image](https://github.com/user-attachments/assets/85474fa0-a856-494d-81f1-9d2fe8e67de5)

```
customer_recepts_202303 = customer_recepts[(customer_recepts['date'] >= '2023-03-01') & (customer_recepts['date'] <= '2023-03-31')]
new_of_customer = customer_recepts_202303[customer_recepts_202303['new_customer'] == 1]['customer_id'].nunique()
```
>The number of new customers is 63.

### 1.5 CAC calculation
```
total_acquition_cost = crm_expense + sale_marketing_salary + daily_marketing_expense
cac = round(total_acquition_cost/ new_of_customer, 2)
```
>The Customer Acquisition Cost (CAC) is $1,213.97.
-> This means that, on average, it costs $1,213.97 to acquire one new customer.
We should consider: Is the value and long-term revenue from each new customer worth this cost?

### 2.  ARPU: Average Revenue Per User
`APRU = [Total Revenue] / [Number of Users]`

Total Revenue
```
total_revenue = customer_recepts_202303['receipt_amount'].sum()
```
 `83033`

Number of Customer
```
number_of_customer = customer_recepts_202303['customer_id'].nunique()
```
 `292`

APRU
```
ARPU = round(total_revenue/number_of_customer, 2)
```
 `284.36`
 
=> We can understand that ARPU (Average Revenue Per User) is $284.36, meaning that on average, each customer generates $284.36 in revenue for the business. This metric helps evaluate how effectively the company earns revenue per customer and serves as a basis for comparing with CAC to assess the potential profitability of acquiring new customers.

### 3. COGS: Cost of Goods Sold
`COGS = [Software Expenses] + [Production]`
Software Expenses : Calculates the total software expenses for production (COGS) in March 2023, including AWS Hosting, Google Cloud Storage, and Atlassian Jira.
```
production_expense = ['AWS Hosting','Google Cloud Storage','Atlassian Jira']
softwware_expense = expense_202303[expense_202303['item'].isin(production_expense)]['amount'].sum()
```

