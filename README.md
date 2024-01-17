# F1-Analysis
This repository is to analyze the F1 race with the F1 sprint results. 
F1 Sprint is a shorter race (1/3 of the entire race distance) held on the Saturday before the main Sunday Grand Prix. It was introduced in 2021 with 2 main goals.
1. To create more excitement for viewers during the Grand Prix weekend.
2. To encourage more opportunities for drivers to fight and gain points, especially for those from mid-tier teams. 

The main objective of this analysis is to see to what extent the sprint achieved the second goal. 
For the purpose of the analysis, the main dataset is sourced from Kaggle: https://www.kaggle.com/datasets/rohanrao/formula-1-world-championship-1950-2020?resource=download
The dataset contains information on F1 races, drivers, contractors, qualifying, circuits, lap times, pit stops, and championships held from 1950 - 2023. For this analysis, we are using the following datasets: sprint_results.csv, gp_results.csv, status.csv, drivers.csv.

sprint_results.csv:
resultId | raceId | driverId | constructorId | number | grid | position	| positionText | positionOrder | points | laps | time | milliseconds | fastestLap | fastestLapTime | statusId

gp_results.csv:
resultId | raceId | driverId | constructorId | number | grid | position	| positionText | positionOrder | points | laps | time | milliseconds | fastestLap | fastestLapTime | statusId

status.csv:
statusId | status

drivers.csv:
driverId | driverRef | number | code | forename | surname | dob | nationality | url

## Here is a breakdown of the steps taken for the analysis:
1. Keeping races that are common between both sprint and grand prix races, so filter the grand prix races to match the race IDs of the sprint races.
2. Changing the fastest lap time calculation from minutes and seconds to seconds only
3. Keeping races where the race is completed, so filter for the status to be completed, +1 Laps, +2 Laps. We ignored the rest since it was not applicable to the filtered dataset.
4. Do an inner join to combine the grand prix race data and sprint race data on raceid and driverid
5. Renaming columns in the combined dataset to be more user-friendly.
6. Changing the data type of 'position' column from string to integer.

Here is a snapshot of the data:
![image](https://github.com/akshaygupta96/F1-Analysis/assets/156336449/f4d13cd1-2e99-47dc-8da7-1414834ab1f1)

7. Next, to create the data to be in the format for plotting the graph, groupby driverid and take the mean of the columns
8. Merge the dataframe with the drivers dataset to get the code name of the drivers when plotting
9. Since the mean is being used as the metric for comparison, outliers are removed based on the number of races the driver has driven. Filter out drivers who only have had one sprint race

Here is a snapshot of the plotting_data:
![image](https://github.com/akshaygupta96/F1-Analysis/assets/156336449/7a434865-7327-486e-9412-aaf58bf2e2d8)

## Graphs Plotted:
1. For the first part of the analysis, we look at the fastest lap time. In the main race, drivers can gain an extra point if they make the fastest lap for that grand prix. We want to compare to see if the fastest laps differ significantly between the sprint and race for the drivers.
![image](https://github.com/akshaygupta96/F1-Analysis/assets/156336449/7a40c259-3070-4b52-bc64-bed089d36232)
For most drivers, the race fastest lap timing is better than the sprint fastest lap timing. This makes sense since they have a longer racing distance and can use different tires to the maximum capabilities. Drivers would not want to push the tires to the maximum extent during the sprint, as there are no points involved. However, we see that these 4 mid-tier drivers: VET, GIO, LAT, and PIA have better Mean Fastest Lap Time during the sprint as compared to the race. In fact, VET has one of the lowest Mean Fastest Lap Time for the sprint races. This means that some mid-tier drivers can perform better in terms of Mean Fastest Lap Time and if a point was awarded during the sprint for this, they may be able to fight and gain points in this aspect.

2. In the second part of the analysis, we look at the average position for both the sprint and race. We want to compare and see the finishing position of the drivers between the two racing types - if there are any noticeable differences, especially amongst the mid-tier drivers.
![image](https://github.com/akshaygupta96/F1-Analysis/assets/156336449/d05e8003-b8df-4bae-8df9-719121f4419a)
For most drivers, there does not seem to be a clear trend in terms of the average positions. However, for the mid-tier drivers, most seem to be doing better in the actual race than in the sprint. HUL, RIC, MAG, GIO, and PIA do better in the sprint race. The biggest difference is seen in PIA, who did win a sprint race and came on the podium as well. Hence, it seems that it really depends on whether the mid-tier teams' driver is able to perform on that day itself, and not really on the sprint format.






