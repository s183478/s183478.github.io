---
layout: continous
title: "Home"
---

<script type="text/javascript" id="MathJax-script" async
  src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js">
</script>

## Introduction

In this article, we will investigate the traffic accidents that have happened in New York City in the period between 2013 and 2022. We will be using a dataset from NYC Open Data to get information about vehicle collisions in New York, where we can see which types of vehicles were involved and where they happened. By using visualization techniques, we will illustrate where the zones with the highest chance of vehicle collisions are located, so that drivers can be mindful of these areas.

## Initial Analysis
In order to analyse the collisions in New York we will use the *Motor Vehicle Collisions* dataset, which contains 1.99 million entries and is updated daily by the New York Police Department. It contains information about the date and time of the crash, the borough it happened in, which vehicles were involved and the reason for the crash. However, the dataset contains many errors of either missing information, wrongly written entries or indistinct types, so filtering the dataset for these errors was necessary in order to continue. 

After the filtering was done, we compared the individual vehicle types as seen in the plot below. It is however immediately apparent that a few vehicle types have a huge overrepresentation compared to the rest of the types. This involves Sedan-type cars, SUVs and the vaguely defined "Passenger Vehicles", which all have above 100.000 entries. The fourth most common types is then Taxis, followed by Pick-up Trucks and Vans, but at this point the amount of incidents per vehicle types falls significantly. The least common type, School Buses, only have a few hundred entries. Due to the low amount of data for the less common vehicle types, we will instead focus only on the most common types, specifically those with 5000 entries or more

<img src="/images/BarChart.png"  width="1000" height="400">

## Analysis of location
After cleaning the dataset we did an analysis of which areas in New York are most afflicted by vehicle collisions. We did this using histogram plotting of both the latitude and longitude given in each entry. Since the different vehicle types have different amounts of data, we are mostly interested in the peaks of each vehicle type as those will indicate if the accidents happen in the same place.

<img src="/images/plot_hist.png"  width="1000" height="200">

As can be seen in the plot the Sedan and SUV collisions are spread out across New York, although an interesting thing to note is that the Taxi is centered around a certain location. This means that we can use this to track where the same peak is for the two other vehicle types.

With this information, we then decided to create heatmaps using `folium`, a python package for mapping data to geodata. Using the Taxi heatmap, we can find out where the largest concentration of accidents happen for Taxis, and infer that knowledge onto the other vehicle types considering the single peak of the Taxi histogram.

[Link to Sedan Heatmap](/heatmaps/map_sedan.html)

[Link to SUV Heatmap](/heatmaps/map_suv.html)

[Link to Taxi Heatmap](/heatmaps/map_taxi.html)

We can see in the Taxi heatmap that it is centered around Manhatten island, which means that the other types also are centered in this location. This is indeed the case for both Sedans and SUVs, which also have a cluster of incidents in Brooklyn. This would indicate that Southern Manhatten and Northeastern Brooklyn are the locations where most motor vehicle collisions happen.


## Interactive plotting
We will also illustrate the trends of the vehicle collisions over years, in order to see if there are interesting patterns. We do know that the Covid-19 has affected the amount of collisions, but we might be able to see patterns in the previous years, and maybe even during the pandemic. These illustrations will be made with Bokeh and its interactive plotting Rangetool, so that we can see how the amount of collisions per week changes over the years. Since the data curve will be very noisy, we will plot an additional line where we have applied a Savitzky–Golay filter in order to smooth the curve.

{% include bokeh_sedan.html %}
Here we can see that the collisions that involve Sedan-type vehicles have declined over the years, even before the covid period. During this period there was a sharp decline in accidents, likely as a consequence of the lockdowns that occured. One thing to note is that there is very little data in the period from 2012 to early 2016. It is unknown why this is the case, as the other two types do not have the same problem.

{% include bokeh_suv.html %}
With the SUVs we can see that there was a positive trend towards the pandemic. During the pandemic however, it flucated between positive and negative trends, but is overall on a decline now.

{% include bokeh_taxi.html %}

soemthing that concludes this

## Conclusion
overall conclusion