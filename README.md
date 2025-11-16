# 🏀 XAI-NBA Injury Risk Prediction  
*Predicting NBA player injury severity with Explainable AI (XAI)*

This project builds an explainable machine learning model to predict **injury severity** for NBA players using performance statistics, physical attributes, and historical injury data. The goal is to provide **transparent, interpretable insights** that help coaches, analysts, and sports scientists understand not just *when* injuries might occur, but *why* a player may be at risk.

The project uses **XGBoost** for multi-class classification and **SHAP/LIME** for model explainability.

---

## 🚀 Features

- Multi-class injury severity prediction:
  - **None**, **Minor**, **Moderate**, **Severe**
- Custom-built **XGBoost classifier**
- Addressed class imbalance using **SMOTE**
- Visual explanations using **SHAP** (global + local)
- Local threshold-based explanations using **LIME**
- Player-level injury risk interpretation
- Real NBA data from the **2024–2025 season**

---

## 📊 Project Motivation

NBA injuries continue to increase in frequency and severity, affecting:
- Team performance  
- Player longevity  
- Financial outcomes  
- Competitive fairness  

The 2024–25 season saw:
- Many teams with **8–10 players injured simultaneously**
- Certain teams exceeding **400+ missed player-days**
- Players like Taylor Hendricks and De’Anthony Melton missing **150+ days**
- Others (Ben Simmons, LaMelo Ball, Ja Morant) experiencing **10+ separate injuries**

Given the growing complexity of load management and performance risk, a transparent and interpretable model is essential.

---

## 📁 Datasets

### **1. Pro Sports Transaction Dataset**
Scraped from ProSportsTransactions.com:
- Injury dates (start/end)
- Injury descriptions & categories
- Player identity & team
- Calculated injury durations  
Special handling applied for “out for season” cases.

### **2. NBA Player Statistics Dataset**
Compiled from public NBA stats sources:
- Biometric data (age, height, weight)
- Season & game-level performance metrics
- Fouls, turnovers, contested shots, and more
- Historical injury counts  
Top ~300 players selected (top 10 per team).

### **Merged Dataset**
Joined by player name and enriched with:
- Total injuries
- Total days missed
- Derived severity labels

---

## 🔧 Preprocessing

### **Injury Severity Labels**

| Class | Definition |
|-------|------------|
| None | 0 games missed |
| Minor | 1–3 games missed |
| Moderate | 4–9 games missed |
| Severe | 10+ games missed |

Most players fell into the **Severe** category, reinforcing the need for robust modeling.

### Additional Engineering
- Height/weight analysis by injury type
- Correlation matrix evaluation
- Removal of highly redundant metrics
- Exploratory injury type labels (lower, upper, hand, major, etc.)

---

## 🤖 Model: XGBoost Classifier

The model was trained:
- From scratch (no pre-trained weights)
- With **softmax** multi-class output
- Using **SMOTE** for minority class oversampling
- With manual hyperparameter tuning (learning rate, depth, estimators)

### **Evaluation Metrics**
- Precision, recall, F1
- Confusion matrix
- Macro & weighted averages  
Model achieved **~71% accuracy** on the validation set.

### Key Findings
- Strong performance on **None** and **Minor** classes
- Moderate injuries were hardest to classify
- Severe often confused with Moderate due to overlapping workload patterns

---

## 🧠 Explainability (XAI)

### 🔹 SHAP (Global & Local Explanations)

Key global predictors:
- **Minutes Played (MP)** — strongest indicator across multiple classes
- **3P%, FG%, PTS** — proxies for offensive workload
- **Age & Weight** — higher physical strain risk
- **PF & TOV** — indicators of aggressive or chaotic play

SHAP waterfall plots provide individualized reasoning, showing feature contributions for:
- None  
- Minor  
- Moderate  
- Severe predictions  

### 🔹 LIME (Local Explanations)

LIME highlights threshold-based interpretations such as:
- Low minutes + low height → increased likelihood of *None*
- High fouls/blocks + younger age → *Minor*
- High turnovers + lower FG% → *Moderate*
- High weight + low 3P% + low minutes → *Severe*

---

## 📈 Results Summary

- Model identifies injury-free players reliably
- Performs well distinguishing minor vs. severe injuries
- Moderate injury category remains challenging due to shared statistical patterns
- XAI analysis reveals intuitive and counterintuitive risk factors

---

## 🔭 Future Work

To enhance predictive power:
- Integrate **time-series data** (fatigue accumulation, back-to-backs, travel)
- Add **biomechanics** or medical context
- Include **multi-season training**
- Improve class definition granularity

---

## 🏁 Conclusion

This project demonstrates that explainable AI can provide meaningful insights into NBA injury risk. By combining real-game performance metrics with transparent XAI tools, this system can help teams better understand how player workload, physical traits, and play style contribute to injury likelihood.

---
