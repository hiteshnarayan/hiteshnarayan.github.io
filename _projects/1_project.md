---
layout: page
title: Multimodal Emotion Recognition with Feature Fusion
description: Deep Learning approach for emotion classification using unimodal models and early/late fusion techniques in PyTorch.
img: assets/img/iemocap_preview.jpg
importance: 2
category: Machine Learning
github: https://github.com/hiteshnarayan/Multimodal-Emotion-Recognition
tags: [ pytorch, fusion, resnet, vggish, bert, emotion-ai,multimodal, iemocap, emotion-recognition ]
---

## Overview

This project implements multimodal emotion recognition on the IEMOCAP dataset, classifying utterances into 4 emotion
classes using pre-extracted ResNet visual features, VGGish audio features, and BERT text embeddings.The project focused
on comparing different feature fusion strategies and understanding when multimodal approaches outperform single-modality
methods.

## Dataset

IEMOCAP (Interactive Emotional Dyadic Motion Capture) is a 12‑hour multimodal corpus of dyadic emotional conversations
from 10 actors, offering synchronized ResNet‑2048 visual, VGGish‑128 acoustic and BERT‑768 textual features.
All features are speaker‑normalized across four emotion classes (Anger, Sadness, Happiness, Neutral)
For more details, refer to the [IEMOCAP dataset documentation](https://sail.usc.edu/iemocap/).

**Core Challenge:** How to effectively combine features from different modalities with different temporal structures.

## Model Architecture

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/iemocap/iemocap_model_architecture.png" title="Fusion-Based Multimodal Architecture for Emotion Recognition" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

- The architecture performs multimodal emotion classification using lexical (BERT), acoustic (VGGish), and visual (
  ResNet) features from the IEMOCAP dataset.
- Temporal mean pooling is applied to align modalities, followed by early or late fusion strategies to combine
  representations.
- A neural network classifier predicts one of four emotion classes: Happiness, Anger, Sadness, or Neutral.

## Methodology

Our approach follows a systematic three-stage pipeline: unimodal classification, multimodal fusion, and neural network
classification.

### Stage 1: Unimodal Feature Processing

Each modality is processed independently to establish baseline performance and understand individual modality
contributions:

#### Temporal Pooling for Visual and Acoustic Features:

```python
def temporal_pooling(features, method='mean'):
    """
    Reduce temporal dimension using mean pooling
    Args:
        features: Input features with temporal dimension
        method: Pooling method ('mean' or 'max')
    """
    if features is None or features.size == 0:
        return None
    if method == 'mean':
        return np.mean(features, axis=0)
    elif method == 'max':
        return np.max(features, axis=0)
    return features

```

Next, we implement unimodal classifiers for each modality using a simple feedforward neural network architecture.Each
classifier is trained independently on its respective modality features.

#### Unimodal Neural Network Architecture:

```python
class ModalityClassifier(nn.Module):
    def __init__(self, input_dim, hidden_dim=128, num_classes=4):
        super(ModalityClassifier, self).__init__()
        self.model = nn.Sequential(
            nn.Linear(input_dim, hidden_dim),  # First hidden layer
            nn.ReLU(),  # hidden_dim, hidden_dim // 2),  # Second hidden layer (64 neurons)
            nn.ReLU(),
            nn.Linear(hidden_dim // 2, num_classes)  # Output layer (4 emotions)
        )

    def forward(self, x):
        return self.model(x)

```

### Stage 2: Multimodal Fusion Strategies

After establishing unimodal baselines, we implement two fusion approaches to combine information from all modalities:

#### Early Fusion (Feature-Level):

```python
class EarlyFusionModel(nn.Module):
    def __init__(self, visual_dim, acoustic_dim, lexical_dim, hidden_dim=256, num_classes=4):
        super(EarlyFusionModel, self).__init__()
        # Concatenate all feature dimensions
        self.combined_dim = visual_dim + acoustic_dim + lexical_dim  # 2048 + 128 + 768 = 2944

        self.model = nn.Sequential(
            nn.Linear(self.combined_dim, hidden_dim),
            nn.ReLU(),
            nn.Linear(hidden_dim, hidden_dim // 2),
            nn.ReLU(),
            nn.Linear(hidden_dim // 2, num_classes)
        )

    def forward(self, x):
        return self.model(x)


# Feature concatenation process
def early_fusion_preprocessing(visual_features, acoustic_features, lexical_features):
    """
    Concatenate normalized features from all modalities
    """
    # Normalize each modality separately
    visual_scaler = StandardScaler()
    acoustic_scaler = StandardScaler()
    lexical_scaler = StandardScaler()

    visual_normalized = visual_scaler.fit_transform(visual_features)
    acoustic_normalized = acoustic_scaler.fit_transform(acoustic_features)
    lexical_normalized = lexical_scaler.fit_transform(lexical_features)

    # Concatenate along feature dimension
    fused_features = np.hstack((visual_normalized, acoustic_normalized, lexical_normalized))
    return fused_features

```

#### Late Fusion (Decision-Level):

```python
def late_fusion_majority_vote(visual_preds, acoustic_preds, lexical_preds):
    """
    Combine predictions from individual modality classifiers using majority voting
    """
    # Stack predictions from all modalities
    stacked_preds = np.vstack([visual_preds, acoustic_preds, lexical_preds])

    # Apply majority voting for each sample
    majority_votes = np.apply_along_axis(
        lambda x: np.bincount(x, minlength=4).argmax(),  # 4 emotion classes
        axis=0,
        arr=stacked_preds
    )
    return majority_votes
```

### Stage 3: Training and Evaluation Pipeline

#### Cross-Validation Setup:

```python
def subject_independent_cv(features, labels, speakers, n_folds=5):
    """
    5-fold subject-independent cross-validation
    Ensures no speaker overlap between train and test sets
    """
    unique_speakers = np.unique(speakers)
    speaker_groups = np.array_split(unique_speakers, n_folds)

    for fold, test_speakers in enumerate(speaker_groups):
        test_mask = np.isin(speakers, test_speakers)
        train_mask = ~test_mask

        yield train_mask, test_mask, fold
```

*Note:*

#### Training Configuration:

- Optimizer: Adam (learning_rate=0.001, weight_decay=1e-5)
- Loss Function: CrossEntropyLoss
- Batch Size: 32
- Epochs: 50 with early stopping
- Evaluation Metric: F1-micro score for balanced class assessment

## Results

Evaluated using 5-fold subject-independent cross-validation:

| Method       | F1-Score |
|--------------|----------|
| Early Fusion | 62.56%   |
| Text Only    | 62.25%   |
| Late Fusion  | 54.31%   |
| Audio Only   | 53.27%   |
| Visual Only  | 38.39%   |

**Key Findings:**

- The early fusion method outperforms the unimodal features and late fusion method, with a mean F1 score of 62.56%.
- Early has the higher F-1, which is likely more effective because it integrates the different modalities' features
  before any processing, allowing the model to capture relationships between them more effectively.
- Apparently, combining features at an earlier stage may provide a more holistic representation of the data, improved
  classification performance.

---
<div class="row">
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/iemocap/performance_comparison.png" title="Performance Comparison Across Methods" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
The above figure illustrates the performance comparison across different methods, highlighting the superiority of early fusion.

--- 
<div class="row">
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/iemocap/modality_contribution.png" title="Individual Modality Contributions" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
The above figure shows the individual contributions of each modality to the overall classification performance, indicating that visual features contribute the least, while text and audio features are more informative.

## REFERENCES

- [IEMOCAP Dataset](https://sail.usc.edu/iemocap/)
- GRATITUDE TO [Prof. Mohammad Soleymani](https://soleymani.org/) for providing the dataset and guidance on the project.
- [PyTorch Documentation](https://pytorch.org/docs/stable/index.liquid) for model building and training utilities.
- Hugging Face's [Transformers](https://huggingface.co/transformers/) library for BERT embeddings.

## Future Directions

1. **Advanced Fusion:** Attention-based mechanisms for dynamic modality weighting
2. **Temporal Modeling:** RNN/Transformer architectures to preserve sequence information
3. **Real-time Deployment:** Optimize for live emotion recognition applications
4. **Cross-dataset Evaluation:** Test generalization on other multimodal emotion datasets

---

## Conclusion

*This project demonstrates the complexity and potential of multimodal emotion recognition, highlighting both the promise
of fusion techniques and the challenges in aligning diverse data modalities for optimal performance.*



