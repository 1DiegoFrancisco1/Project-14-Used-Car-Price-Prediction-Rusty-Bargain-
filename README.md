# 🚗 Project 14 — Used Car Price Prediction (Rusty Bargain)

### 🏢 Project Context
**Rusty Bargain** is a second-hand car marketplace developing a mobile app that estimates the **market value** of vehicles based on technical specifications and historical sales data.

Your task was to build and compare several **machine learning models** that predict a car’s market price efficiently — balancing **prediction quality, training speed, and inference time**.

---

## 🎯 Project Objectives
- Predict the **market price** of used vehicles.  
- Compare at least **four different ML models** (linear and nonlinear).  
- Evaluate **training time**, **prediction time**, and **model accuracy**.  
- Select the best model for **production deployment**.

---

## 🧹 Step 1 — Data Cleaning and Preprocessing

### ✅ Preprocessing Summary

1. **Duplicate Removal**  
   - 262 duplicate records removed to improve dataset integrity.

2. **Missing Value Treatment**  
   - Filled missing categorical values (`VehicleType`, `Gearbox`, `Model`, `FuelType`, `NotRepaired`) with `"unknown"`.  
   - Preserved maximum data for model training.

3. **Target (`Price`) Cleaning**  
   - Removed rows with `Price = 0` as invalid market entries.

4. **Power (`Power`) Correction**  
   - Replaced unrealistic values (`0` or `>1000 HP`) with NaN.  
   - Imputed missing values using **median power per brand** for realistic ranges.

5. **Irrelevant Features**  
   - Dropped `NumberOfPictures` since all values were zero.

After cleaning, the dataset was consistent, complete, and ready for exploration and modeling.

---

## 🌳 Step 2 — Feature Importance (Decision Tree Model)

After training an optimized **Decision Tree**, feature importances were analyzed:

| Feature | Importance (%) | Insight |
|----------|----------------|----------|
| `RegistrationYear` | **50.1** | Most decisive factor — newer cars are worth more. |
| `Power` | **28.7** | Strong influence — more powerful cars hold higher value. |
| `VehicleType_unknown` | **7.9** | Missing or ambiguous body type affects price predictions. |
| `Mileage` | **3.0** | Moderate influence — higher mileage reduces price. |
| `VehicleType_convertible` | **1.4** | Special case — niche pricing behavior. |
| `Model`, `NumberOfPictures` | ~0.0 | Little to no contribution. |

📈 **Conclusion:**  
The model relies mainly on **car age, power, and body type**, aligning perfectly with real-world car market trends.

---

## ⚙️ Step 3 — Model Comparison

Several algorithms were trained and tuned to find the best balance between accuracy and computational efficiency.

| Model | RMSE (€) | R² | Training Time | Comments |
|--------|----------:|------:|----------------:|-----------|
| **Linear Regression** | ≈ 2900 | 0.59 | ~0.01 s | Simple sanity check — fast but inaccurate. |
| **Decision Tree (tuned)** | ≈ 1889 | 0.83 | <1 s | Captures nonlinearities; interpretable. |
| **Gradient Boosting (sklearn)** | ≈ 1775 | 0.85 | ~318 s | High precision but slow training. |
| **LightGBM** | **≈ 1569** | **0.88** | **18–40 s** | ✅ Best trade-off between speed & accuracy. |
| **XGBoost** | ≈ 1640 | 0.87 | ~530–967 s | Good results but slow — less practical. |

---

## 🧠 Step 4 — Insights and Analysis

### Model Insights
- **Linear Regression** serves as a baseline — confirms superiority of advanced methods.  
- **Decision Tree** provides explainability with good speed — ideal as a quick baseline.  
- **Gradient Boosting** improves accuracy significantly but requires longer training.  
- **LightGBM** emerges as **the most balanced and production-ready** model.  
- **XGBoost** offers comparable results but with higher computational cost.

---

## ⚡️ Step 5 — Final Conclusions

- **Linear Regression**: good sanity check, poor predictive power.  
- **Decision Tree**: interpretable and fast, but slightly less accurate.  
- **Gradient Boosting**: excellent precision, slow training.  
- **LightGBM**: ⭐ **Winner** — best accuracy–speed trade-off, handles categorical features efficiently.  
- **XGBoost**: solid alternative but slower; not optimal for production environments.

📊 **Final Verdict:**  
> **LightGBM** is the best model for **Rusty Bargain**, providing the **highest predictive accuracy** and **fast inference**, essential for a real-time car valuation app.

---

## 💡 Business Impact

- Enables instant **price estimation** for customers via mobile app.  
- Improves **trust and engagement** by giving accurate valuations.  
- Supports the company’s goal of **scaling listings efficiently** with data-driven automation.  
- Foundation for potential **dynamic pricing systems** in the future.

---

## 🧰 Tools and Libraries
- **Python:** pandas, numpy, scikit-learn, LightGBM, XGBoost  
- **Evaluation Metrics:** RMSE, R²  
- **Visualization:** matplotlib, seaborn  
- **Model Comparison:** time tracking, feature importance, cross-validation  

---

## 👨‍💻 Author
**Diego Francisco Domínguez Aguilar**  
Data Science Bootcamp – TripleTen (2025)
