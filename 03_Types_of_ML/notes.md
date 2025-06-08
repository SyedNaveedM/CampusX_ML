# Video 3: Types of Machine Learning

## Main Categories

### 1. Supervised Learning
- **Definition**: Learning with labeled training data
- **Goal**: Predict output for new inputs based on input-output pairs
- **Data**: Has both features (X) and target labels (y)

#### Types:
**Classification**
- Predicts discrete categories/classes
- Examples: Email spam detection, image recognition, disease diagnosis
- Algorithms: Logistic Regression, Decision Trees, SVM, Random Forest

**Regression**
- Predicts continuous numerical values
- Examples: House price prediction, stock prices, temperature forecasting
- Algorithms: Linear Regression, Polynomial Regression, Ridge/Lasso

### 2. Unsupervised Learning
- **Definition**: Learning from data without labels
- **Goal**: Find hidden patterns and structures in data
- **Data**: Only features (X), no target labels

#### Types:
**Clustering**
- Groups similar data points together
- Examples: Customer segmentation, gene analysis, market research
- Algorithms: K-Means, Hierarchical Clustering, DBSCAN

**Association Rules**
- Finds relationships between different items
- Examples: Market basket analysis ("People who buy X also buy Y")
- Algorithms: Apriori, FP-Growth

**Dimensionality Reduction**
- Reduces number of features while preserving information
- Examples: Data visualization, noise reduction, feature selection
- Algorithms: PCA, t-SNE, LDA

### 3. Semi-Supervised Learning
- **Definition**: Learning with both labeled and unlabeled data
- **Goal**: Improve performance using small labeled + large unlabeled datasets
- **Data**: Mix of labeled (X,y) and unlabeled (X only) data

#### Key Concepts:
- Uses small amount of labeled data to guide learning
- Leverages large amounts of unlabeled data
- Combines benefits of both supervised and unsupervised learning

#### Examples:
- Web page classification (few labeled pages, millions unlabeled)
- Medical image analysis (limited expert annotations)
- Speech recognition with limited transcripts
- Text classification with few labeled documents

#### Common Approaches:
- **Self-training**: Use model predictions on unlabeled data
- **Co-training**: Multiple models train on different feature sets
- **Graph-based**: Propagate labels through data similarity graphs

### 4. Reinforcement Learning
- **Definition**: Learning through interaction with environment
- **Goal**: Maximize cumulative reward through trial and error
- **Components**: Agent, Environment, Actions, Rewards, States

#### Examples:
- Game playing (AlphaGo, Chess)
- Autonomous vehicles
- Trading algorithms
- Robotics control

## Quick Comparison

| Type | Data Required | Goal | Examples |
|------|---------------|------|----------|
| **Supervised** | Labeled (X,y) | Predict labels | Classification, Regression |
| **Unsupervised** | Unlabeled (X only) | Find patterns | Clustering, Association |
| **Semi-Supervised** | Labeled + Unlabeled | Improve with limited labels | Web classification, Medical imaging |
| **Reinforcement** | Environment feedback | Maximize reward | Games, Robotics |

## Key Decision Framework

### Choose Supervised Learning when:
- You have labeled data
- Want to predict specific outcomes
- Clear input-output relationship exists

### Choose Unsupervised Learning when:
- No labeled data available
- Want to explore data structure
- Looking for hidden patterns

### Choose Semi-Supervised Learning when:
- Limited labeled data but lots of unlabeled data
- Labeling is expensive or time-consuming
- Want to improve supervised model performance

### Choose Reinforcement Learning when:
- Sequential decision making needed
- Learn from trial and error
- Maximize long-term rewards

## Memory Tips

- **Supervised** = Teacher guides learning (has answers)
- **Unsupervised** = Self-discovery (no answers provided)
- **Semi-Supervised** = Partial guidance (few answers + lots of practice)
- **Reinforcement** = Learning from consequences (trial & error)

## Common Algorithms Summary

### Supervised:
- Classification: Decision Trees, SVM, Naive Bayes
- Regression: Linear/Polynomial Regression, Ridge/Lasso

### Unsupervised:
- Clustering: K-Means, DBSCAN
- Dimensionality: PCA, t-SNE

### Reinforcement:
- Q-Learning, Policy Gradient, Actor-Critic