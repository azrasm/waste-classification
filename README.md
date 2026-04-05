# Waste Classification using ResNet50 & Transfer Learning

Manual waste sorting is slow and prone to human error. This project implements an automated system for classifying waste into two categories: Organic and Recyclable, using a Convolutional Neural Network (CNN) based on the ResNet50 architecture to automate the identification of waste types from images.

## Dataset

The model was trained and tested using the **Waste Classification Data** from Kaggle:
* Total Images: 25,077
* Classes: Organic (O) and Recyclable (R)
* Training Set: 22,564 images (85%)
* Test Set: 2,513 images (15%)
* Characteristics: Real-world images with diverse backgrounds and lighting conditions, simulating actual recycling facility environments.

## Model Architecture & Training Strategy

The core of the system is ResNet50, a deep residual network known for its "skip connections" that prevent gradient vanishing.

* Experimental Approach

   Six different training experiments were conducted to find the optimal configuration:
  1. Base Transfer Learning: Freezing ResNet50 layers and adding a custom classification head.
  2. EarlyStopping: Increasing epochs (up to 30) with a patience mechanism to prevent overfitting.
  3. Fine-tuning: Unfreezing the last 15 layers of ResNet50 (resulted in overfitting).
  4. Learning Rate Adjustment: Testing lower learning rates for stability.
  5. Resolution Scaling: Testing 128x128 vs. 224x224 (lower resolution led to significant accuracy loss).
  6. Class Balancing (Final Model): Implementing class_weights to handle data imbalance and reduce bias toward the dominant class.

Selected Model: Experiment 6 was chosen as the final model due to its superior balance between accuracy and class-specific recall.

## Evaluation Results

The final model achieved a balanced performance, proving its ability to generalize on unseen data.

| Metric | Value | Interpretation |
| :--- | :---: | :--- |
| **Accuracy** | **0.7911** | Overall percentage of correctly classified images. |
| **Precision** | **0.7346** | Accuracy of positive (Recyclable) predictions. |
| **Recall** | **0.8264** | Ability to find all actual Recyclable items in the set. |
| **F1-Score** | **0.7778** | Harmonic mean of Precision and Recall. |
| **AUC-ROC** | **0.8600** | Model's ability to distinguish between classes. |

Key Insights:
+ Confusion Matrix: Low error rates, with a strong ability to correctly identify Recyclable waste (Recall: 0.83).
+ Precision-Recall Curve: Achieved an Average Precision (AP) of 0.83, indicating high stability across different decision thresholds.
+ Visualization: Testing on random samples confirmed that the model makes logical decisions, with errors occurring mostly on visually ambiguous items.

## User Interface (GUI)

The project includes an interactive web interface built with Gradio.

 + Input: Image upload.
 + Output: Predicted class (Organic/Recyclable) with a confidence probability score.

## Conclusion
The implementation of ResNet50 via Transfer Learning proved to be a technically viable approach for waste classification. By optimizing for class weights and using EarlyStopping, the model reached a test accuracy of ~79%.

While the initial target was 90%, the current results are consistent with state-of-the-art benchmarks for this specific, high-variance dataset. This system provides a solid foundation for future integration into "Smart Bins" or automated sorting lines.

## References

**Dataset:** https://www.kaggle.com/datasets/techsash/waste-classification-data

**Processed dataset and final model:** https://drive.google.com/drive/folders/1MGEcIYwJizm8w-NCIHjToBUdXcj1CE8x
