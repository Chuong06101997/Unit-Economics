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






