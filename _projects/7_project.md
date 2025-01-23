---
layout: page
title: Transfer Learning for Image Classification 
description: >
  Tech Stack: TensorFlow, Keras, scipy, scikit-learn
  Technologies: Deep Learning, Computer Vision, Transfer Learning, Data Augmentation, Model Evaluation
img: assets/img/Transfer_learning.png
importance: 1
category: Academic
related_publications: false
---
##  Overview

In this project,
I developed an advanced image classification system
using transfer learning techniques to distinguish between six different scene categories.
This work demonstrates my proficiency in deep learning, computer vision,
and practical application of the latest machine learning models.

<hr>

## Key Achievements

-   Implemented transfer learning using four pre-trained models: ResNet50, ResNet100, EfficientNetB0, and VGG16
    
-   Engineered a robust data pipeline for preprocessing and augmenting image data
    
-   Optimized model performance through fine-tuning and regularization techniques
    
-   Conducted comprehensive model evaluation and comparison

<hr>

## **Technical Approach**

## Data Preparation and Augmentation

I began by organizing the image dataset into class-specific folders and implementing one-hot encoding for labels. To ensure uniform input dimensions, I applied resizing and zero-padding techniques. To enhance model generalization, I implemented a suite of data augmentation methods, including:

-   Random cropping
    
-   Zooming
    
-   Rotation
    
-   Flipping
    
-   Contrast adjustment
    

These augmentation techniques significantly expanded the effective size of our training set and improved model robustness.

## Model Architecture and Training

For each pre-trained model (ResNet50, ResNet100, EfficientNetB0, VGG16):

-   Utilized the pre-trained networks as feature extractors
    
-   Fine-tuned the last fully connected layer while freezing earlier layers
    
-   Implemented ReLU activation in the hidden layers and softmax in the output layer
    
-   Applied L2 regularization, batch normalization, and dropout (20%) to prevent overfitting
    

The training process involved:

-   Using the ADAM optimizer with multinomial cross-entropy loss
    
-   Training for a minimum of 50 epochs (up to 100)
    
-   Implementing early stopping based on validation set performance
    
-   Utilizing a 20% validation split for each class
    
## Model Comparison

| Model            | Precision | Recall  | F1 Score | AUC   |
|-------------------|-----------|---------|----------|-------|
| ResNet50         | 0.7306    | 0.7280  | 0.7262   | 0.9441 |
| ResNet101V2      | 0.7003    | 0.6997  | 0.6979   | 0.9333 |
| EfficientNetB0   | 0.0494    | 0.1673  | 0.0761   | 0.7283 |
| VGG16            | 0.8863    | 0.8857  | 0.8856   | 0.9881 |

**Best performing model based on F1 Score:** VGG16


## Performance Evaluation

To assess and compare model performance:

-   Tracked and visualized training and validation errors across epochs
    
-   Calculated Precision, Recall, AUC, and F1 scores for training, validation, and test sets
    
-   Conducted a comparative analysis of model performances to identify the most effective architecture for this specific task
    
---

To check out the project code, visit the [GitHub repository](https://github.com/Hit07/Transfer_Learning-CNN)