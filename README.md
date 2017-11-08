# Matplotlib_Pyber
Homework for Matplotlib



```python
#import dependencies
import matplotlib.pyplot as plt
import pandas as pd
import os
import numpy as np
import seaborn as sns
plt.style.use("seaborn")
```


```python
#make data frames for the data
ride_data = os.path.join("raw_data/ride_data.csv")
city_data = os.path.join("raw_data/city_data.csv")
ride_df = pd.read_csv(ride_data)
city_df = pd.read_csv(city_data)
city_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>driver_count</th>
      <th>type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Kelseyland</td>
      <td>63</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Nguyenbury</td>
      <td>8</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>2</th>
      <td>East Douglas</td>
      <td>12</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>3</th>
      <td>West Dawnfurt</td>
      <td>34</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Rodriguezburgh</td>
      <td>52</td>
      <td>Urban</td>
    </tr>
  </tbody>
</table>
</div>




```python
#combine the data
combined_df = pd.merge(ride_df,city_df, on = "city", how = "right")
combined_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
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
      <td>Sarabury</td>
      <td>2016-01-16 13:49:27</td>
      <td>38.35</td>
      <td>5403689035038</td>
      <td>46</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Sarabury</td>
      <td>2016-07-23 07:42:44</td>
      <td>21.76</td>
      <td>7546681945283</td>
      <td>46</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Sarabury</td>
      <td>2016-04-02 04:32:25</td>
      <td>38.03</td>
      <td>4932495851866</td>
      <td>46</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Sarabury</td>
      <td>2016-06-23 05:03:41</td>
      <td>26.82</td>
      <td>6711035373406</td>
      <td>46</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Sarabury</td>
      <td>2016-09-30 12:48:34</td>
      <td>30.30</td>
      <td>6388737278232</td>
      <td>46</td>
      <td>Urban</td>
    </tr>
  </tbody>
</table>
</div>




```python

```


```python
#group by city
grouped_df = combined_df.groupby(["city","driver_count"])
grouped_df
```




    <pandas.core.groupby.DataFrameGroupBy object at 0x10df196a0>




```python
total_fares = grouped_df["fare"].sum()
total_fares.head()
```




    city          driver_count
    Alvarezhaven  21              741.79
    Alyssaberg    67              535.85
    Anitamouth    16              335.84
    Antoniomouth  21              519.75
    Aprilchester  49              417.65
    Name: fare, dtype: float64




```python
#find total rides per city
total_rides = grouped_df["ride_id"].nunique()
total_rides.head()
```




    city          driver_count
    Alvarezhaven  21              31
    Alyssaberg    67              26
    Anitamouth    16               9
    Antoniomouth  21              22
    Aprilchester  49              19
    Name: ride_id, dtype: int64




```python
#find average price per ride
total_drivers = grouped_df["driver_count"].mean()
average_fare = total_fares / total_rides
average_fare.head()
```




    city          driver_count
    Alvarezhaven  21              23.928710
    Alyssaberg    67              20.609615
    Anitamouth    16              37.315556
    Antoniomouth  21              23.625000
    Aprilchester  49              21.981579
    dtype: float64




```python
type_of_city = grouped_df["type"].unique()
type_of_city = type_of_city.str[0]
type_of_city.head()
```




    city          driver_count
    Alvarezhaven  21                 Urban
    Alyssaberg    67                 Urban
    Anitamouth    16              Suburban
    Antoniomouth  21                 Urban
    Aprilchester  49                 Urban
    Name: type, dtype: object




```python
#merge all the dataframe
new_data = {"Total Riders" : total_rides,
           "Total Fares" : total_fares, "Average Fare" : average_fare,
            "City Type" : type_of_city}
new_df = pd.DataFrame(new_data)
new_df = new_df.reset_index()
new_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>driver_count</th>
      <th>Average Fare</th>
      <th>City Type</th>
      <th>Total Fares</th>
      <th>Total Riders</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Alvarezhaven</td>
      <td>21</td>
      <td>23.928710</td>
      <td>Urban</td>
      <td>741.79</td>
      <td>31</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Alyssaberg</td>
      <td>67</td>
      <td>20.609615</td>
      <td>Urban</td>
      <td>535.85</td>
      <td>26</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Anitamouth</td>
      <td>16</td>
      <td>37.315556</td>
      <td>Suburban</td>
      <td>335.84</td>
      <td>9</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Antoniomouth</td>
      <td>21</td>
      <td>23.625000</td>
      <td>Urban</td>
      <td>519.75</td>
      <td>22</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aprilchester</td>
      <td>49</td>
      <td>21.981579</td>
      <td>Urban</td>
      <td>417.65</td>
      <td>19</td>
    </tr>
  </tbody>
</table>
</div>




```python
ctypes = ["Urban","Suburban","Rural"]
fg = sns.FacetGrid(data=new_df, hue='City Type', hue_order=ctypes, aspect=1.61)
fg.map(plt.scatter, "Total Riders", "Average Fare", "driver_count",alpha = .45, linewidth = 2).add_legend()
```




    <seaborn.axisgrid.FacetGrid at 0x107ec17f0>




```python
plt.title("Uber Data in Different City Types")
plt.xlabel("Riders per City")
plt.ylabel("Average Fare ($) per City")
plt.xlim(0,40)
plt.ylim(15,55)
```




    (15, 55)




```python
plt.show()
```


![png](output_12_0.png)



```python
#% total fares by city type
pie_group = new_df.groupby("City Type")
pie_group_fares = pie_group["Total Fares"].sum()
pie_group_fares
```




    City Type
    Rural        4255.09
    Suburban    20335.69
    Urban       40078.34
    Name: Total Fares, dtype: float64




```python
cities = ["Urban", "Suburban","Rural"]
city_fares = [40078.34,20335.69,4255.09]
explode = [.1,0,0]
colors = ["red", "lightcoral", "lightskyblue"]
plt.title("Total Fares by City Type")
plt.pie(city_fares, explode = explode, labels = cities, colors=colors,
        autopct="%1.1f%%", shadow=True, startangle=90)
plt.axis("equal")
```




    (-1.2108148572569786,
     1.119508187827537,
     -1.1505575694756089,
     1.1024075033082694)




```python
plt.show()
```


![png](output_15_0.png)



```python
#% of total rides per city
pie_group["Total Riders"].sum()
```




    City Type
    Rural        125
    Suburban     657
    Urban       1625
    Name: Total Riders, dtype: int64




```python
city_riders = [1625, 657, 125]
plt.title("Total Riders by City Type")
plt.pie(city_riders, explode = explode, labels = city_riders, colors=colors,
        autopct="%1.1f%%", shadow=True, startangle=90)
plt.axis("equal")
```




    (-1.1932705425802141,
     1.1098032420872641,
     -1.1614913715500408,
     1.1029281738927599)




```python
plt.show()
```


![png](output_18_0.png)



```python
#% total drivers by city
pie_group["driver_count"].sum()
```




    City Type
    Rural        104
    Suburban     638
    Urban       2607
    Name: driver_count, dtype: int64




```python
driver_count = [2607,638,104]
plt.title("Total Drivers by City Type")
plt.pie(driver_count, explode = explode, labels = cities, colors=colors,
        autopct="%1.1f%%", shadow=True, startangle=90)
plt.axis("equal")
```




    (-1.1701245406694292,
     1.0866561826119843,
     -1.1858793591165591,
     1.1040894932912575)




```python
plt.show()
```


![png](output_21_0.png)



```python

```
