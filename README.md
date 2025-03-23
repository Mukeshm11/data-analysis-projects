# Bank Loan Report

### Dashboard Link : https://app.powerbi.com/groups/me/reports/abb32d53-6f84-47cb-9c03-de1bea2b2d2f/f771e6bd4c2799630079?experience=power-bi

## Problem Statement

The Bank Loan Dashboard assists financial institutions in managing, analyzing, and streamlining the loan approval process. In order to help banks make well-informed lending decisions, this dashboard offers a thorough overview of loan applications, approvals, rejections, default risks, and borrower demographics.
Banks and other financial organizations can use this dashboard to:

- Track trends in loan approval and rejection to pinpoint important variables affecting lending choices.

- Determine a borrower's creditworthiness by looking at their income, credit scores, and loan repayment history.

- Analyze default risks by monitoring past-due loans, high-risk segments, and repayment trends.

- Determine the most lucrative and low-risk client segments to maximize loan offerings.
- Simplify the loan application review procedure to increase operational efficiency.

- Enhance financial risk management by using historical trend analysis and predictive analytics.

By making strategic, data-driven decisions in loan management, this dashboard helps financial institutions to minimize loan default rates, improve lending efficiency, and improve customer satisfaction.


### Steps followed 

- Step 1 : Load data into Power BI Desktop, datasource is a SQL Server.

- Step 2 : Open power query editor & in view tab under Data preview section, check "column distribution", "column quality" & "column profile" options.

- Step 3 : Also since by default, profile will be opened only for 1000 rows so you need to select "column profiling based on entire dataset".
- Step 4 : It was observed that in none of the columns errors & empty values were present except column named "Emp title".
- Step 5 : A new table, called 'Date Table', was created using the CALENDAR function in DAX. The 'Date Table' includes a column named 'Date', which contains a continuous sequence of dates ranging from the earliest loan issue date to the latest loan issue date in the dataset.
The DAX formula used to create this table is:

     Date Table = CALENDAR(MIN(financial_loan[issue_date]),MAX(financial_loan[issue_date])) 

- Step 6 : In the report view, under the view tab, theme was selected.

- Step 7 : New measure was created to find total count of customers ID.

Following DAX expression was written for the same,
        
       Total loan applications = COUNT(financial_loan[id])
        
and also added a new Measure to calculate the Month-to-Date (MTD) loan applications, which means it returns the total number of loan applications received from the start of the current month up to the current date.
        
        MTD loan applications = CALCULATE(TOTALMTD([total loan applications],'Date Table'[Date]))


added a new measure which measures the percentage change in loan applications compared to the previous month.

        MOM loan applications = ([MTD loan applications]-[PMTD loan applications])/[PMTD loan applications]

A card visual was used to represent Total loan applications, MTD loan applications & MOM loan applications.

![Image](https://github.com/user-attachments/assets/c32916cd-aed5-4277-bab8-59cb933eb344)

        
 - Step 8 : New measure was created to find  Total Funded Amount,
 
 Following DAX expression was written to find Total Funded Amount,
 
         Total funded amount = CALCULATE(SUM(financial_loan[loan_amount]))
 
DAX expression written to find MTD funded amount

        MTD funded amount = CALCULATE(TOTALMTD(SUM(financial_loan[loan_amount]),'Date Table'[Date].[Date]))
        
DAX expression written to find MOM funded amount

        MOM Funded Amount = ([MTD funded amount] - [PMTD Funded Amount])/ [PMTD Funded Amount]

        where
         PMTD Funded Amount = CALCULATE(SUM(financial_loan[loan_amount]),DATESMTD(DATEADD('Date Table'[Date],-1,MONTH)))

 A card visual was used to represent this 
 
 
 
 ![Image](https://github.com/user-attachments/assets/9e97e0d5-c6ab-42ec-9ce9-c252aa61a689)

 
 - Step 9 : New measure was created to find  Total Amount Received,
 
 Following DAX expression was written to find Total Amount Received,
 
         Total amount received = CALCULATE(SUM(financial_loan[total_payment]))
 
DAX expression written to find MTD amount Received

        MTD amount received = CALCULATE(SUM(financial_loan[total_payment]),DATESMTD('Date Table'[Date]))
        
DAX expression written to find MOM amount received

        MOM amount received = ([MTD amount received] - [PMTD amount received]) / [PMTD amount received]

        where
         PMTD amount received = CALCULATE(TOTALMTD(SUM(financial_loan[total_payment]),DATEADD('Date Table'[Date],-1,MONTH)))

 A card visual was used to represent this 
 
 
 
 ![Image](https://github.com/user-attachments/assets/3beda159-9175-4a40-b6c7-879dd8eb1b14)
 
 
- Step 10 : New measure was created to find  Average Intereset Rate,
 
 Following DAX expression was written to find Total Amount Received,
 
         Average Interest Rate = CALCULATE(Average(financial_loan[int_rate]))
 
DAX expression written to find MTD Intereset Rate

        MTD Interest Rate = CALCULATE(AVERAGE(financial_loan[int_rate]),DATESMTD('Date Table'[Date]))
        
DAX expression written to find MOM amount received

        MOM Interest Rate = ([MTD Interest Rate] - [PMTD Interest Rate]) / [PMTD Interest Rate]

        where
         PMTD Interest Rate = CALCULATE(AVERAGE(financial_loan[int_rate]),DATESMTD(DATEADD('Date Table'[Date],-1,MONTH)))

 A card visual was used to represent this 
 
 
 
![Image](https://github.com/user-attachments/assets/800852d8-38a3-4cdb-9552-9576a0d01fde)
 
 - Step 11 : New measure was created to find  Average Debt to Income ratio,
 
 Following DAX expression was written to find Total Amount Received,
 
         Average DTI= CALCULATE(Average(financial_loan[dti]))
 
DAX expression written to find MTD DTI

        MTD Average DTI = CALCULATE(AVERAGE(financial_loan[dti]),DATESMTD('Date Table'[Date]))
        
DAX expression written to find MOM amount received

        MOM Average DTI = ([MTD Average DTI] - [PMTD average DTI]) / [PMTD average DTI]

        where
         PMTD Average DTI = CALCULATE(AVERAGE(financial_loan[dti]),DATESMTD(DATEADD('Date Table'[Date],-1,MONTH)))

 A card visual was used to represent this 
 
 
 
![Image](https://github.com/user-attachments/assets/2cf10205-1fc1-4895-80de-bdf4d24a8040)
 
- step 12 : New graph visual for Total loan application by month

![Image](https://github.com/user-attachments/assets/887be0aa-99b1-487d-87c8-3e4b8ba2ef4d)


- step 13 : New Map visual for Total loan application by address

![Image](https://github.com/user-attachments/assets/dbf2255d-7899-4781-8ebf-d84d651d1509)

 - step 14 : New Treemap visual for Total loan application by address

![Image](https://github.com/user-attachments/assets/541ccccd-87e5-4744-b209-6fc64c2ab6ba)

- step 15 : New Clustered bar chart visual for Total loan application by pupose

![Image](https://github.com/user-attachments/assets/9ad48164-4fa2-430f-82cb-60f87e0d2256)


- step 16 : New Donut chart visual for Total loan application by term

![Image](https://github.com/user-attachments/assets/c505c647-0932-40d0-8e5a-f72412a9723a)

- step 17 : New Clustered bar chart visual for Total loan application by employee lenght

![Image](https://github.com/user-attachments/assets/a7e66bf5-91df-461b-b56e-d87a13626407)


 - Step 18 : The report was then published to Power BI Service.
 

## Snapshot of Summary Dashboard (Power BI Desktop)

![Image](https://github.com/user-attachments/assets/ec4910e2-b4c5-45c7-809f-665ba85b379a)


 
 # overview Snapshot (Power BI DESKTOP)

 
![Image](https://github.com/user-attachments/assets/e6cb64c6-d573-45a3-a3c8-4801db1c1df5)

# Repor Snapshot (Power BI DESKTOP)

 
![Image](https://github.com/user-attachments/assets/3b77acfe-3c4d-4357-9ce9-073e13e2ef53)

# Insights

A single page report was created on Power BI Desktop & it was then published to Power BI Service.

Following inferences can be drawn from the dashboard;

###  Total loan applications = 38.6K

        Total number of good loan issued = 33.2K

        Total number of Bad  loan issued = 5.3K

### Total Funded Amount = $435.8M

        Good loan funded amount = $370.2 M

        Bad loan funded amount = $65.5.2 M


### Total Amount received = $473.1 M

        Good loan total received = $435.8 M

        Bad  loan total received = $37.3 M

### Average Intereset Rate = 12.05%

### Average DTI (Debt to Income Ratio) = 13.33%

### Loan status
         Fully paid loan applications: 32.1K
         Current loan applications: 1.08 K
         Charged off loan applications: 5.3 K

#### Loan applications by month
        The month of December recorded the highest number of loan applications, with a total of 4.3K applications. This indicates a seasonal spike in loan demand, possibly driven by year-end financial planning, holiday expenditures, or business investments.

#### Amount funded and received by State
        The state of California (CA) recorded the highest loan funding, with a total amount of $78.5 million funded and $83.9 million received. This indicates strong loan demand and financial activity in the state, potentially driven by high business investments, real estate financing, or economic growth.

#### Total loan applications by purpose 
        The highest number of loan applications was recorded for the purpose of data consolidation, with a total of over 18 K applications. This suggests that a significant number of borrowers are seeking loans to merge existing debts into a single payment

#### Total loan applications by emp_lenght
        Employees with a work tenure of 10+ years have the highest number of loan applications, indicating that individuals with long-term job stability are more likely to seek financial support. This is followed by employees with less than 1 year and 2 years of employment, suggesting that both experienced professionals and relatively new employees have significant borrowing needs.
