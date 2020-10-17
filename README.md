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


To answer these questions, we downloaded a [CVS file](201908-citibike-tripdata.csv.zip) from Citibike’s public facing site for activity in August 2019.  This data contains a number of different fields to include the following:
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


>**[User Overview Workbook](https://public.tableau.com/profile/marty4826#!/vizhome/UserOverviewWorkbook/CitiBike)**

![User Overview Workbook](https://github.com/MaureenFromuth/bikesharing/blob/main/Overview.png)




***When Do People Get Bikes?***

What time of day to most people get bikes? In August in NYC, we see users starting rides primarily from 7am-10pm, with the greatest usage from 7am-9am and then again from 4pm-7pm.  This makes sense considering the transit times of most people to/from work.  Additionally, considering the lighter hours in the summer, 7pm is still early enough for daylight and therefore bike riding to be high.  


>**[Ride Start Times in August](https://public.tableau.com/profile/marty4826#!/vizhome/RideStartTimesinAugust/RideStartTimesinAugust)**

![Ride Start Times in August](https://github.com/MaureenFromuth/bikesharing/blob/main/Start%20Times.png)





***What Hour per Day of the Week to Users Take Trips the Most?***

Let's break down the start and end of trips even further into days of the week.  The majority of rides are again between 7am-9am and 5pm-6pm, but not surprisingly they are during the traditional work week of Monday through Friday.   On the weekend, however, we see most rides from 10am-6pm, matching the fact that most people do not work on the weekends and therefore can be out traveling on a bike outside of the transit times.

>**[Trips by Weekday per Hour](https://public.tableau.com/profile/marty4826#!/vizhome/TripsbyWeekdayperHour/TripsbyWeekdayperHour)**

![Trips by Weekday per Hour](https://github.com/MaureenFromuth/bikesharing/blob/main/Weekday%20per%20Hour.png)





***What Hour per Day of the Week to Users Take Trips the Most Based on Gender?***

If we then break the graph above down one step further and look at gender, is there a difference?  As you can see, the trend is the same for male and female riders, but, as we pointed out in the overview, there are more male riders than female.  Interestingly, the trend is slightly different for unknown riders, with the preponderance being on the weekends between 11am and 6pm.  Does this difference in trend have anything to do with whether or not the ‘unknown’ gender is usually assigned to non-subscribing customers who do not have to identify a gender?  

>**[Trips by Gender (Weekday per Hour)](https://public.tableau.com/profile/marty4826#!/vizhome/TripsbyGenderWeekdayperHour_16028153655880/TripsbyGenderWeekdayperHour)**

![Trips by Gender (Weekday per Hour)](https://github.com/MaureenFromuth/bikesharing/blob/main/Gender%20Weekday%20per%20Hour.png)





***Does Weekday Usage per Gender Change Based on User Type?***

If we break down gender usage per day into user types, you see most males and females are subscribers, and unknown tend to be customers.  This answers the question above in the previous assessment, and confirms that a likely reason why you see more ‘unknown’ gender riders on the weekend is because they are typically non-subscribers.  Of note, there is an interesting trend on weekday usage by male and female subscribers: Monday, Tuesday, Thursday and Friday have high usage while Wednesday is less active.  This may be for a number of reasons to include shift work, as many shift-work users will have their overlap days on Wednesday.  


>**[User Trips by Gender by Weekday](https://public.tableau.com/profile/marty4826#!/vizhome/UserTripsbyGenderbyWeekday_16028155069180/UserTripsbyGenderbyWeekday)**

![User Trips by Gender by Weekday](https://github.com/MaureenFromuth/bikesharing/blob/main/Gender%20by%20Weekday.png)





***How Long are Bikes Out For?***

Using the Trip Duration column we transformed, we can see that bike ride duration peaks at 5 min.  For a city, this is fairly common as most places are relatively close together.  There are, however, some users who keep the bike past 5 minutes and some out over well over 24 hours.  

*Of note, the graph below shows hours and minutes, which is what is stated as ‘correct’ in the module.  This is, however, inaccurate - it should be identified as minutes and seconds instead.  This would require a change in the initial Python/Pandas code above from ‘m’ as units to ’ns’ as units.  In order to keep with the module, I did not make any changes but you can see in this paragraph the changes I would have made.* 


>**[Checkout Times for Users](https://public.tableau.com/profile/marty4826#!/vizhome/CheckoutTimesforUsers_16028148200070/CheckoutTimesforUsers)**

![Checkout Times for Users](https://github.com/MaureenFromuth/bikesharing/blob/main/Checkout%20Times.png)





***How Long are Bikes Out For Based On Gender?***

If we dive one level deeper, we can see that bike ride duration peaks at 5 min for both males and females, but is steady for unknown.  Again, with the knowledge of the overall breakout from our first analysis and study of the overall data, this is not surprising.  

*Of note, as with the previous graph, the graph below shows hours and minutes, which is what is stated as ‘correct’ in the module.  This is, however, inaccurate - it should be identified as minutes and seconds instead.  This would require a change in the initial Python/Pandas code above from ‘m’ as units to ’ns’ as units.  In order to keep with the module, I did not make any changes but you can see in this paragraph the changes I would have made.* 


>**[Checkout Times by Gender](https://public.tableau.com/profile/marty4826#!/vizhome/CheckoutTimesforUsers_16028148200070/CheckoutTimesforUsers)**

![Checkout Times by Gender](https://github.com/MaureenFromuth/bikesharing/blob/main/Checkout%20Times%20by%20Gender.png)



