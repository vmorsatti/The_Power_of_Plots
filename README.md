

```python
# Pyber - Week 5 Assignment by Verna Orsatti June 18, 2018
# Updated with new data files on June 12
```

# Pyber Ride Sharing Trends

In the following Bubble Chart for year 2018, data values of dated, individual rides are summarized in the bubble, representing the number of rides per city and it's average fare.  Each bubble is further represented by a size relative to the number of drivers per city. 

The chart effectively shows the trend that rides in rural areas are higher priced. It is possible that the higher average price of rides in rural areas is affected by greater distances traveled to other locations. Prices could be higher due to the lesser number of drivers as well as seen in traditional supply and demand curves.

As population density increases, with urban being the most highly denes, individual average ride costs goes down. Reasons for lower ride cost are most likely explained by more numbers of short distance rides, and more drivers available, leading to competition.  What these charts don't show is the actual relationship between city and population to see how the numbers of drivers are relation to population that would give insight into trends towards driving privately or through Pyber rides.
 
With the values for suburban locations are somewhere in-between rural and urban.  It is safe to conlude that:
1) Rides prices are going to range from higher to lower prices as population density increases as shown in ride type. 
2) The number of rides increases with density and,
3) The number of drivers increases with density.

As the provided pie charts show, the proportions of of rides, drivers, and fares by city type are fairly consistant across the three charts, further showing the direct relation of price being the element that is affected by density of where rides occur.
There is a slight reduction in fares in rural areas that can be likely explained be the necessity of having personal owned transportation due to distances and driver availability.


```python
## Option 1: Pyber

# * You must use the Pandas Library and the Jupyter Notebook.
# * You must use the Matplotlib and Seaborn libraries.

# * You must include a written description of three observable trends based on the data.

# * You must include an exported markdown version of your Notebook called
#         `README.md` in your GitHub repository.
# * See [Example Solution](Pyber/Pyber_Example.pdf) for a reference on expected format.
```


```python
#Utilities
import os
import csv
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```


```python
# Read and Merge Data
city_data = pd.read_csv('city_data.csv')
# city_data.head(5)
# city_data.shape # > (120,3)
```


```python
ride_data = pd.read_csv('ride_data.csv')
# ride_data.shape  # > (2375, 4)
```


```python
# Merged csv files into 1 dataframe
merge_df = pd.merge(ride_data, city_data, on="city")

print(merge_df)
```

                        city                 date   fare        ride_id  \
    0     Lake Jonathanshire  2018-01-14 10:14:22  13.83  5739410935873   
    1     Lake Jonathanshire  2018-04-07 20:51:11  31.25  4441251834598   
    2     Lake Jonathanshire  2018-03-09 23:45:55  19.89  2389495660448   
    3     Lake Jonathanshire  2018-04-07 18:09:21  24.28  7796805191168   
    4     Lake Jonathanshire  2018-01-02 14:14:50  13.89   424254840012   
    5     Lake Jonathanshire  2018-04-06 11:30:32  16.84  6164453571846   
    6     Lake Jonathanshire  2018-03-21 00:18:34  37.95  8353656732934   
    7     Lake Jonathanshire  2018-01-28 00:07:00   5.67  9756573174778   
    8     Lake Jonathanshire  2018-01-24 12:24:22  34.65  3319117904437   
    9     Lake Jonathanshire  2018-03-24 16:27:49  14.94  1670908453476   
    10    Lake Jonathanshire  2018-04-11 22:10:30  12.81  5999870428814   
    11    Lake Jonathanshire  2018-01-23 21:43:16  21.11  7711472105447   
    12    Lake Jonathanshire  2018-01-29 00:19:07  41.05  6649692036139   
    13    Lake Jonathanshire  2018-03-22 14:33:32  18.72  4675968803527   
    14    Lake Jonathanshire  2018-04-16 20:26:30  32.47  1013873953228   
    15    Lake Jonathanshire  2018-04-11 19:49:34  25.92  8533808747676   
    16    Lake Jonathanshire  2018-04-09 21:41:30  15.96   577276092645   
    17    Lake Jonathanshire  2018-01-16 09:27:03  26.27  3267656258507   
    18    Lake Jonathanshire  2018-01-21 12:12:56  37.25  2966536034637   
    19    Lake Jonathanshire  2018-04-11 21:32:27  22.48  3505458786874   
    20    Lake Jonathanshire  2018-02-16 01:49:45  17.58  3641777572467   
    21    Lake Jonathanshire  2018-01-17 13:15:58  28.42  6544222037368   
    22    Lake Jonathanshire  2018-01-21 09:48:28  22.36  2522096563712   
    23    Lake Jonathanshire  2018-02-23 06:10:30  26.63  5372487991955   
    24    South Michelleport  2018-03-04 18:24:09  30.24  2343912425577   
    25    South Michelleport  2018-03-02 09:54:50  33.12   813844006721   
    26    South Michelleport  2018-01-08 09:38:14  23.77  4916160406018   
    27    South Michelleport  2018-04-22 03:15:33  43.62  4663606096929   
    28    South Michelleport  2018-03-03 16:13:34  41.62  2339775503972   
    29    South Michelleport  2018-01-27 19:38:12  15.45  7465262064048   
    ...                  ...                  ...    ...            ...   
    2345          Newtonview  2018-04-01 13:39:13  26.73  3723530332713   
    2346          Newtonview  2018-04-25 10:20:13  55.84  9990581345298   
    2347         North Jaime  2018-03-06 09:09:23  44.17  1152195873170   
    2348         North Jaime  2018-03-12 13:05:56  23.21  5987447089759   
    2349         North Jaime  2018-04-04 13:13:40  51.83  9116047435376   
    2350         North Jaime  2018-02-01 08:59:24  17.05  9481117811603   
    2351         North Jaime  2018-05-06 00:58:17  41.18  7328094869758   
    2352         North Jaime  2018-04-04 01:58:37  43.86  8195436622338   
    2353         North Jaime  2018-04-27 17:58:27  14.01  2156688209209   
    2354         North Jaime  2018-02-10 21:03:50  11.11  2781339863778   
    2355         Penaborough  2018-02-24 00:44:00  21.89  2069309881916   
    2356         Penaborough  2018-04-27 06:02:10  38.33   547013925055   
    2357         Penaborough  2018-01-14 15:58:48  54.10   432925983890   
    2358         Penaborough  2018-02-03 17:15:31  51.80  5383427508621   
    2359         Penaborough  2018-01-22 15:36:24  10.11  4129933467653   
    2360      Harringtonfort  2018-01-06 07:38:40  47.33  3849747342021   
    2361      Harringtonfort  2018-02-17 04:42:56  30.58  6835140871685   
    2362      Harringtonfort  2018-04-16 16:30:50  17.39  4023962353348   
    2363      Harringtonfort  2018-03-10 10:11:37  19.02  6717313402790   
    2364      Harringtonfort  2018-02-26 07:03:11  54.66  9201585331171   
    2365      Harringtonfort  2018-01-09 15:30:35  31.84  3730685356921   
    2366        West Heather  2018-03-12 04:22:26  26.55  7035849392668   
    2367        West Heather  2018-02-22 09:01:37  17.40  8702491506161   
    2368        West Heather  2018-02-22 01:46:43  33.38  5551691454078   
    2369        West Heather  2018-02-04 16:29:23  13.97  7118893881453   
    2370        West Heather  2018-04-18 19:33:12  46.60  3671003215967   
    2371        West Heather  2018-03-02 21:04:10  20.99  5766454453070   
    2372        West Heather  2018-03-06 20:06:51  48.11  2570548892682   
    2373        West Heather  2018-02-02 06:28:04  53.07  2462950442268   
    2374        West Heather  2018-05-07 19:22:15  44.94  4256853490277   
    
          driver_count   type  
    0                5  Urban  
    1                5  Urban  
    2                5  Urban  
    3                5  Urban  
    4                5  Urban  
    5                5  Urban  
    6                5  Urban  
    7                5  Urban  
    8                5  Urban  
    9                5  Urban  
    10               5  Urban  
    11               5  Urban  
    12               5  Urban  
    13               5  Urban  
    14               5  Urban  
    15               5  Urban  
    16               5  Urban  
    17               5  Urban  
    18               5  Urban  
    19               5  Urban  
    20               5  Urban  
    21               5  Urban  
    22               5  Urban  
    23               5  Urban  
    24              72  Urban  
    25              72  Urban  
    26              72  Urban  
    27              72  Urban  
    28              72  Urban  
    29              72  Urban  
    ...            ...    ...  
    2345             1  Rural  
    2346             1  Rural  
    2347             1  Rural  
    2348             1  Rural  
    2349             1  Rural  
    2350             1  Rural  
    2351             1  Rural  
    2352             1  Rural  
    2353             1  Rural  
    2354             1  Rural  
    2355             6  Rural  
    2356             6  Rural  
    2357             6  Rural  
    2358             6  Rural  
    2359             6  Rural  
    2360             4  Rural  
    2361             4  Rural  
    2362             4  Rural  
    2363             4  Rural  
    2364             4  Rural  
    2365             4  Rural  
    2366             4  Rural  
    2367             4  Rural  
    2368             4  Rural  
    2369             4  Rural  
    2370             4  Rural  
    2371             4  Rural  
    2372             4  Rural  
    2373             4  Rural  
    2374             4  Rural  
    
    [2375 rows x 6 columns]


# Bubble Plot of Ride Sharing Data


```python
# Prep for Bubble Chart
```


```python
# Total Number of Rides All Cities
num_rides_city = merge_df.groupby('city').ride_id.count().tolist() #
# num_rides_city
# sum(num_rides_city) # = 2375
```


```python
# 3 City Types (Urban, Surburban, Rural) for Bubble Chart
```


```python
# Ride type = Rural data
rural_rides_city = merge_df.query('type == "Rural"')
# Number of Rides per City
num_rides_city_rural = rural_rides_city.groupby('city').ride_id.count().tolist()
# Average Fare ($) in Rural 
ave_fare_rural = rural_rides_city.groupby('city').fare.mean().tolist()
# Number of Drivers per City 
size_rural = rural_rides_city.groupby('city').driver_count.mean().tolist()
```


```python
# Ride type = Surburban data
suburban_rides_city = merge_df.query('type == "Suburban"')
# Number of Rides per City
num_rides_city_suburban = suburban_rides_city.groupby('city').ride_id.count().tolist()
# Average Fare ($) 
ave_fare_suburban = suburban_rides_city.groupby('city').fare.mean().tolist()
# Number of Drivers per City 
size_suburban = suburban_rides_city.groupby('city').driver_count.mean().tolist()
```


```python
# Ride type = Urban data
urban_rides_city = merge_df.query('type == "Urban"')
# Number of Rides per City
num_rides_city_urban = urban_rides_city.groupby('city').ride_id.count().tolist()
# Average Fare ($) 
ave_fare_urban = urban_rides_city.groupby('city').fare.mean().tolist()
ave_fare_suburban = suburban_rides_city.groupby('city').fare.mean().tolist()
# Number of Drivers per City 
size_urban = urban_rides_city.groupby('city').driver_count.mean().tolist()
```


```python
#Prepare for Bubble Chart
sns.set()

plt.figure(figsize=(8,6))
plt.xlim(0,40)
plt.ylim(15,45)

plt.scatter(num_rides_city_rural, ave_fare_rural, s=rural_rides_city['driver_count']*4, c="gold", edgecolors="black", alpha=.5, linewidth=1, label="Rural")
plt.scatter(num_rides_city_suburban,ave_fare_suburban, s=suburban_rides_city['driver_count']*4, c="lightskyblue", edgecolors="black",alpha=.5, linewidth=1, label="Suburban")
plt.scatter(num_rides_city_urban,ave_fare_urban, s=urban_rides_city['driver_count']*4, c="lightcoral", edgecolors="black",alpha=.5, linewidth=1, label="Urban")

plt.text(42, 38, "Note")
plt.text(42 ,36, "Size of Bubble Corresponds to Number of Drivers per City")
plt.title('Pyber Ride Sharing Data (2018)')
plt.xlabel('Total Number of Rides per City')
plt.ylabel('Average Fare ($)')

legen = plt.legend(title="City Types", fontsize=8, loc='upper right')
legen.legendHandles[0]._sizes = [40]
legen.legendHandles[1]._sizes = [40] 
legen.legendHandles[2]._sizes = [40]

plt.show()
```


![png](output_15_0.png)


# Total Fares by City Type


```python
# Total Fares by City TYPE data to list
data_tfct = merge_df.groupby(['type']).sum()["fare"].tolist()
# data_tfct # Returns [4327.93, 19356.329999999994, 39854.38]
```


```python
# Pie Chart Figure varables
values = data_tfct
title = "% Total Fares by City Type"
labels = ['Rural', 'Urban','Suburban']
colors = ['gold','lightblue','lightcoral']
explodes = (0,0,.14)
autopct = "%1.1f%%"
startangle = 115
shadow = "True"
```


```python
# Show figure
plt.title(title)
plt.pie(values, explode=explodes,startangle=startangle, autopct=autopct, labels=labels,colors=colors,shadow=shadow)
plt.show()
```


![png](output_19_0.png)


# Total Rides by City Type


```python
# Total RIDES by CITY TYPE data to list
data_trct = merge_df.groupby(['type']).count()["ride_id"].tolist()
# data_trct # Returns [125, 625, 1625]
```


```python
# Pie Chart Figure varables
values = data_trct
title = "% Total Rides by Per City Type"
labels = ['Rural', 'Urban','Suburban']
colors = ['gold','lightblue','lightcoral']
explodes = (0,0,.14)
autopct = "%1.1f%%"
startangle = 128
shadow = "True"
```


```python
# Show figure
plt.title(title)
plt.pie(values, explode=explodes,startangle=startangle, autopct=autopct, labels=labels,colors=colors,shadow=shadow)
plt.show()
```


![png](output_23_0.png)


# Total Drivers by City Type


```python
# Total DRIVERS by CITY TYPE data to list
data_tdct = merge_df.groupby(['type']).mean()["driver_count"].tolist()
# data_tdct # Returns [4.296, 13.712, 36.67815384615385]
```


```python
# Pie Chart Figure varables
values = data_tdct
title = "% Total Drivers by City Type"
labels = ['Rural', 'Urban','Suburban']
colors = ['gold','lightblue','lightcoral']
explodes = (0,0,.14) 
autopct = "%1.1f%%"
startangle = 123
shadow = "True"
```


```python
# Show figure
plt.title(title)
plt.pie(values, explode=explodes,startangle=startangle, autopct=autopct, labels=labels,colors=colors,shadow=shadow)
plt.show()
```


![png](output_27_0.png)



```python
# "It's all a point of view.  
#     If the view isn't what you like, 
#     step outside the box you're in, and see the bigger picture. 
#     Repeat until the view makes sense and you're at peace and have joy.  
#     Then you'll know that you are in the right place of mind for this place in time."
#     ~ Verna Oratti June 18, 2018

```
