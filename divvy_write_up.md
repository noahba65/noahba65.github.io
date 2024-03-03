---
layout: page
title: Divvy Bike Share Project
permalink: /divvy_write_up/
---

# Navigating the Divvy Bike Share Challenge with Data Science

Divvy, the city-owned bike share program of Chicago, operated in partnership with Lyft, has seen substantial growth since its inception in 2013. However, a significant challenge that has emerged with this expansion is the imbalance in bike station capacities across the city. Some stations frequently experience shortages, while others have an excess of bikes. To manage this issue, Divvy has employed manual rebalancing strategies, involving paid workers who use vans to redistribute bikes from crowded stations to those with fewer bikes. Despite these efforts, the dynamic nature of station statuses, particularly during peak hours, underscores the critical need for advanced predictive modeling to enhance operational efficiency.

## Balancing Bikes and Docks in Chicago's Dynamic Landscape

The program's success reflects the city's commitment to sustainable transportation, yet it also poses a challenge: ensuring bike and dock availability are balanced across an extensive network of stations. The problem arises when Divvy rebalncing workers leave for a station that is empty, but by the time they get there, it is full. Or they leave a general area with stations that will soon be wiped out by morning rush hour Divvy commuters. 

This led me to explore predictive modeling, specifically the application of advanced algorithms that can predict potential imbalances 30 and 60 minutes ahead to give rebalancing workers an edge when it comes to route planning.

What makes this model so complex is that it is dynamic in both space and time. When you are predicting station status over time, each station can be thought as a time series. These could be thought of as independent time series, but it is more complicated by the fact that riders ride from one station to another causing station statuses across stations to be correlated in space. This data would be classified as a joint time series. Joint time series can be tricky and most standard forecasting models such as linear regressions, ARIMA, or Facebooks Prophet model are not directly applicable. All of these could be coereced to fit the problem, but there are more specific models designed for problems like these. 

This led me to the [StemGNN model](https://arxiv.org/abs/2103.07719), developed by Cao et al. (2020). This model was was originally designed for complex network systems like traffic flows in Los Angeles. Each traffic sensor was treated as a node in a network where traffic flowed over time between each sensor. Divvy bike station relationships over time present a very similar setup. 


## The Data Dive and Machine Learning Approach

At the heart of this analysis is an expansive dataset sourced from the [Chicago Data Portal](https://data.cityofchicago.org/), offering a granular view of bike availability at Divvy stations, updated every 10 minutes. Covering the years 2013 to 2022, the dataset initially contained an overwhelming 242 million entries. To manage this vast amount of data more efficiently, I focused on a subset from July to September 2022, coinciding with Divvy's peak ridership months. This period was chosen to ensure the data reflected the most dynamic user interactions with the bike-share system.

The study zeroes in on three specific community areas: Lincoln Square, Uptown, and North Center. These areas were strategically selected due to their unique positioning away from the Red Line—Chicago's main North-South commuter rail. This separation often compels residents to rely on Divvy bikes for East-West travel, thereby increasing and diversifying ridership within these regions.

![Target Community Areas](/images/target_community_areas.png)

Within these neighborhoods, 52 stations were identified (shown below), though only 41 were operational during the selected study period. Each station, or "node" as referred to in our model, plays a critical role in understanding the broader network of urban mobility facilitated by Divvy.

![Target Stations](/images/target_stations.png)

Armed with this refined dataset, I embarked on training the StemGNN model. The objective was not just to predict when and where bikes would be needed but also to map the intricate web of interconnectivity that defines Chicago's urban landscape through the lens of bike-share usage.


## The Model: Simplifying the Science Behind Predicting Bike Needs

The challenge of forecasting bike availability in Chicago's Divvy program led to the adoption of a specialized model known as StemGNN. This model acts much like a meteorological forecast for bike distribution, predicting where and when bikes will be needed across the city.

### Decoding Daily and Weekly Bike Usage Patterns

StemGNN meticulously analyzes patterns in bike usage over time, akin to how weather patterns are studied. It identifies the regular rhythms of urban life, such as peak commuting times or leisurely weekend rides, to predict bike usage trends throughout the day and across the week.

### Mapping the Network of Bike Stations

Beyond temporal analysis, the model delves into the spatial dynamics of the city's bike stations, examining how they influence one another. It's akin to mapping a network of interconnected points, highlighting how a surge in demand at one station might impact its neighbors.

### Constructing a Comprehensive Analysis Framework

The model is structured in layers, with each contributing uniquely to the learning process, similar to a multidisciplinary team where every member brings a distinct skill set. Some layers capture the overarching trends, while others focus on the finer details of the data.

### Tailoring the Model for Divvy's Infrastructure

The StemGNN model was meticulously fine-tuned to align with Divvy's specific needs, akin to customizing a precision tool for a particular task. Adjustments were made to optimize its learning rate and the amount of historical data it examines, ensuring the predictions were as accurate as possible.

This refined tool now offers a detailed forecast of bike availability, facilitating a smoother operation of the bike-share system. The insights provided by the model are instrumental not just for Divvy but also offer a window into the future of urban mobility management.

For an in-depth technical exploration, the full academic paper detailing the work with Divvy and the StemGNN model can be found [here](https://github.com/noahba65/stemGNN_divvy/blob/capstone/Assignments/final-paper/final_paper.pdf).

## Results: A Closer Look at Predictive Accuracy

The performance of the model yielded impressive results, as shown below.
![Metrics Table Overview](/images/metrics_table.png)

The metric used to gauge accuracy was the Root Mean Squared Error (RMSE), expressed as a percentage. This aligns with the data metric for station availability. The model achieved an average accuracy of 4.9% for the 30-minute forecast and 4.8% for the 60-minute forecast. Essentially, this indicates that the model's predictions typically deviate from the actual station usage status by about 5%.

However, RMSE alone doesn't provide a complete picture without a baseline for comparison. That's where the Mean Absolute Scaled Error (MASE) becomes valuable. MASE measures the model's Mean Average Error against that of a basic benchmark model—specifically, a naïve forecasting model that assumes no change over the forecast horizon. For instance, if a station is 70% full at the present moment, the naïve model would predict it to remain 70% full an hour later. This comparative approach effectively positions the StemGNN model against the simplest prediction method available.

The MASE values for our model further confirm its robustness: 0.59 for the 30-minute forecasts and 0.39 for the 60-minute forecasts. This implies that the 30-minute forecast model's error rate is only 60% of the error rate of the naïve model, while the 60-minute forecast model performs even better, with an error rate at 40% of the naïve model's error. In layman's terms, for both forecasting horizons, the StemGNN model significantly outperforms the scenario of using no predictive model at all.

Through this process, I'm not just addressing the current imbalances in bike availability; I'm anticipating future trends, paving the way for a more efficient bike-share experience throughout Chicago. The results of my work offer promising insights into the use of machine learning for urban planning. By refining parameters such as learning rates and window sizes, I've identified models that can predict dock availability with a margin of error within 5%.

By customizing the StemGNN model to Divvy's data, I created a predictive tool capable of forecasting dock availability with significant precision. The implications of this research extend beyond Divvy, suggesting a strategy for cities around the globe to employ data-driven solutions for transportation management.
