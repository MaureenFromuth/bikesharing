# Citi Bike Rides

## Overview of Project

Our primary customer for this project is a potential seed investor for you and your friend Kate, who are looking to start up a Citibike business in Des Moines, Iowa.  Using your experience this summer in NYC as inspiration, you are taking a sample of data from Citibike’s August 2019’s operations to conduct analysis and show your investor how this business would work in Iowa.  You want to show your investors the typical breakdown of usage patterns to get a good understanding of what your business would look like, with the aim of getting your seed investor to support you.   More specifically, your proposal needs to answer the following key questions on usage trends:
- How many users did we see in the month of August?
- How many of those users were male, female, or unknown and how many were subscribers vs. one time customers?
- What time of day do most users start riding bikes?
- What time of day do most users start riding their bikes for each day of the week?
- Do those days and hours change based on a persons gender?
- Does the usage per gender for each day of the week change if they are a customer or a subscriber?
- What is the most common length of a bike ride?


To answer these questions, we downloaded a [CVS file] (201908-citibike-tripdata.csv.zip) from Citibike’s public facing site for activity in August 2019.  This data contains a number of different fields to include the following:
- Trip Duration (Sec)
- Start Time (Date Time)
- Stop Time (Date Time)
- Start Station Id (Number)
- Start Station Name (String)
- Start Station Latitude (Number)
- Start Station Longitude (Number)
- End Station Id (Number)
- End Station Name (String)
- End Station Latitude (Number)
- End Station Longitude (Number)
- Bike Id (Number)
- User Type (String)
- Birth Year (Number)
- Gender (Number)


Before conducting our analysis, however, we needed to perform a few key transformation steps on the CSV data.  First, we needed to convert the seconds in the Trip Duration column into minutes and seconds.  We executed this transformation using both Python and Pandas with the code below.  More specifically, we used Pandas to create a dataframe out of the CSV file, and then to convert the data type of the Trip Duration column into a date time format with a unit of milliseconds.  To complete the transformation, we exported the updated dataframe into a new CSV file.  

```
# 1. Create a DataFrame for the 201908-citibike-tripdata data. 
citibike = pd.read_csv("201908-citibike-tripdata.csv")

# 2. Convert the 'tripduration' column to datetime datatype.
citibike['tripduration'] = pd.to_datetime(citibike['tripduration'], unit='m')

# 3. Export the Dataframe as a new CSV file without the index.
citibike.to_csv(r'201908-citibike-tripdata-updated.csv', index=False)
```

Second, once uploaded into Tableau we needed to transform the existing Gender column.  To do so, we needed to first change the data type from number to string.  Then we created a calculated field off of that column and used the following code to create a new column titled, ‘Gender_String’.

```
IF [Gender]=‘0’ then ‘UNKNOWN’
ELSEIF [Gender]=‘1’ then ‘MALE’
ELSEIF [Gender]=‘2’ then ‘FEMALE’ END
```


## Results

The Citibank data provides key details that highlights trends in bike usage, and identifies how Citibikes could be used in Des Moines, Iowa.  Using a Tableau Story, we created the following combination of workbooks and dashboards at this [link](https://public.tableau.com/profile/marty4826#!/).  


***Overview of the Data:  A Good Place to Start***

Let’s take a look at the basics of CitiBike's NYC users in August - there are over 2.3M users, with most of those users being subscribers (approx 80%) and male (approx 70%).  As such, when we break out gender and/or customer type in each of our trend analysis questions, you will see that trend stronger in males and subscribers comparatively.     


>**User Overview Workbook**

[User Overview Workbook](https://public.tableau.com/profile/marty4826#!/vizhome/UserOverviewWorkbook/CitiBike)
