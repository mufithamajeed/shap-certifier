# SHAP Certifier: A Formal Auditing Framework for AI Explanation Consistency

## Project Summary

In AI applications deployed in **healthcare, finance, and safety-critical environments**, it is not enough for models to be accurate, **their explanations must also be logically consistent and trustworthy**.

This project introduces **SHAP Certifier**:  
A lightweight auditing framework that formally checks whether **SHAP explanations** behave in line with **domain knowledge expectations**. We combine **SHAP values** with formal verification using **Z3 SMT solvers** to flag inconsistent or unstable model explanations.

---
## Dataset

This project uses the **Heart Disease UCI dataset** available from the **UCI Machine Learning Repository**:  
[https://archive.ics.uci.edu/ml/datasets/Heart+Disease](https://archive.ics.uci.edu/ml/datasets/Heart+Disease)

The dataset contains clinical and demographic features related to heart disease diagnosis and is commonly used for classification tasks in healthcare AI research.

The dataset was preprocessed to create a **binary classification target** indicating the **presence or absence of heart disease**.

---

## What We Did

We evaluated two machine learning models on the **Heart Disease UCI dataset**:

1. **Random Forest Classifier**
2. **Monotonic XGBoost Classifier** (with constraints ensuring that increasing **Age** should not decrease the predicted risk)

For both models:
- We computed **SHAP values** to explain individual predictions.
- We applied **formal monotonicity checks** using **Z3 SMT solving** to detect explanation inconsistencies.

---

## Key Findings

| Model                | Predictive Accuracy | AUC    | Explanation Inconsistency Rate |
|----------------------|--------------------|--------|---------------------------------|
| Random Forest        | 84%                | 89%    | 100%                           |
| Monotonic XGBoost    | 83%                | 89%    | 100%                           |

- Both models performed well in traditional predictive metrics.
- However, **every single instance** tested showed **at least one violation of explanation consistency**:
  - In some cases, **increasing Age** led to a **lower SHAP value** for Age or a **lower predicted risk**, contradicting common sense and medical reasoning.
- Even with **monotonic constraints**, **SHAP explanations** remained **locally unstable**, proving that constraining predictions is **not sufficient to ensure explanation consistency**.

---

## Why This Matters

- AI systems used in decision-making must not only predict accurately but also **explain consistently**.
- The **SHAP Certifier** highlights a critical issue: **Explanation-level inconsistencies often go undetected in standard AI evaluation**.
- By systematically auditing explanations, we can help prevent **silent failures** in AI decision support systems.

---

## Takeaways for Future Work

- **Explanation auditing** should be a **standard step** in model validation pipelines, especially in regulated domains.
- Alternative explanation methods or **explanation-regularized training** may help reduce inconsistencies.
- The approach demonstrated here is **model-agnostic** and can be extended to other datasets, features, and explanation frameworks.

---

> **Key Insight:**  
> Even models designed to respect monotonicity in predictions can produce **inconsistent or illogical explanations**—and these inconsistencies can (and should) be formally detected before deployment.


## License

This project is provided **for educational and portfolio display purposes only**.  
All rights reserved © [Mufitha Majeed], [2025].  
Reuse, modification, redistribution, or commercial use of this work is **not permitted without explicit written consent**.
