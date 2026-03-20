# Zomathon-Recommender-System-Top-10-
Food Cart Add-On Recommendation System
# 🍽️ Cart Super Add-On Recommendation System (CSAO)

🚀 Built during **Zomathon 2026 (Coding Ninjas × Eternal)**
👥 Team: *Kachow* — IIT (BHU) Varanasi

---

# 📌 Overview

Cart Super Add-On (CSAO) is a **context-aware recommendation system** designed to suggest relevant add-ons (e.g., drinks, sides, desserts) during cart building in food delivery platforms.

The goal is to:

* Increase **Average Order Value (AOV)**
* Improve **add-on acceptance rate**
* Maintain **low-latency production performance**

---

# ❓ Why This Problem?

* As users ourselves, we identified this as a **high-impact real-world problem**
* Add-on recommendations directly influence:

  * 🍽️ Order completeness
  * 💰 Revenue (AOV)
  * 📈 User engagement

---

# 🧠 Problem Formulation

We model this as a:

> **Context-Aware Ranking Problem**

Given:

* Current cart items
* User preferences
* Restaurant context

👉 Rank candidate add-ons by **relevance score**

---

# 📊 Data Generation Strategy

Due to lack of unbiased public datasets, we designed a **synthetic data pipeline**.

## 🔹 Why not Kaggle data?

* Region/cuisine biased
* Not representative of full ecosystem

---

## 🔹 Our Approach: Simulated Dataset

We generated a dataset representing:

* Users
* Restaurants
* Orders
* Add-ons

### Example Distributions:

* Veg vs Non-Veg: **40% / 60%**
* Cuisine mix: North Indian, South Indian, Chinese, Italian, Fast Food, Biryani

---

## 🔹 Session Simulation

* Orders grouped by `user_id`
* Sorted by time
* Cart-level context preserved

---

## 🔹 Negative Sampling

* For each accepted add-on:

  * Sampled non-selected items
* Converts problem into:
  👉 **Learning-to-Rank setup**

---

# 🧩 Feature Engineering

We designed features across **4 key dimensions**:

## 👤 User Features

* Price sensitivity
* Historical preferences
* Cuisine affinity

## 🛒 Cart Context

* Current cart value
* Number of items
* Item categories

## 🏪 Restaurant Features

* Cuisine type
* City tier
* Menu categories

## ⏱️ Contextual Signals

* Hour of day
* Weekend flag
* Meal time

---

# 🤖 Model Architecture

## 🔹 Core Model: LightGBM Ranker

* Objective: **LambdaRank**
* Handles tabular data efficiently
* Chosen for:

  * ⚡ Low latency
  * 📉 Low memory usage
  * 🧠 Strong ranking performance

---

## 🔹 (Extension) Sequential Modeling

To capture ordering behavior:

* LSTM-based session embeddings can be added
* Encodes:

  * item sequence
  * co-occurrence patterns

These embeddings can be fed into the ranker for improved contextual relevance.

---

# ⚙️ Training Setup

## 🔧 Hyperparameters

* n_estimators: 800
* learning_rate: 0.03
* num_leaves: 63
* subsample: 0.8
* colsample_bytree: 0.8

---

## 🧪 Training Strategy

* Grouped by **order_id (query groups)**
* Optimized using ranking loss
* Compared with popularity baseline

---

# 📈 Evaluation Metrics

| Metric                   | Value       |
| ------------------------ | ----------- |
| Validation AUC           | **0.813**   |
| Precision@5              | **0.252**   |
| Recall@5                 | **0.993**   |
| NDCG@5                   | **0.822**   |
| Acceptance Rate@5        | **0.252**   |
| Projected AOV Lift       | **+363.94** |
| Avg Category Diversity@5 | **2.09**    |

---

## 🔍 Key Insights

* Strong ranking quality (**NDCG@5 = 0.822**)
* Very high recall → captures almost all relevant items
* Significant improvement in:

  * ✅ Add-on acceptance
  * ✅ AOV
  * ✅ Cart completeness

---

# 💼 Business Impact

* 📈 **+363.8 AOV Lift**
* 🛒 Higher items per order
* 🍽️ More complete meals
* 🎯 Better user experience

---

# ⚡ Production Readiness

## 🚀 Latency

* **~0.178 ms per request**
* ~178 ms for 1000 predictions

✅ Meets **< 200–300 ms constraint**

---

## 🏗️ System Design

* Candidate filtering reduces search space
* Offline feature computation
* Stateless ranking architecture
* Scalable to millions of requests

---

# ✅ Pros & Cons

## ✔️ Pros

* Extremely low latency
* High business impact (AOV, acceptance rate)
* Context-aware recommendations
* Scalable and lightweight

---

## ❌ Cons

* Trained on simulated data
* Real-world noise not fully captured
* Cold-start limitations

---

# 🔮 Future Improvements

* Transformer-based models (SASRec, BERT4Rec)
* LLM-based semantic embeddings
* Real-time personalization
* A/B testing on live users
* Improved cold-start strategies

---

# 🏁 Conclusion

This project demonstrates a **production-ready recommendation system** that balances:

* ⚡ Speed (low latency)
* 🧠 Intelligence (context-aware ranking)
* 💰 Business impact (AOV optimization)

---


