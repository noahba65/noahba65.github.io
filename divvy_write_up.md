

# Navigating the Divvy Bike Share Challenge with Data Science

Divvy, the city-owned bike share program of Chicago, operated in partnership with Lyft, has seen substantial growth since its inception in 2013. However, a significant challenge that has emerged with this expansion is the imbalance in bike station capacities across the city. Some stations frequently experience shortages, while others have an excess of bikes. To manage this issue, Divvy has employed manual rebalancing strategies, involving paid workers who use vans to redistribute bikes from crowded stations to those with fewer bikes. Despite these efforts, the dynamic nature of station statuses, particularly during peak hours, underscores the critical need for advanced predictive modeling to enhance operational efficiency.

## Balancing Bikes and Docks in Chicago's Dynamic Landscape

In my analysis of Chicago's Divvy bike share program, I've observed firsthand the complexities associated with its growth. The program's success reflects the city's commitment to sustainable transportation, yet it also poses a challenge: ensuring bike and dock availability are balanced across an extensive network of stations. Traditionally, Divvy has relied on manual redistribution of bikes, a process I found to be inefficient and non-scalable.

This led me to explore predictive modeling, specifically the application of advanced algorithms that can predict potential imbalances. My research centered on the [StemGNN model](https://arxiv.org/abs/2103.07719), developed by Cao et al. (2020), which was originally designed for complex network systems like traffic flows.


## The Data Dive and Machine Learning Approach

The foundation of my study is a comprehensive dataset from the Chicago Data Portal, which provided detailed insights into bike availability trends. With this data, I trained the StemGNN model to understand not just the timing of bike demand but also how it interconnects across different locations in the city.

## The Model: Deciphering Urban Rhythms with StemGNN

In the bustling urban environment of Chicago, Divvy bike stations are akin to network nodes, each with its own pattern of bike availability. My challenge was to predict the activity at these nodes, a task that required a robust approach to time-series data analysis: the StemGNN model.

### Unveiling Patterns with Discrete Fourier Transform

The model employs Discrete Fourier Transform (DFT) to explore the temporal dynamics of the data, allowing me to identify patterns and dependencies that are critical for predicting dock occupancy rates.

### Exploring Spatial Dynamics with Graph Fourier Transform

Conversely, the Graph Fourier Transform (GFT) element of the model allowed me to examine spatial relationships within the network of bike stations, revealing how the activity of one station relates to another.

### Neural Network Layers: The Analytical Journey

At the heart of the StemGNN model is a series of neural network layers, each designed to reveal deeper insights from the data. Starting with the Latent Correlation Layer, which uncovers spatial correlations, I navigated through transformative layers that shifted the data into both spatial and temporal frequency domains. This facilitated a comprehensive analysis of the intricate patterns present in the data.

### Adapting the Model for Divvy's Ecosystem

The versatility of the StemGNN model meant that I could fine-tune it to suit the specificities of the Divvy bike-share data. I adapted the historical dock occupancy data into a structure compatible with the model, leading to forecasts that demonstrated remarkable accuracy and adaptability to urban mobility patterns.

### The Outcome: Precision in Forecasting

By customizing the StemGNN model to Divvy's data, I created a predictive tool capable of forecasting dock availability with significant precision. The integration of the Inverse Discrete Fourier Transform was the final step, translating the model's predictions into practical, actionable insights.

Through this process, I'm not just addressing the current imbalances in bike availability; I'm anticipating future trends, paving the way for a more efficient bike-share experience throughout Chicago.

## Insights and Implications

The results of my work offer promising insights into the use of machine learning for urban planning. By refining parameters such as learning rates and window sizes, I've identified models that can predict dock availability with a margin of error within 5%.

![MASE and RMSE per Node](/images/mase_per_node.png)

The implications of this research extend beyond Divvy, suggesting a strategy for cities around the globe to employ data-driven solutions for transportation management.

## Towards a Data-Driven Future

My study marks a step towards a future where data science is not just a support tool but a driving force in decision-making for urban mobility. For Divvy, the journey towards optimal balance is just beginning, with the potential to reshape the transportation landscape of Chicago and beyond.

![Metrics Table Overview](/images/metrics_table.pdf)

As I continue to explore data-driven solutions, I welcome collaboration and further innovation. Together, we can harness the power of data to transform urban transit—one bike at a time.

