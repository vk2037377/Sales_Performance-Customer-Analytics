# Sales_Performance-Customer-Analytics
End-to-End Data Analytics Project using Excel, Python, MySQL and Power BI.

uploaded the excel doc using python pandas and sqlalchemy
import pandas as pd
from sqlalchemy import create_engine

df = pd.read_csv(r'SSCD1.csv')

engine = create_engine(
    "mysql+pymysql://root:password@localhost:3306/sales_analysis"
)

df.to_sql(
    name="ssreport",
    con=engine,
    if_exists="append",
    index=False
)

---------------------------------------------------------------------------------------------------------------------------------------------------------

check the sql analysis 
Once the data received in mysql database:

*) SELECT SUM(Sales) FROM orders;
*) SELECT Customer_Name, SUM(Sales) AS Revenue FROM orders GROUP BY Customer_Name ORDER BY Revenue DESC LIMIT 10;
*) SELECT YEAR(Order_Date), MONTH(Order_Date), SUM(Sales) FROM orders GROUP BY YEAR(Order_Date), MONTH(Order_Date);
*) SELECT Category, SUM(Sales) Revenue FROM orders GROUP BY Category ORDER BY Revenue DESC;
*) SELECT Region, SUM(Sales), SUM(Profit) FROM orders GROUP BY Region;
*) SELECT Customer_Name, SUM(Sales),RANK() OVER(ORDER BY SUM(Sales) DESC) Customer_Rank FROM orders GROUP BY Customer_Name;

----------------------------------------------------------------------------------------------------------------------------------------------------------

Connect SQL to Power BI

Open Power BI.
Home → Get Data → MySQL/PostgreSQL
Connect database.
Load table.

Using DAX Funcition to create calculations that do not exist directly in the dataset.
*) Total Sales = SUM(ssreport[Sales])
*) Total_profit = SUM('sales_analysis ssr'[Profit])
*) Total_order = COUNT('sales_analysis ssr'[Order_ID])
*) Total_margin = DIVIDE([Total_profit], [Total_sales],0)
*) Total_customer = DISTINCTCOUNT('sales_analysis ssr'[Customer_Name])
*) Avg_Rev_Per_Customer = DIVIDE([Total_sales], [Total_customer],0)

Create the dashboards and pasted screenshot FYR
Sales Performance:
<img width="1738" height="727" alt="image" src="https://github.com/user-attachments/assets/001b524c-1068-4708-9d8c-0b12731bdea1" />
Customer analytics:
<img width="1307" height="732" alt="image" src="https://github.com/user-attachments/assets/19d4de32-f9d0-44df-b3be-de60061d7814" />
Insights:
<img width="1350" height="598" alt="image" src="https://github.com/user-attachments/assets/e51a6c70-3575-4f56-9891-8f41164c80ea" />

----------------------------------------------------------------------------------------------------------------------------------------------------------














