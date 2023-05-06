# Wind-Turbine-Analysis
My ongoing project of a wind turbine SCADA data.
------------------------------------------------

#Data:

From https://www.kaggle.com/datasets/psycon/wind-turbine-energy-kw-generation-data
Many thanks for publishing it to: Batucan Senkal - https://www.kaggle.com/psycon

I start with the "features.csv"
This set has:
Rows: 154.262
Columns: 77
Size: 146,3 MiB

---------------------------------------------------------------------------------

#Scenario:

I'm  a technician for wind turbines and just finished my Google Data Analytics Course.\
As I want to enter the field of data analytics, I thougt, this might be a good idea to do an
analysis of a wind turbine. I found this dataaset on Kaggle, this is NOT from any of my employer's turbines.\
\
My scope is on main bearing temperature, generator temperature and power production\
\
Here I'd like to describe the process of this analysis.

-----------------------------------------------------------------------------------

#Tools:

I'm using Libre Office Calc (spreadsheets)

-----------------------------------------------------------------------------------

#Cleaning:

First thing I did, was to use the statistics tool for descriptive statistics to get a first overview.

![image](https://user-images.githubusercontent.com/132265260/236620504-1e0a917a-2f2c-457f-96bf-bbb94758dce1.png)

Min and Max are -273 and 99999. This is the same for other temperature variables.
Power outages, shortcurcits or open wires can cause this issiues.\

Set a filter, remove the unreasonable rows and recheck.\
My main focus is on the bearing temperature, as I found out, on other columns the 99999, was 1300 rows. So I thought it's better to just focus on the columns I want to use later.
The filter for -273 was as expected, in several temperature columns at the same time, overall 26 rows have been removed.\
While filtering, I found some other unreasonable temperatures.

![image](https://user-images.githubusercontent.com/132265260/236621698-04bb25a7-0124-4fa8-8d1a-f5def164a89f.png)

After removing the empty cells and the 99999 cells from the bearing temperature as well, 148.847 rows left.

I repeated the steps for the other columns, try to automate it.

---------------------------------------------------------------------------------------------------------------------------

#Analyzing/Visualizing:






 












