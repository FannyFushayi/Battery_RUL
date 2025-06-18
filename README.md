# Battery RUL Prediction Project

## 🔋 Overview

This project explores data-driven methods for predicting the Remaining Useful Life (RUL) of lithium-ion batteries using machine learning. The central motivation stems from an earlier hybrid energy storage system (HESS) project where thermal stress on the battery was reduced using a supercapacitor. While it was possible to quantify the temperature reduction, translating that into a measurable increase in cycle life proved elusive.

This project aims to answer that question: *How many extra cycles can be gained by reducing stress on a battery?* To do this, we leverage the HNEI dataset, which provides structured cycle-level features across multiple battery cells.

---

## 🧠 Project Goals

- Understand and visualize battery degradation patterns.
- Explore multiple machine learning and (later) deep learning pipelines for RUL prediction.
- Evaluate trade-offs between generalization and specialization in modeling battery health.
- Benchmark various data split strategies for model training and validation.
- Build toward a generalizable, ensemble-based RUL estimation framework.

---

## 📁 Repository Structure (Data Splits)

To systematically investigate model behavior under different assumptions, this project uses versioned data splits:

- **`ver_1`** – No explicit validation strategy. Full dataset used for both training and testing. Quick prototyping baseline.
- **`ver_2`** – Battery-wise split. Each model is trained on a subset of batteries and tested on unseen batteries. This tests generalization to new batteries.
- **`ver_3`** – End-of-life (EOL) split. For each battery, the last 200 cycles are held out for testing. This mimics a realistic predictive maintenance scenario: forecasting how much life remains based on earlier usage.

Each version is stored in a separate folder (actually not anymore folders feel like hard work for some reason) with associated scripts and notebooks for reproducibility.

---

## 🧪 Current Findings

- **Models perform better on later-cycle predictions** than on early-cycle predictions. This is likely due to stronger degradation signals (voltage drop, capacity loss) that are easier for models to detect.
- **Including `battery_id` as a feature improves performance**, but raises questions of data leakage. For generalization tests, we exclude it.
- Outlier filtering using Isolation Forest improved RMSE slightly, suggesting some noisy cycles skewed earlier results.
- So far, ensemble tree models (Extra Trees, XGBoost) have outperformed other methods using engineered features.
- Future directions include using sequence models (e.g., LSTM) once time-like features or temporal ordering is better defined.

---

## ⚠️ Known Limitations

- The HNEI dataset, while rich, represents *accelerated cycling tests* under lab conditions. This may not fully reflect real-world battery usage patterns.
- There is no impedence or Temperature Related Data 
- The dataset does not explicitly include time stamps, which limits the use of time-series models unless surrogate features (e.g., cycle count or duration) are constructed.

---

## 📌 Next Steps

- Finalize data pipelines for each version (ver_1, ver_2, ver_3).
- Perform full model benchmarking across splits using consistent metrics (RMSE, MAE, R²).
- Develop a hybrid ensemble that combines classical ML with sequence-based deep learning models.
- Investigate model interpretability using SHAP or permutation feature importance.

---

## 👨‍🔬 Author

Fanny Fushayi  
Electrical Engineer | ML Enthusiast | Independant "Researcher"

---

## 📜 License

MIT License (or your license of choice, should be prestigious)
