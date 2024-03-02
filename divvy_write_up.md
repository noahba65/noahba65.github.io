---
layout: page
title: Divvy Write Up
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

The foundation of my study is a comprehensive dataset from the [Chicago Data Portal](https://data.cityofchicago.org/), which provided detailed insights into bike availability across Divvy stations every 10 minutes. This data spans from 2013-2022 and contains 242 million rows. To make this a more approachable problem, I scaled down the data and to contain data from July 2022 through September of 2022 and to contain only 3 community areas, the idea being that training it on city wide data that spans the full 9 year period would require far too many computational power for an efficient real time tool. July through September were the selected months since that is the peak ridership of Divvy providing the most dynamic data. 

The chosen community areas, which can be seen below, are Lincoln Square, Uptown, and North Center. These areas were selected strategically since they are not directly connected by the Red Line, Chicago's busiest commuter rail line running North-South, resulting in increased and dynamic ridership as residents rely on Divvy to travel East to West.
![Target Community Areas](/images/target_community_areas.png)

In total there have been 


With this data, I trained the StemGNN model to understand not just the timing of bike demand but also how it interconnects across different locations in the city.

## The Model: Deciphering Urban Rhythms with StemGNN

### Model Structure
The StemGNN model innovatively combines Discrete Fourier Transform (DFT) and Graph Fourier Transform (GFT) to effectively analyze time-series data. The DFT component of StemGNN plays a pivotal role in modeling temporal dependencies, enabling the model to detect and interpret patterns like seasonality and autocorrelation, which are common in time-series data. This temporal analysis is crucial for understanding the underlying trends and cyclic behaviors in the dataset. In contrast, the GFT component focuses on interseries correlations, analyzing the spatial interactions between nodes. By employing GFT, the model is adept at uncovering the spatial relationships that exist in the data, providing insights into how different data points (or nodes) interact and influence each other in a given space.

The model operates on data formatted in a T * N. At its core, StemGNN is composed of multiple neural network layers, each contributing to the deep learning capabilities of the model. The journey through the model begins with the Latent Correlation Layer, designed to initially explore and learn the spatial correlations present within the data. This layer sets the stage for more intricate spatial analyses which are further enhanced by subsequent layers. 

Following this, the Graph Fourier Transform is applied, transforming the data into the frequency domain with a specific focus on spatial relationships. This transformation is a crucial step in distilling the spatial characteristics of the data, enabling the model to handle complex spatial structures effectively. The model then shifts its focus to temporal aspects, employing the Discrete Fourier Transform (DFT). By applying DFT, StemGNN is able to transform the time-series data into the frequency domain, a step that is fundamental in unveiling and understanding temporal dynamics and patterns that unfold over time.

The model further refines its analysis with a 1D Convolutional layer, which is adept at extracting key temporal features from the data. This layer methodically scans the transformed data, pinpointing significant temporal features and patterns that are essential for accurate forecasting. The Spectral Graph Convolution layer then takes over, applying Graph Fourier Transform (GFT) to capture the intricate spatial correlations between different nodes. This layer is integral to understanding how different series or nodes within the graph are interconnected and influence each other, revealing the complex web of spatial dependencies in the dataset.

An additional layer, the Gated Linear Unit (GLU), is incorporated into the model, serving as a sophisticated filter. The GLU layer critically evaluates and determines the relevance of the information processed by previous layers, ensuring that only pertinent features are carried forward for predictions. This layer adds an element of decision-making to the model's processing, enhancing its ability to focus on the most relevant aspects of the data.

The final step in the model's processing pipeline is the application of the Inverse Discrete Fourier Transform (IDFT). This transformation is pivotal as it converts the frequency-domain data back into the time domain, making the model's outputs interpretable and directly applicable to the original temporal structure of the data. This step is essential for rendering the model's predictions and analyses in a format that is meaningful and actionable in real-world contexts.


### Adapting the Model for Divvy's Ecosystem

The versatility of the StemGNN model meant that I could fine-tune it to suit the specificities of the Divvy bike-share data. I adapted the historical dock occupancy data into a structure compatible with the model, leading to forecasts that demonstrated remarkable accuracy and adaptability to urban mobility patterns.

In this research, the focus was on fine-tuning two primary parameters of the StemGNN model: the learning rate and window size, while maintaining the default settings for other parameters. The learning rate influences the model's learning speed, and the window size specifies the quantity of past data points used for forecasting. Experiments were conducted with forecast horizons of 3 and 6 (equivalent to 30 and 60 minutes into the future), learning rates of 0.01, 0.001, and 0.0001, and window sizes of 6, 12, 18, were considered. The results shown in this write up only focus on the most successful learning rate of .001 and window size of 6. For more specifics on model tuning you can find a downloadable pdf of my academic paper regarding Divvy for Stem GNN [here](https://github.com/noahba65/stemGNN_divvy/blob/capstone/Assignments/final-paper/final_paper.pdf) 

### The Outcome: Precision in Forecasting

By customizing the StemGNN model to Divvy's data, I created a predictive tool capable of forecasting dock availability with significant precision. The integration of the Inverse Discrete Fourier Transform was the final step, translating the model's predictions into practical, actionable insights.

Through this process, I'm not just addres
sing the current imbalances in bike availability; I'm anticipating future trends, paving the way for a more efficient bike-share experience throughout Chicago.

## Insights and Implications

The results of my work offer promising insights into the use of machine learning for urban planning. By refining parameters such as learning rates and window sizes, I've identified models that can predict dock availability with a margin of error within 5%.

![MASE and RMSE per Node](/images/mase_per_node.png)

The implications of this research extend beyond Divvy, suggesting a strategy for cities around the globe to employ data-driven solutions for transportation management.

## Towards a Data-Driven Future

My study marks a step towards a future where data science is not just a support tool but a driving force in decision-making for urban mobility. For Divvy, the journey towards optimal balance is just beginning, with the potential to reshape the transportation landscape of Chicago and beyond.

![Metrics Table Overview](/images/metrics_table.png)

As I continue to explore data-driven solutions, I welcome collaboration and further innovation. Together, we can harness the power of data to transform urban transit—one bike at a time.

