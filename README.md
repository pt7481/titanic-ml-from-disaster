# 🚢 Titanic: Machine Learning from Disaster

## Project Summary

This project tackles the classic Kaggle challenge: predicting passenger survival on the Titanic using machine learning. It serves as a hands-on exercise in feature engineering, model development, and interpretability within a well-known dataset, allowing for deep exploration of structured data analysis and model evaluation techniques.

---

### What I Did

- Conducted extensive feature engineering, combining domain knowledge and statistical validation to create globally smoothed target-encoded features and subgroup-specific smoothed features.
- Designed features around Pclass-Sex cohorts using conditional masking, binning, and normalization strategies (e.g., Pclass_Title_normalized, Age_Group, Deck_bin).
- Evaluated features using Chi-Squared tests, Cramér’s V, and cross-fold KL divergence, prioritizing variables with consistent distributions and statistically significant survival associations.
- Built a high-performing XGBoostClassifier pipeline, using ablation testing, SHAP plots, and hyperparameter tuning (e.g., max_depth, min_child_weight, gamma, reg_alpha) to balance accuracy and generalization.  Achieved a mean average accuracy of 0.8114 across cross-validation of the Kaggle training data set.
---

### What I Learned

- High cross-validation accuracy on the training set doesn't always translate to strong performance on the unseen test set — my 0.8114 CV accuracy dropped to 0.7727 on Kaggle's hidden test set. This highlighted how easily models can overfit to patterns specific to the training distribution, especially when engineered features subtly leak group identity or encode rare patterns that don't generalize.
- Smoothed rate encoding can outperform one-hot encoding when group sizes are sufficiently supported and carefully regularized to avoid leakage.
- Subgroup relevance masking (e.g., using Pclass_Sex) is tricky to enforce in practice; even zeroing out or setting NaNs doesn't fully eliminate feature leakage in tree-based models.
- KL divergence is a powerful diagnostic for assessing train–validation distribution shifts, especially for engineered composite features.
- SHAP plots revealed how certain features (e.g., P3_Female_Embarked_smoothed, Deck_bin) mislead the model when data sparsity or masking wasn't properly handled.
- Small gains in accuracy sometimes come at the cost of generalizability. Monitoring standard deviation in CV scores became as important as mean accuracy.
---

### What's Next

- Implement model ensembling to incorporate predictions from a complimentary model (e.g. LogisticRegression) to improve generalization to unseen data.
- Continue experimenting with features and model configurations to improve accuracy score.
- Continue refining SHAP-driven debugging workflows to triage false positives/negatives and identify data segments where the model is overconfident or blind.
