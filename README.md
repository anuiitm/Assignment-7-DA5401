# Assignment-7-DA5401
## NAME - Anubhav agarwal
## Roll No - HS22H059
## Documentation
### The repo contains a .ipynb file and README.md file, the main submission is in .ipynb file. Please use that to see my work

# Machine Learning Model Comparison for Statlog (Landsat Satellite) Dataset
## Dataset
*   **Name**: Statlog (Landsat Satellite)
*   **Source**: UCI Machine Learning Repository (ID: 146)
*   **Description**: Contains multi-spectral values of pixels from a satellite image to classify the central pixel's land cover. Class label '6' (mixture class) was intentionally removed from the dataset as per instructions.
*   **Features (X)**: 36 integer attributes (multi-spectral values) representing 3x3 pixel neighborhoods.
*   **Target (y)**: 1 categorical attribute ('class') representing the land cover type (classes 1, 2, 3, 4, 5, 7).

## Methodology

### Part A: Data Preparation and Baseline
1.  **Data Loading and Filtering**: The Landsat dataset was loaded, and all instances with class label '6' were removed.
2.  **Feature Standardization**: Features (X) were standardized using `StandardScaler` to ensure uniform scaling.
3.  **Train/Test Split**: The data was split into training (70%) and testing (30%) sets with `random_state=42`.
4.  **Model Training**: Six initial classification models were trained:
    *   K-Nearest Neighbors (`KNeighborsClassifier`)
    *   Decision Tree Classifier (`DecisionTreeClassifier`)
    *   Dummy Classifier (`DummyClassifier(strategy='prior')`)
    *   Logistic Regression (`LogisticRegression`)
    *   Gaussian Naive Bayes (`GaussianNB`)
    *   Support Vector Machine (`SVC(probability=True)`)
5.  **Baseline Evaluation**: Each model's performance was evaluated using Overall Accuracy and Weighted F1-Score on the test set.

### Part B: ROC Analysis for Model Selection
1.  **One-vs-Rest (OvR) Explanation**: A detailed explanation of how the One-vs-Rest strategy extends ROC curves and AUC calculation to multi-class problems was provided.
2.  **Target Binarization**: The target variable `y_test` was one-hot encoded using `LabelBinarizer` for OvR evaluation.
3.  **OvR ROC and AUC Calculation**: For each model, individual class ROC curves and AUC scores were calculated using the OvR approach. Macro-averaged AUC was computed.
4.  **ROC Plotting**: A single plot displaying macro-averaged OvR ROC curves for all models, including a random classifier baseline, was generated.
5.  **ROC Interpretation**: Models were ranked by Macro-averaged AUC, and the implications of an AUC < 0.5 were discussed.

### Part C: Precision-Recall Curve (PRC) Analysis
1.  **PRC Suitability Explanation**: An explanation was provided on why PRC is a more suitable metric than ROC for highly imbalanced datasets, emphasizing its sensitivity to False Positives and focus on the minority class.
2.  **OvR Precision-Recall and AP Calculation**: For each model, Precision, Recall, and Average Precision (AP) for each class were computed using the OvR approach. Macro-averaged AP was calculated.
3.  **PRC Plotting**: A single plot displaying macro-averaged OvR Precision-Recall curves for all models, including a random classifier baseline, was generated.
4.  **PRC Interpretation**: Models were ranked by Macro-averaged AP, and the behavior of the worst-performing model's PRC (Dummy Classifier) was analyzed.

## Brownie Points Task: Experimentation with Additional Models
1.  **Additional Models Trained**:
    *   Random Forest (`RandomForestClassifier`)
    *   XGBoost (`XGBClassifier`)
    *   Uniform Dummy Classifier (`DummyClassifier(strategy='uniform')`)
2.  **Extended Evaluation**: All metrics (Accuracy, F1-Score, Macro-averaged AUC, Macro-averaged AP) were calculated for these new models.
3.  **Comprehensive Visualization**: Consolidated bar plots comparing all nine models across all four metrics were generated.

## Key Findings & Recommendation

### Model Rankings
Across all key metrics (F1-Score, Macro-averaged AUC, and Macro-averaged AP), the models consistently ranked as follows:

*   **Top Performers**: **XGBoost** and **Random Forest** consistently achieved the highest scores, demonstrating superior performance.
*   **Mid-Range Performers**: K-Nearest Neighbors, Support Vector Machine, Logistic Regression, and Gaussian Naive Bayes showed competitive, though slightly lower, performance.
*   **Worst Performers**: The Dummy Classifier and Uniform Dummy Classifier performed at or near random chance, serving as effective baselines.

### Trade-offs (High ROC-AUC vs. Lower PRC-AP)
Some models, like Gaussian Naive Bayes, exhibited a relatively high Macro-averaged AUC but a comparatively lower Macro-averaged AP and F1-Score. This indicates that while such models are good at separating classes generally (discriminative power), their precision might suffer, especially when striving for high recall, leading to more false positives. PRC is more sensitive to these trade-offs, making it crucial for imbalanced scenarios.

### Final Recommendation

Based on the comprehensive analysis across all evaluated metrics, the **XGBoost** model is recommended as the **superior choice** for the Statlog (Landsat Satellite) classification task. It consistently achieved the highest scores in:

*   **Accuracy**: 0.9146
*   **Weighted F1-Score**: 0.9131
*   **Macro-averaged AUC**: 0.9892
*   **Macro-averaged AP**: 0.9503

XGBoost's robust and well-rounded performance, particularly its excellent balance between precision and recall (as indicated by its leading AP score), makes it the most reliable and effective model for accurately classifying satellite image pixels.
