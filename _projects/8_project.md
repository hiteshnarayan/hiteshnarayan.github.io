---
layout: page
title: Human Activity Classification
description: Advanced ML pipeline for sensor-based activity recognition
img: assets/img/activity_classification.png
importance: 2
category: Academic
giscus_comments: false
---

# Human Activity Classification using Body Sensor Data

This project implements an advanced machine learning pipeline for human activity classification using multi-dimensional time-series data from body-worn sensors. The system processes and analyzes data from the AReM (Activity Recognition system based on Multisensor data fusion) dataset to classify seven distinct human activities.

## Project Highlights
- **94% Classification Accuracy** across seven distinct human activities
- **12% Accuracy Improvement** through advanced preprocessing and optimization
- **Comprehensive ML Pipeline** implementation for time-series data
- **Robust Feature Engineering** with multiple selection techniques

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/data_pipeline.png" title="Data Engineering Pipeline" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Data Engineering Pipeline: From raw sensor data to final evaluation
</div>

## Technical Architecture

### Advanced Feature Engineering
1. **Time Series Processing**
   - Dynamic segmentation up to 20 segments per series
   - Temporal pattern extraction
   - Local characteristic analysis

2. **Statistical Feature Extraction**
```python
features = {
'statistical': ['min', 'max', 'mean', 'median'],
'distribution': ['std', 'q1', 'q3'],
'temporal': ['sliding_windows', 'segment_analysis']
}
```

3. **Dimensionality Reduction**
- Principal Component Analysis (PCA)
- Recursive Feature Elimination (RFE)
- Cross-validated feature selection

<div class="row">
 <div class="col-sm mt-3 mt-md-0">
     {% include figure.liquid loading="eager" path="assets/img/feature_engineering.png" title="Feature Engineering Process" class="img-fluid rounded z-depth-1" %}
 </div>
</div>
<div class="caption">
 Visualization of the feature engineering process, showcasing the transformation from raw data to engineered features.
</div>

## Technical Implementation

### Class Imbalance Solutions
- **SMOTE Implementation**
- Synthetic sample generation
- Balanced class distribution
- Enhanced model robustness

### Model Optimization
1. **Regularization Techniques**
- L1 (Lasso) for feature sparsity
- L2 (Ridge) for overfitting prevention
- Cross-validation for hyperparameter tuning

2. **Performance Metrics**
```python

metrics = {
'accuracy': 0.94,
'improvement': '12%',
'cross_validation': '5-fold',
'evaluation': ['confusion_matrix', 'ROC_curves']
}
```
This project demonstrates the effective application of advanced machine learning techniques to classify
human activities from sensor data. The implemented pipeline achieves high accuracy through careful feature engineering, model optimization, and handling of class imbalances.
---
For more details, visit the [GitHub repository](https://github.com/Hit07/human-activity-recognition-ml)