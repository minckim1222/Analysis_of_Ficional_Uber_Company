# Analysis of Fictional Uber Company

An analysis was done on ride data for a fictional ride share company.  The data was split into two .csv files.  The first .csv file gave an overall view of locations with number of drivers, city name, and the type of location: urban, suburban, and rural.  The second .csv file contained more detailed information about the rides: the city name, date, and fair amount were shown.  The data can be found [here.](https://github.com/minckim1222/Analysis_of_Ficional_Uber_Company/tree/master/raw_data)

## Beginning of Analysis

The first step was to combine both the .csv files together in a Pandas dataframe.  The data was cleaned and filtered to come up with the final dataframe, which showed the city, amount of drivers, average fair, total fares, total riders, and the type of location.  A sample of the final data frame is shown here:

![Final Dataframe](https://github.com/minckim1222/Analysis_of_Ficional_Uber_Company/blob/master/final_dataframe.png)

## Scatter plot

A bubble scatter plot was graphed using matplotlib to compare riders per type of area and the average fare cost.  The size of the bubble is scaled by driver count per city.

![Bubble plot](https://github.com/minckim1222/Analysis_of_Ficional_Uber_Company/blob/master/Pyber_Bubble_Plot.png)

## Pie Charts 

Three pie charts were made to showcase different types of data.

#### Drivers by City Type

![Drivers](https://github.com/minckim1222/Analysis_of_Ficional_Uber_Company/blob/master/Drivers_by_City_Type.png)

#### Fares by City Type

![Fares](https://github.com/minckim1222/Analysis_of_Ficional_Uber_Company/blob/master/Fares_by_City_Type.png)

#### Riders by City Type

![Riders](https://github.com/minckim1222/Analysis_of_Ficional_Uber_Company/blob/master/Riders_by_City_Type.png)

## Final Thoughts

1.) The data came out as one would expect. Urban areas have more drivers, more users, and more total profit.

2.) The average fare for rural and suburban were both higher than the average fare for urban. This makes sense. People in urban areas are probably going a shorter distance, where as people in the suburban and rural were probably going a farther distance. The total fares would be lower in this area due to less volume, but the average will be higher because of distance travelled.

3.) Working an urban area might be less profitable than a rural area. Urban areas have more competition, and make less per customer. Would be cool to have data throughout the day, to try and pinpoint when the optimal time to work would be. My friend actually drove for uber, and he drove most of his customers before 8A.M. when the work day started. He also made great money shuttling between hotels and DFW Airport.

