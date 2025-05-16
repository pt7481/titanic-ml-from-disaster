## Project Summary

This project tackles the classic Kaggle challenge: predicting passenger survival on the Titanic using machine learning. It serves as a hands-on exercise in feature engineering, model development, and interpretability within a well-known dataset, allowing for deep exploration of structured data analysis and model evaluation techniques.

---

### What I Did

- Performed exploratory data analysis (EDA) to understand patterns in survival across features like class, gender, fare, and cabin location.
- Conducted advanced feature engineering, including interaction features (e.g., `Pclass × Sex × Age Group`) and smoothed binary indicators for rare subgroups.
- Handled missing values with targeted imputation strategies.
- Trained and tuned multiple models (e.g., XGBoost, Random Forest) and compared cross-validation scores across feature sets.
- Interpreted model predictions using SHAP values and worst-fold mistake analysis to identify sources of misclassification.
- Developed a modular, iterative framework for feature testing and scoring consistency.

---

### What I Learned

- How to systematically test the predictive power of engineered features using cross-validation and mistake analysis.
- The impact of overrepresented or underrepresented groups on feature reliability and generalization.
- The value of designing interpretable binary features for decision tree models, especially when dealing with small or extreme-case subgroups.
- Best practices for combining domain intuition with statistical evidence when crafting features.
- How to balance model complexity with interpretability through visualizations and score decomposition.

---

### What's Next

- Automate feature testing and scoring pipelines for faster iteration.
- Expand into ensemble methods and stacking with model-specific feature subsets.
- Try alternative modeling techniques like LightGBM or TabNet.
- Experiment with semi-supervised learning or active learning to handle small or ambiguous passenger groups.
- Submit final models to Kaggle and track performance over time with versioned feature sets.
