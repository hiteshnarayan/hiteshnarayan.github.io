---
layout: page
title: Boston Housing Price Prediction
description: A comprehensive analysis and prediction of housing prices using multivariable regression.
img: assets/img/boston.jpg
importance: 2
category: Personal
giscus_comments: true
---

## Boston Housing Price Prediction

This project involves predicting housing prices in Boston using a multivariable regression model. The project demonstrates the application of data exploration, model development, evaluation, and optimization techniques to achieve accurate predictions.

### Dataset Exploration and Visualization

- **Exploration:** Analyzed the Boston Housing dataset to understand its structure and key features impacting housing prices.
- **Visualization:** Utilized Seaborn's `pairplot()` to visualize relationships between features such as the number of rooms (RM), distance to employment centers (DIS), socio-economic status (LSTAT), and school quality metrics (PTRATIO) against the target variable (PRICE).

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/boston_pairplot.jpg" title="Pairplot of Features" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Pairplot illustrating relationships between key features and housing prices.
</div>

### Data Preparation and Model Development

- **Data Splitting:** Split the dataset into training and testing sets using `train_test_split()` from sklearn to ensure robust model evaluation.
- **Model Development:** Developed a multivariable regression model leveraging significant features such as RM, DIS, LSTAT, and PTRATIO.

### Model Evaluation and Interpretation

- **Evaluation Metrics:** Assessed model performance using R-squared values for both training and testing datasets.
- **Interpretation:** Analyzed regression coefficients to understand the impact of each feature on housing prices.
- **Residual Analysis:** Investigated residuals to identify patterns and assess model performance.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/boston_residuals.jpg" title="Residual Plot" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Residual plot showing the distribution of errors in predictions.
</div>

### Model Improvement and Optimization

- **Data Transformations:** Applied log transformations to improve model accuracy and meet regression assumptions.
- **Iterative Refinement:** Refined the model based on insights from residual analysis and coefficient interpretation.

### Prediction and Deployment

- **Scenario Analysis:** Specified input values for various features to predict home prices under hypothetical scenarios.
- **Deployment:** Utilized the trained model to make predictions on new data points, demonstrating practical applicability.

### Learning Outcomes

- Enhanced skills in data exploration, visualization, and preprocessing.
- Developed expertise in building and interpreting multivariable regression models.
- Gained experience in model evaluation, optimization, and deployment.

## Conclusion

This project showcases a comprehensive approach to predicting housing prices using multivariable regression. By employing advanced data analysis techniques, we achieved significant insights into factors affecting housing prices in Boston.
