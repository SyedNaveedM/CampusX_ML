# ML Evaluation: Accuracy, Confusion Matrix & Error Types

## Confusion Matrix

The confusion matrix is a table used to evaluate the performance of a classification model. It shows the relationship between actual and predicted classifications.

### Binary Classification Confusion Matrix

```
                    PREDICTED
                 Negative  Positive
ACTUAL Negative    TN       FP
       Positive    FN       TP
```

### Key Terms
- **TP (True Positive)**: Correctly predicted positive cases
- **TN (True Negative)**: Correctly predicted negative cases
- **FP (False Positive)**: Incorrectly predicted positive cases (Type I Error)
- **FN (False Negative)**: Incorrectly predicted negative cases (Type II Error)

### Example: Medical Diagnosis
```
Disease Test Results:
                    PREDICTED
                 Healthy  Sick
ACTUAL  Healthy    85     5    (90 total)
        Sick        10    95   (105 total)
```

- **TP = 95**: Correctly identified sick patients
- **TN = 85**: Correctly identified healthy patients
- **FP = 5**: Healthy patients incorrectly labeled as sick
- **FN = 10**: Sick patients incorrectly labeled as healthy

## Accuracy

**Definition**: The proportion of correct predictions out of total predictions.

### Formula
```
Accuracy = (TP + TN) / (TP + TN + FP + FN)
```

### Example Calculation
Using the medical diagnosis example:
```
Accuracy = (95 + 85) / (95 + 85 + 5 + 10)
         = 180 / 195
         = 0.923 or 92.3%
```

### When Accuracy is Misleading

#### Class Imbalance Problem
Consider a rare disease affecting 1% of the population:
```
                    PREDICTED
                 Healthy  Sick
ACTUAL  Healthy    990     10   (1000 total)
        Sick         5      5   (10 total)
```

```
Accuracy = (990 + 5) / (990 + 5 + 10 + 5) = 995/1010 = 98.5%
```

**Problem**: High accuracy (98.5%) but the model only correctly identifies 50% of sick patients! A model that always predicts "healthy" would achieve 99% accuracy but be useless for diagnosis.

## Type I and Type II Errors

### Type I Error (False Positive)
- **Definition**: Rejecting a true null hypothesis
- **In classification**: Predicting positive when actual is negative
- **Symbol**: α (alpha)
- **Also called**: False alarm, false positive rate

#### Examples
- **Medical**: Diagnosing a healthy person as sick
- **Email**: Marking legitimate email as spam
- **Security**: Fire alarm going off when there's no fire
- **Legal**: Convicting an innocent person

### Type II Error (False Negative)
- **Definition**: Accepting a false null hypothesis
- **In classification**: Predicting negative when actual is positive
- **Symbol**: β (beta)
- **Also called**: Miss, false negative rate

#### Examples
- **Medical**: Missing a diagnosis (sick person labeled as healthy)
- **Email**: Spam email reaching inbox
- **Security**: Security system missing an intruder
- **Legal**: Failing to convict a guilty person

### The Trade-off

There's typically an inverse relationship between Type I and Type II errors:
- **Reducing Type I errors** → Usually increases Type II errors
- **Reducing Type II errors** → Usually increases Type I errors

### Decision Threshold Impact

In binary classification with probability scores:

```python
# Lower threshold (e.g., 0.3 instead of 0.5)
- More positive predictions
- Fewer Type II errors (fewer missed positives)
- More Type I errors (more false alarms)

# Higher threshold (e.g., 0.7 instead of 0.5)
- Fewer positive predictions  
- More Type II errors (more missed positives)
- Fewer Type I errors (fewer false alarms)
```

## Related Metrics

### Precision
Focus on minimizing Type I errors
```
Precision = TP / (TP + FP)
```
"Of all positive predictions, how many were actually positive?"

### Recall (Sensitivity, True Positive Rate)
Focus on minimizing Type II errors
```
Recall = TP / (TP + FN)
```
"Of all actual positives, how many did we correctly identify?"

### Specificity (True Negative Rate)
```
Specificity = TN / (TN + FP)
```
"Of all actual negatives, how many did we correctly identify?"

### F1-Score
Harmonic mean of precision and recall
```
F1 = 2 × (Precision × Recall) / (Precision + Recall)
```

## Multi-class Confusion Matrix

For problems with more than 2 classes:

```
           PREDICTED
         A    B    C
ACTUAL A  50   3    2   (55 total)
       B   5   45   5   (55 total)  
       C   1    2   47  (50 total)
```

### Calculating Metrics for Multi-class

For class A:
- **TP**: 50 (correctly predicted A)
- **FP**: 6 (predicted A but actually B or C)
- **FN**: 5 (actually A but predicted B or C)
- **TN**: 89 (correctly predicted not-A)

## Practical Considerations

### When to Prioritize Different Error Types

#### Minimize Type I Errors (False Positives) When:
- **Cost of false alarm is high**
- Email spam detection (don't want to lose important emails)
- Marketing campaigns (don't want to annoy customers)
- Medical screening with expensive follow-ups

#### Minimize Type II Errors (False Negatives) When:
- **Cost of missing positive is high**
- Disease diagnosis (don't want to miss sick patients)
- Fraud detection (don't want to miss fraudulent transactions)
- Security systems (don't want to miss threats)

### Domain-Specific Examples

#### Medical Diagnosis
```
Cancer Screening:
- Type I Error: Healthy person diagnosed with cancer
  - Consequences: Unnecessary stress, treatment, costs
- Type II Error: Cancer patient not diagnosed  
  - Consequences: Disease progression, potential death

Generally prefer Type I errors over Type II errors in medical diagnosis.
```

#### Legal System
```
Criminal Trial:
- Type I Error: Convicting innocent person
  - Consequences: Injustice, wrongful imprisonment
- Type II Error: Guilty person goes free
  - Consequences: Criminal remains in society

Legal system designed to minimize Type I errors ("innocent until proven guilty").
```

## Code Example: Calculating Metrics

```python
from sklearn.metrics import confusion_matrix, accuracy_score
import numpy as np

# Example predictions
y_true = [0, 1, 1, 0, 1, 0, 1, 1, 0, 0]
y_pred = [0, 1, 0, 0, 1, 1, 1, 1, 0, 0]

# Confusion matrix
cm = confusion_matrix(y_true, y_pred)
print("Confusion Matrix:")
print(cm)

# Extract values
tn, fp, fn, tp = cm.ravel()
print(f"TN: {tn}, FP: {fp}, FN: {fn}, TP: {tp}")

# Calculate metrics
accuracy = accuracy_score(y_true, y_pred)
precision = tp / (tp + fp)
recall = tp / (tp + fn)
specificity = tn / (tn + fp)

print(f"Accuracy: {accuracy:.3f}")
print(f"Precision: {precision:.3f}")
print(f"Recall: {recall:.3f}")
print(f"Specificity: {specificity:.3f}")
print(f"Type I Error Rate: {fp / (tn + fp):.3f}")
print(f"Type II Error Rate: {fn / (tp + fn):.3f}")
```

## Key Takeaways

### Accuracy Limitations
- Can be misleading with imbalanced datasets
- Doesn't distinguish between different types of errors
- May not align with business objectives

### Error Type Selection
- Consider the cost and consequences of each error type
- Domain knowledge is crucial for choosing the right metric
- Often need to balance both types based on business requirements

### Best Practices
- Always examine the confusion matrix, not just accuracy
- Consider multiple metrics together
- Validate performance on realistic, representative data
- Adjust decision thresholds based on error type priorities
- Use stratified sampling to handle class imbalance