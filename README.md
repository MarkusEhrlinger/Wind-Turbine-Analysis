# Wind-Turbine-Analysis
My project of a wind turbine SCADA data.
------------------------------------------------

#Data:

From https://www.kaggle.com/datasets/psycon/wind-turbine-energy-kw-generation-data

Many thanks for publishing it to: Batucan Senkal - https://www.kaggle.com/psycon

License: CC BY-NC-SA 4.0\
Provenance: This dataset collected from open sources.

I start with the "features.csv"\
This table has:\
Rows: 154.262\
Columns: 77\
Size: 146,3 MiB

---------------------------------------------------------------------------------

#About:

I'm  a technician for wind turbines and just finished my Google Data Analytics Course.\
As I want to enter the field of data analytics, I thougt, this might be a good idea to do an
analysis of a wind turbine. I found this dataaset on Kaggle, this is NOT from any of my employer's turbines.\
\
My focus is on main bearing temperature. 
\
Here I'd like to describe the process of this analysis.\

-----------------------------------------------------------------------------------

#Tools:

I'm using Libre Office Calc (spreadsheets) and R-Studio.

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

I repeated the steps for the other columns. Only 10.689 rows left. I'm rethinking this. Maybe just clean the columns needed.

---------------------------------------------------------------------------------------------------------------------------

#Analyzing/Visualizing:

Although, I cleaned a lot, which might not be suitable for a proper, in depth visualization and/or analysis, I used the descriptive statistics function to take a closer look at the single columns to look if something is catching my attention.\

I can see, max temperature on the bearing is 72°C, in my experience this seems to be a little hot, but I don't know the turbine type or have any data on this, so I will take a closer look to see the temperature change over the years.

![image](https://user-images.githubusercontent.com/132265260/236666996-33fa860a-9d82-485c-ad93-e2927479e4da.png)


So, I go back to the raw data set, filter only this column and create a graph to get a better understanding.\
Maybe I will do this in R, not sure if Calc and my laptop can handle this.

-----------------------------------------------------------------------------------------------

![image](https://user-images.githubusercontent.com/132265260/236668240-fd108263-5383-4996-8c61-f99aaa16a8dc.png)

It looks like, the 72°C isn't too unusual, seems to be a yearly trend.

I continue with R, as it's easier to adjust the visualization to gain some more insight.

```R
X2023_05_04_SCADA_Analysis_workcopy <- read_csv("~/Downloads/Projects/Wind_Turbine_SCADA/2023-05-04_SCADA-Analysis_workcopy.csv")

ggplot(data = X2023_05_04_SCADA_Analysis_workcopy) +
    geom_point(mapping = aes(x = Timestamp, y = Temperature_Bearing_A))
```

![image](https://user-images.githubusercontent.com/132265260/236673125-228cd6d2-18d0-464d-8057-bef1936c826f.png)

```R
# per year
ggplot(data = X2023_05_04_SCADA_Analysis_workcopy) +
  geom_point(mapping = aes(x = Timestamp, y = Temperature_Bearing_A)) +
  facet_wrap(~year(Timestamp))

#per year colored
ggplot(data = X2023_05_04_SCADA_Analysis_workcopy) +
  geom_point(mapping = aes(x = Timestamp, y = Temperature_Bearing_A, color = year(Timestamp))) +
  facet_wrap(~year(Timestamp))
```
![image](https://user-images.githubusercontent.com/132265260/236891434-887331a3-e085-405e-925c-a7307f0fb10f.png)

Need to work with the aestetics, smaller dots and maybe filter, so each plot has only one year

I made smaler dots and made the x-axis for one year only.

```R
startTime <- as_datetime("2019-01-01 00:00:00")
endTime <- as_datetime("2020-01-01 00:00:00")
start.end <- c(startTime, endTime)
start.end

X2023_05_04_SCADA_Analysis_workcopy %>% 
  
  ggplot() +
  geom_point(aes(x = Timestamp, y = Temperature_Bearing_A, color = year(Timestamp)), size = 0.1) +
  (scale_x_datetime(limits = start.end))

```

![image](https://github.com/MarkusEhrlinger/Wind-Turbine-Analysis/assets/132265260/4141d2b7-70a4-43ca-a5b4-cce311dfa6d3)


The single plots, each year in a row.

![image](https://github.com/MarkusEhrlinger/Wind-Turbine-Analysis/assets/132265260/506a00bd-2392-45d9-8e30-14aff01d26d2)


Now I can see easier the different years, the rise in temperature can be explained by the season, outside temperature.
But a closer look to the year 2021 shows, temperatures seem to be a bit higher in the colder months Jan - April  and Oct - Dec as compared to 2019.
Data for 2022 would be needed to see if there's a trend. For now my suggestion would be, to increase the grease cycle for a while or flush the bearing with some extra grease to make sure, the bearing has enough grease. Results should be visible quickly afterwards and if there's a trend or temperature stays at this level, a bearing inspection should be performed, to ensure the bearing isn't already damaged.

---------------------------------------------------------------------------------------------------------

Analysis like this are performed by some AI, which can constantly survey all of the temperatures. For me this was to train my newly learned skills, use some spreadsheet, do some plots in R. 









 












