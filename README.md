

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

merge_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>date</th>
      <th>fare</th>
      <th>ride_id</th>
      <th>driver_count</th>
      <th>type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Lake Jonathanshire</td>
      <td>2018-01-14 10:14:22</td>
      <td>13.83</td>
      <td>5739410935873</td>
      <td>5</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Lake Jonathanshire</td>
      <td>2018-04-07 20:51:11</td>
      <td>31.25</td>
      <td>4441251834598</td>
      <td>5</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Lake Jonathanshire</td>
      <td>2018-03-09 23:45:55</td>
      <td>19.89</td>
      <td>2389495660448</td>
      <td>5</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Lake Jonathanshire</td>
      <td>2018-04-07 18:09:21</td>
      <td>24.28</td>
      <td>7796805191168</td>
      <td>5</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Lake Jonathanshire</td>
      <td>2018-01-02 14:14:50</td>
      <td>13.89</td>
      <td>424254840012</td>
      <td>5</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Lake Jonathanshire</td>
      <td>2018-04-06 11:30:32</td>
      <td>16.84</td>
      <td>6164453571846</td>
      <td>5</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Lake Jonathanshire</td>
      <td>2018-03-21 00:18:34</td>
      <td>37.95</td>
      <td>8353656732934</td>
      <td>5</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Lake Jonathanshire</td>
      <td>2018-01-28 00:07:00</td>
      <td>5.67</td>
      <td>9756573174778</td>
      <td>5</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Lake Jonathanshire</td>
      <td>2018-01-24 12:24:22</td>
      <td>34.65</td>
      <td>3319117904437</td>
      <td>5</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Lake Jonathanshire</td>
      <td>2018-03-24 16:27:49</td>
      <td>14.94</td>
      <td>1670908453476</td>
      <td>5</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Lake Jonathanshire</td>
      <td>2018-04-11 22:10:30</td>
      <td>12.81</td>
      <td>5999870428814</td>
      <td>5</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Lake Jonathanshire</td>
      <td>2018-01-23 21:43:16</td>
      <td>21.11</td>
      <td>7711472105447</td>
      <td>5</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Lake Jonathanshire</td>
      <td>2018-01-29 00:19:07</td>
      <td>41.05</td>
      <td>6649692036139</td>
      <td>5</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Lake Jonathanshire</td>
      <td>2018-03-22 14:33:32</td>
      <td>18.72</td>
      <td>4675968803527</td>
      <td>5</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Lake Jonathanshire</td>
      <td>2018-04-16 20:26:30</td>
      <td>32.47</td>
      <td>1013873953228</td>
      <td>5</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Lake Jonathanshire</td>
      <td>2018-04-11 19:49:34</td>
      <td>25.92</td>
      <td>8533808747676</td>
      <td>5</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Lake Jonathanshire</td>
      <td>2018-04-09 21:41:30</td>
      <td>15.96</td>
      <td>577276092645</td>
      <td>5</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Lake Jonathanshire</td>
      <td>2018-01-16 09:27:03</td>
      <td>26.27</td>
      <td>3267656258507</td>
      <td>5</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Lake Jonathanshire</td>
      <td>2018-01-21 12:12:56</td>
      <td>37.25</td>
      <td>2966536034637</td>
      <td>5</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Lake Jonathanshire</td>
      <td>2018-04-11 21:32:27</td>
      <td>22.48</td>
      <td>3505458786874</td>
      <td>5</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Lake Jonathanshire</td>
      <td>2018-02-16 01:49:45</td>
      <td>17.58</td>
      <td>3641777572467</td>
      <td>5</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Lake Jonathanshire</td>
      <td>2018-01-17 13:15:58</td>
      <td>28.42</td>
      <td>6544222037368</td>
      <td>5</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Lake Jonathanshire</td>
      <td>2018-01-21 09:48:28</td>
      <td>22.36</td>
      <td>2522096563712</td>
      <td>5</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Lake Jonathanshire</td>
      <td>2018-02-23 06:10:30</td>
      <td>26.63</td>
      <td>5372487991955</td>
      <td>5</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>24</th>
      <td>South Michelleport</td>
      <td>2018-03-04 18:24:09</td>
      <td>30.24</td>
      <td>2343912425577</td>
      <td>72</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>25</th>
      <td>South Michelleport</td>
      <td>2018-03-02 09:54:50</td>
      <td>33.12</td>
      <td>813844006721</td>
      <td>72</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>26</th>
      <td>South Michelleport</td>
      <td>2018-01-08 09:38:14</td>
      <td>23.77</td>
      <td>4916160406018</td>
      <td>72</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>27</th>
      <td>South Michelleport</td>
      <td>2018-04-22 03:15:33</td>
      <td>43.62</td>
      <td>4663606096929</td>
      <td>72</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>28</th>
      <td>South Michelleport</td>
      <td>2018-03-03 16:13:34</td>
      <td>41.62</td>
      <td>2339775503972</td>
      <td>72</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>29</th>
      <td>South Michelleport</td>
      <td>2018-01-27 19:38:12</td>
      <td>15.45</td>
      <td>7465262064048</td>
      <td>72</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2345</th>
      <td>Newtonview</td>
      <td>2018-04-01 13:39:13</td>
      <td>26.73</td>
      <td>3723530332713</td>
      <td>1</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2346</th>
      <td>Newtonview</td>
      <td>2018-04-25 10:20:13</td>
      <td>55.84</td>
      <td>9990581345298</td>
      <td>1</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2347</th>
      <td>North Jaime</td>
      <td>2018-03-06 09:09:23</td>
      <td>44.17</td>
      <td>1152195873170</td>
      <td>1</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2348</th>
      <td>North Jaime</td>
      <td>2018-03-12 13:05:56</td>
      <td>23.21</td>
      <td>5987447089759</td>
      <td>1</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2349</th>
      <td>North Jaime</td>
      <td>2018-04-04 13:13:40</td>
      <td>51.83</td>
      <td>9116047435376</td>
      <td>1</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2350</th>
      <td>North Jaime</td>
      <td>2018-02-01 08:59:24</td>
      <td>17.05</td>
      <td>9481117811603</td>
      <td>1</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2351</th>
      <td>North Jaime</td>
      <td>2018-05-06 00:58:17</td>
      <td>41.18</td>
      <td>7328094869758</td>
      <td>1</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2352</th>
      <td>North Jaime</td>
      <td>2018-04-04 01:58:37</td>
      <td>43.86</td>
      <td>8195436622338</td>
      <td>1</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2353</th>
      <td>North Jaime</td>
      <td>2018-04-27 17:58:27</td>
      <td>14.01</td>
      <td>2156688209209</td>
      <td>1</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2354</th>
      <td>North Jaime</td>
      <td>2018-02-10 21:03:50</td>
      <td>11.11</td>
      <td>2781339863778</td>
      <td>1</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2355</th>
      <td>Penaborough</td>
      <td>2018-02-24 00:44:00</td>
      <td>21.89</td>
      <td>2069309881916</td>
      <td>6</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2356</th>
      <td>Penaborough</td>
      <td>2018-04-27 06:02:10</td>
      <td>38.33</td>
      <td>547013925055</td>
      <td>6</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2357</th>
      <td>Penaborough</td>
      <td>2018-01-14 15:58:48</td>
      <td>54.10</td>
      <td>432925983890</td>
      <td>6</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2358</th>
      <td>Penaborough</td>
      <td>2018-02-03 17:15:31</td>
      <td>51.80</td>
      <td>5383427508621</td>
      <td>6</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2359</th>
      <td>Penaborough</td>
      <td>2018-01-22 15:36:24</td>
      <td>10.11</td>
      <td>4129933467653</td>
      <td>6</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2360</th>
      <td>Harringtonfort</td>
      <td>2018-01-06 07:38:40</td>
      <td>47.33</td>
      <td>3849747342021</td>
      <td>4</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2361</th>
      <td>Harringtonfort</td>
      <td>2018-02-17 04:42:56</td>
      <td>30.58</td>
      <td>6835140871685</td>
      <td>4</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2362</th>
      <td>Harringtonfort</td>
      <td>2018-04-16 16:30:50</td>
      <td>17.39</td>
      <td>4023962353348</td>
      <td>4</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2363</th>
      <td>Harringtonfort</td>
      <td>2018-03-10 10:11:37</td>
      <td>19.02</td>
      <td>6717313402790</td>
      <td>4</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2364</th>
      <td>Harringtonfort</td>
      <td>2018-02-26 07:03:11</td>
      <td>54.66</td>
      <td>9201585331171</td>
      <td>4</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2365</th>
      <td>Harringtonfort</td>
      <td>2018-01-09 15:30:35</td>
      <td>31.84</td>
      <td>3730685356921</td>
      <td>4</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2366</th>
      <td>West Heather</td>
      <td>2018-03-12 04:22:26</td>
      <td>26.55</td>
      <td>7035849392668</td>
      <td>4</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2367</th>
      <td>West Heather</td>
      <td>2018-02-22 09:01:37</td>
      <td>17.40</td>
      <td>8702491506161</td>
      <td>4</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2368</th>
      <td>West Heather</td>
      <td>2018-02-22 01:46:43</td>
      <td>33.38</td>
      <td>5551691454078</td>
      <td>4</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2369</th>
      <td>West Heather</td>
      <td>2018-02-04 16:29:23</td>
      <td>13.97</td>
      <td>7118893881453</td>
      <td>4</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2370</th>
      <td>West Heather</td>
      <td>2018-04-18 19:33:12</td>
      <td>46.60</td>
      <td>3671003215967</td>
      <td>4</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2371</th>
      <td>West Heather</td>
      <td>2018-03-02 21:04:10</td>
      <td>20.99</td>
      <td>5766454453070</td>
      <td>4</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2372</th>
      <td>West Heather</td>
      <td>2018-03-06 20:06:51</td>
      <td>48.11</td>
      <td>2570548892682</td>
      <td>4</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2373</th>
      <td>West Heather</td>
      <td>2018-02-02 06:28:04</td>
      <td>53.07</td>
      <td>2462950442268</td>
      <td>4</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2374</th>
      <td>West Heather</td>
      <td>2018-05-07 19:22:15</td>
      <td>44.94</td>
      <td>4256853490277</td>
      <td>4</td>
      <td>Rural</td>
    </tr>
  </tbody>
</table>
<p>2375 rows × 6 columns</p>
</div>



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
