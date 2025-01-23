---
layout: page
title: Statistical Analysis of Childbed Fever
description: >
  Investigating the Impact of Handwashing on Childbed Fever Mortality Rates
  Technologies: Data Analysis, Statistical Testing, Time Series Analysis, Data Visualization
img: assets/img/Childbed_fever.jpg
importance: 5
category: Personal
giscus_comments: False
---

## Overview

This project investigates the impact of handwashing on reducing death rates due to childbed fever based on historical data from Dr. Ignaz Semmelweis. The analysis provides insights into how hand hygiene practices significantly improved health outcomes in maternity wards.
- **Historical Context:** Dr. Ignaz Semmelweis hypothesized that handwashing could prevent infections in maternity wards. This project analyzes his original data to validate his hypothesis.
- **Objective:** To demonstrate the effectiveness of handwashing in reducing mortality rates from childbed fever.

### Dataset

- **Source:** Historical data collected by Dr. Semmelweis.
- **Key Columns:**
  - `date`: The date of the record.
  - `births`: The number of births in the clinic.
  - `deaths`: The number of deaths in the clinic.
  - `clinic`: The name of the clinic.

### Methodology

1. **Data Cleaning:** Addressed missing values and converted data types for accurate analysis.
2. **Data Visualization:** Utilized histograms, KDE plots, and line charts to visualize data distributions and trends.
3. **Statistical Analysis:** Performed t-tests to compare death rates before and after implementing handwashing.
4. **Time Series Analysis:** Analyzed different periods in the data using rolling averages to highlight trends.


<br>


#### Histograms and KDE Plots

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/Kde.jpg" title="KDE plots" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Kernel Density Estimate (KDE) plots showing the distribution of death rates.
</div>

- **Histograms:** Visualized death rate distributions before and after handwashing.
- **KDE Plots:** Used kernel density estimates to smooth distributions and highlight differences.



<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/handwashing_analysis.jpg" title="Handwashing Impact Analysis" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Visualization showing the reduction in death rates after introducing handwashing.
</div>

- **Rolling Averages:** Calculated 6-month rolling averages of death rates before mandatory handwashing.
- **Trend Analysis:** Highlighted changes in death rates over time with handwashing implementation.

<br>

---

### Results

The analysis shows a significant reduction in death rates after introducing handwashing:

- Average death rate before handwashing: 9.92%
- Average death rate after handwashing: 3.88%
- t-test p-value: 0.0000002985, indicating a highly significant difference.

### Conclusion

The analysis provides strong evidence supporting Dr. Semmelweis's hypothesis that handwashing significantly reduces death rates due to childbed fever. This finding underscores the importance of hygiene practices in medical settings.
