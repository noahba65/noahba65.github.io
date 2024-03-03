---
layout: page
title: Divvy Bike Share Project
permalink: /divvy_write_up/
---

# Navigating the Divvy Bike Share Challenge with Data Science

Divvy's growth in Chicago, despite its benefits, introduces a significant operational challenge: balancing bike and dock availability across the city. Manual rebalancing efforts, though diligent, struggle to adapt to the dynamic demand, highlighting the necessity for a predictive model that can anticipate station imbalances in advance.

## The Challenge of Dynamic Urban Mobility

The key to enhancing Divvy's operational efficiency lies in predictive modeling. The dynamic nature of bike usage—complicated by the intertwined spatial and temporal patterns of station demand—requires a sophisticated approach to forecast potential imbalances accurately.

## Leveraging Advanced Predictive Modeling with StemGNN

The exploration led to the adoption of the StemGNN model, initially designed for complex networks like traffic systems. By treating each Divvy station as a node within a network, StemGNN offers a nuanced approach to understanding and predicting bike availability across Chicago.

## A Deep Dive into Data

A focused dataset from the Chicago Data Portal for July to September 2022 serves as the foundation for this analysis. Concentrating on Lincoln Square, Uptown, and North Center—areas selected for their distinct biking patterns due to geographic considerations—provides a detailed lens through which to examine and predict station usage trends.

![Target Community Areas](/images/target_community_areas.png)

Identifying active stations within these areas allows for a targeted approach to modeling, enhancing the relevance and application of the StemGNN model to Divvy's operational challenges.

![Target Stations](/images/target_stations.png)

## Results: Demonstrating Predictive Accuracy

The application of the StemGNN model yielded promising results, showcasing the potential for significantly improving bike rebalancing efforts. With RMSEs of 4.9% for 30-minute forecasts and 4.8% for 60-minute forecasts, the model demonstrates a high degree of precision in predicting dock availability.

![Metrics Table Overview](/images/metrics_table.png)

Furthermore, the model's performance, when evaluated using the Mean Absolute Scaled Error (MASE), indicates a substantial improvement over a naïve forecasting approach. With MASE values of 0.59 for 30-minute forecasts and 0.39 for 60-minute forecasts, StemGNN significantly outperforms basic benchmark models, offering a more reliable tool for anticipating station demand.

## Implications for Urban Transportation Management

This study not only addresses the immediate challenges faced by Divvy but also contributes to the broader conversation on urban mobility management. By demonstrating the efficacy of predictive modeling in optimizing bike-sharing operations, it paves the way for more data-driven approaches to urban transportation challenges.

The success of the StemGNN model in forecasting bike availability highlights the transformative potential of advanced analytics in enhancing the efficiency and reliability of bike-share systems. Such innovations are crucial for developing smarter, more responsive urban transit networks, ultimately leading to more sustainable and accessible cities.

