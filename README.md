# Car-Sales-Analysis-Power-Bi-Dashboard
Our company is a car dealership that sells various car models. To effectively track and analyse our sales performance, we need a comprehensive Car Sales Dashboard in Power BI. 

# Objective :
The objective of this project is to design and develop a dynamic and interactive Car Sales Dashboard using Power BI. The dashboard will visualize critical KPIs related to car sales, helping us understand sales performance over time and make data-driven decisions.

# Problem Statement:
The dashboard should provide real-time insights into key performance indicators (KPIs) related to our sales data. This will enable us to make informed decisions, monitor our progress, and identify trends and opportunities for growth.

# Data Cleaning/ Preparation:

- The data consists of over 23907 rows and 16 columns.
- Car_id consist all unique & not null so its our Primary Key.
- From column Engine Replaced Double**A** Overhead Camshaft to DoubleA Overhead Camshaft.
- Created Calender table by pulling date from Car dataset & in calender table created Date,Year,Month Week in Table View.
- converted date into 14 March, 2001 (d mmmm, yyyy) format.
- Dataset was clean enough to perform the analysis directly.
- One to many relationhip has been created.(calendar date(Primary) to car_data_date(foreign key)

# DAX Formulas:

- Calendar Table = CALENDAR(MIN(car_data[Date]),MAX(car_data[Date]))
- Year = YEAR('Calendar Table'[Date])
- Month = FORMAT('Calendar Table'[Date],"MMMM")
- Week = WEEKNUM('Calendar Table[Date]')

# 1.	Sales Overview:
- YTD Total Sales = TOTALYTD(SUM(car_data[Price ($)]),'Calendar Table[Date]')
- PYTD Total Sales = CALCULATE(SUM(car_data[Price ($)]),SAMEPERIODLASTYEAR('Calendar Table[Date]')
- Sales Difference = [YTD Total Sales] - [PYTD Total Sales]
- Sales Diff Colour = If([Sales Difference] > 0,"Green","Red")
- YoY Sales Growth = [Sales Diffrence] / [PYTD Total Sales]   (%)
- MTD Total Sales = TOTALMTD(SUM(car_data[Price ($)]),'Calendar Table'[Date])
- MTD KPI = CONCATENATE("MTD Total Sales : ",FORMAT([MTD Total Sales]/1000000,"$0.00M"))

# 2.	Average Price Analysis:
- Avg Price = SUM(car_data[Price ($)])/ COUNT(car_data[Car_id])
- YTD Avg Price = TOTALYTD([Avg Price],'Calendar Table'[Date])
- PYTD Avg Price = CALCULATE([Avg Price],SAMEPERIODLASTYEAR('Calendar Table'[Date]))
- Avg Price Diff = [YTD Avg Price] - [PYTD Avg Price]
- Avg Price Colour = IF([Avg Price Diff]>0,"Green","Red")
- YoY Avg Price Growth = [Avg Price Diff]/[PYTD Avg Price]   (%)
- MTD Avg Price = TOTALMTD([Avg Price],'Calendar Table'[Date])
- MTD Avg Price KPI = CONCATENATE("MTD Avg Price : ",FORMAT([MTD Avg Price] / 1000,"$0.00K")

# 3.	Cars Sold Metrics:
- YTD Cars Sold = TOTALYTD(COUNT(car_data[Car_id]),'Calendar Table'[Date])
- PYTD Cars Sold = CALCULATE(COUNT(car_data[Car_id]), SAMEPERIODLASTYEAR'Calendar Table'[Date]))
- Cars Sold Diff = [YTD Cars Sold] - [PYTD Cars Sold]
- Cars Sold Colour = IF(car_data[Cars Sold Diff]>0,"Green","Red")
- YoY Cars Sold Growth = [Cars Sold Diff] / [PYTD Cars Sold] (%)
- MTD Cars Sold = TOTALMTD(COUNT(car_data[Car_id]),'Calendar Table'[Date])
- MTD Cars Sold KPI = CONCATENATE("MTD Cars Sold : ",FORMAT([MTD Cars Sold] / 1000,"$0.00K"))

- Max Point on Area Chart = IF(MAXX(ALLSELECTED('Calendar Table'[Week],[Total Sales]) =
    [Total Sales],MAXX(ALLSELECTED('Calendar Table'[Week],[Total Sales]),BLANK()
  

