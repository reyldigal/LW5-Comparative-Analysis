# LW5-Comparative-Analysis

## Google Colab Link: https://colab.research.google.com/drive/17_zenTBH1YSmXq8rd52bCiJfD-bjQy1e?usp=sharing

# Save model: https://drive.google.com/drive/folders/1fxN-cxWYg3gbViSm4HkWTvmzBQBgBIkw?usp=drive_link

# GUIDE QUESTIONS (FINAL REFLECTION)

### A. Model Performance

#### 1. Which pre-trained model achieved the highest accuracy? Why?
#### Answer: ResNet50 had the highest accuracy (98.20% validation accuracy). The deep architecture of 50 layers with skip connections enables it to learn complex features of the plant without vanishing gradients and hence is very effective in fine-grained tasks such as classification of 20 plant species.
#### 2. Which model had the lowest performance? What could be the reason?
#### Answer: MobileNetV2 had the lowest performance at 74.56% validation accuracy. This is because MobileNetV2 was originally designed to be used on mobile devices with depthwise separable convolutions in order to reduce the amount of computation in the model, which means that it has some loss of representational power. It does not have enough depth to extract fine-grained visual features for a complex 20 classes plant data set.
#### 3. How did loss values compare across models?
#### Answer: There is a significant gap in the MobileNetV2 model's ability to predict the images (Train: 0.8856, Val: 0.9808) suggesting low confidence in the model's predictions. EfficientNetB0 and ResNet50 were the two models with the lowest losses (less than 0.12), indicating high and confident predictions. ResNet50 recorded the least loss with 0.0454 loss on train and 0.0871 loss on validation.

### B. Evaluation Metrics
#### 4. Why is accuracy not enough to evaluate a model?
#### Answer: With unbalanced datasets, accuracy can be deceiving. One could have a model that will be very accurate just by guessing the majority class most of the time. Precision, Recall, F1-score and AUC provide a comprehensive understanding regarding the performance of a model in all classes including minority classes.
#### 5. Which model had the best F1-score? What does it indicate?
#### Answer: ResNet50 had the best F1-score at 0.9820. It means it's well-balanced in its precision and recall for all 20 plant classes – correctly identifying plants, whilst ensuring it has low false positives and false negatives.
#### 6. How did Precision and Recall differ across models?
#### Answer: Interestingly, MobileNetV2 showed lower precision (0.7498) and recall (0.7456) indicating a tendency to misclassify plant species. Both EfficientNetB0 and ResNet50 had above 0.97 for both metrics, which is quite high and indicates that both models rarely misclassified plants and missed very few correct plants.

### C. Confusion Matrix Analysis

#### 7. Which classes were frequently misclassified?
#### Answer: The diversity of plant classes in this dataset makes it difficult to determine which ones the model failed at best. The most likely cases for failure are those that have similar leaf shapes and colors, such as DwarfSnakePlant vs VariegatedSnakePlant, or FlossFlower vs WildWhitePetunia.
#### 8. What patterns did you observe in the confusion matrix?
#### Answer: The confusion matrix of the MobileNetV2 is probably more off diagonal, indicating that the plant species are often confused with each other because they have similar visual characteristics. EfficientNetB0 and ResNet50 matrices should be close to the diagonal: predictions should be close to correct, and there should be few confusions between classes.

### D. ROC and AUC

#### 9. Which model had the highest AUC score?
#### Answer: The best AUC (0.9967) was obtained by EfficientNetB0, just outperforming ResNet50 (0.9966). Both are exceptionally close, but EfficientNetB0 marginally outperforms in terms of class separability.
#### 10. What does AUC tell us about model performance?
#### Answer: AUC (Area Under the ROC Curve) - evaluation of model performance independent of the threshold. 1.0 is an ideal AUC score. All three models achieved AUCs of more than 0.95, with MobileNetV2's 0.9550 indicating it has some difficulty distinguishing between some of the plant classes compared to the other two.
### E. Explainability (Grad-CAM)

#### 11. What did Grad-CAM reveal about model decision-making?
#### Answer: Grad-CAM kind of showed which parts of each image every model really looked at during the predictions. The better performing ones, for example ResNet50 and EfficientNetB0, mostly shaded leaf textures and distinct patterns, plus those plant related structures, rather than random background. This usually meant their “feature attention” was more sensible and aligned with what youd expect from plant images.
#### 12. Did the model focus on relevant image regions?
#### Answer: ResNet50 along with EfficientNetB0 are mostly tuned to the plant itself, like leaves, flowers, and those standout textures too. Meanwhile MobileNetV2 , since it is usually less accurate, sometimes kind of veers off and learns from surrounding background regions or other unnecessary fragments of the image, in a few cases anyway.
#### 13. Which model produced the most meaningful heatmaps?
#### Answer: ResNet50 ended up giving the most meaningful Grad-CAM heatmaps, and it did so pretty consistently , it kept lighting up the plants key distinguishing parts like leaf shape color patterns and even the flower structures, which pretty much matches it having the highest accuracy.

### F. Model Comparison & Improvement
#### 14. Which model would you recommend for deployment? Why?
#### Answer: ResNet50 is really recommended for deployment, mostly because it shows the highest validation accuracy 98.20% , along with the lowest loss it seems to have, and also the best F1-score, 0.9820. It kind of shows strong generalization over all those 20 plant classes, with precision and recall that are pretty consistent, like almost steady.
#### 15. How can you further improve your best-performing model?
#### Answer: ResNet50 is still kinda improvable by doing things like: (1) unfreezing the upper layers a bit for fine tuning, (2) using data augmentation such as flips, rotations, or brightness shift, (3) putting in some learning rate scheduling so it dosent stay constant, (4) adding more training images per class, and (5) trying a bigger cousin variant like ResNet101.

### G. Real-World Application

#### 16. How can your model be applied in real-world scenarios?
#### Answer: The plant classification model can be used inside mobile apps for plant identification  for botanical garden kiosks, for agricultural monitoring systems, or even for teaching tools that help students and researchers figure out which species of plant it is, mostly by seeing photos . It kind of works as a sort of digital assistant, matching visual data to plant taxonomy, while the user snaps a picture.
#### 17. What are the risks of deploying an inaccurate model?
#### Answer: If a model is inaccurate it might misidentify plant species , which then results in care directions that are off, and even could lead to accidentally using toxic plants. It can also cause the wrong type of pesticide application in agriculture , plus plant disease misdiagnosis, and that can seriously hurt in real-world situations, really.
#### 18. How can this system be integrated into a mobile/web app?
#### Answer: The .keras saved model can be turned into TensorFlow Lite, for mobile placement , or it can be served through a Flask/FastAPI backend for web apps. In practice users upload a photo of a plant, through the interface, and that image is sent over to the model for classification, then it comes back with the identified species and a confidence ranking . So, basically it helps the app react quickly and in a rather transparent way .


