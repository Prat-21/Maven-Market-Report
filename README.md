![Maven_Market](https://github.com/Prat-21/Maven-Market-Report/assets/165648053/bbbec253-6b0a-4503-bd26-57b47b998329)



# Maven Market Data Analysis


![Screenshot (15)](https://github.com/Prat-21/Maven-Market-Report/assets/165648053/08f3f89b-2d9d-4271-8937-9e96eb3debc1)



## Maven Market Project

For this project, I used Power BI to clean, analyze and visualize a data set from Maven Analytics called Maven Market. Maven Market is a business which owns a variety of grocery stores of differing sizes across multiple countries including the United States, Canada and Mexico.

In this dashboard analysis, I will review the insights I gained while creating the report. This project was a bonus project from the Power BI Desktop For Business Intelligence Course from Maven Analytics.

## Data Cleaning

The raw data came in the from of CSV files which were then brought into Power BI using Get Data. The data was then transformed and cleaned into a more workable set. This process was repeated for each table/CSV file.

The cleaning process for this dataset was fairly straightforward requiring mainly header promotion, data type corrections and creation of additional columns that made working with the dataset easier later on. Additionally, the raw dataset provided 2 tables for transactions, one for each year (1997 and 1998). As both of these tables had the same table and column structure, they were appended into one table titled “Transactions Data” containing both years. I then conducted data verification and ensured that the new table contained the correct number of rows and columns.



![Screenshot (16)](https://github.com/Prat-21/Maven-Market-Report/assets/165648053/7b7bd62c-7ad4-4a4b-90b3-fdfe66dda813)



## Data Modeling

After ensuring my data’s accuracy and consistency, I began the process of creating a data model for my tables. I connected 'Stores' and 'Regions' as a snowflake schema. Both the fact tables i.e. 'Transaction Data' and 'Return Data' were placed at the bottom and the dimension tables above them. This was done to achieve ease of viewing cardinality and cross filter direction.



![Screenshot (17)](https://github.com/Prat-21/Maven-Market-Report/assets/165648053/1a0d1635-3fb3-4826-a72b-74116ac067d0)



## DAX Functions

Now that I had established my table relationships, I began writing DAX functions to create measures. These were used to calculate my KPI’s and other metrics which would later be placed inside my visuals. Some of the functions I used include:

**1**.**CALCULATE**():  This function was essential in the calculation of metrics such as those dealing with Returns, Profits, Revenue and Transactions.

                                      Last Month Transactions = CALCULATE([Total Transactions],
                                                 DATEADD('Calendar'[date],-1,MONTH))

**2**.**ALL**(): This function was used in conjunction with the CALCULATE function to assist with the calculation of Returns, Profits, Revenue and Transactions by overriding all filter context.

                                      All Returns = CALCULATE([Total Returns], ALL(Return_Data))

 **3**. **DATESINPERIOD**(): It was used to create a 60-Day Revenue measure by using the CALCULATE function to take the Total Revenue from the last 60 days by specifying the DATESINPERIOD to use the Date column and further utilize the MAX function on that same column, adding our interval of -60, and then specifying type as DAY.

                                      60-Day Revenue = CALCULATE([Total Revenue],
                                             DATESINPERIOD('Calendar'[date], MAX('Calendar'[date]),-60,DAY))

**4**.**SUM/SUMX**(): Both SUM and SUMX were used in the report. The iterator function SUMX was used to calculate the 'Total Cost' by multiplying the Quantity column from the Transactions table with the Product Cost Column in the Product Lookup table through the use of the RELATED() function

                                      Total Cost = SUMX(Transaction_Data, Transaction_Data[quantity] * RELATED(Products[product_cost]))

**5**.**COUNTROWS/DISTINCTCOUNT**: This function was used to calculate the measure 'Total Returns' by counting the number of rows in the Returns Data table.

                                      Total Returns = COUNTROWS(Return_Data)

