# PHASE 3 PROJECT
---

## **1. Problem Definition**  

**Business Problem:**
***"Your company sees that many tech professionals are moving to cities with growing tech scenes, but the challenge is that these cities vary widely in terms of being financially comfortable. Your company wants to help new tech professionals make informed decisions about where to move for the best career opportunities in the tech industry while also considering whether the city is financially comfortable for them. However, they are unsure how to identify which cities offer the best combination of both tech growth and financial comfort."***

**Stakeholders:**
1. **Tech Professionals (Target Audience)**
- Why they're a stakeholder: They are the end-users who will benefit from identifying cities that balance career opportunities and financial comfort.
2. **City Governments and Municipalities**
- Why they're a stakeholder: They could use the insights from this project to attract tech talent to their cities by showcasing their strengths as tech hubs and their affordability.
3. **Tech Companies and Startups**
- Why they're a stakeholder: These companies may be looking to relocate or expand to cities with a strong pool of tech talent.
4. **Real Estate Developers and Agents**
- Why they're a stakeholder: They may use the insights to target cities with increasing tech workers and strong growth, ensuring that there are suitable housing options available for these professionals.
5. **Local Economists and Data Analysts**
- Why they're a stakeholder: These professionals will be involved in analyzing the data, creating reports, and forecasting trends based on the findings.
6. **Government Agencies Focused on Employment and Economic Development**
- Why they're a stakeholder: These entities may use the information to shape policies that encourage growth in tech sectors or incentivize companies to move to certain cities.

--- 
**Examples of Issues:**
- New York City may have a lot of opportunities for people who just stepped into tech, but people haven't been comfortable living financially there.
- Seattle may be a tech hub city, but its only been useful for people who already have high and senior level experience in tech.
- Cities in Iowa and Maine may be affordable, but it's nowhere near a tech hub.
---

**GOAL:** This project aims to help **new tech professionals** find cities that offer **strong career opportunities** in the tech sector while also being **financially sustainable**.  

---

## Project Route

Instead of treating this as a **single categorical classification**, we will **split the target into two separate but related binary classifications**:  
1. **Tech Hub Classification (Binary Output: Yes/No)** → Does the city have a growing tech scene?  
2. **Affordability Classification (Binary Output: Yes/No)** → Is the city affordable for an entry-level tech worker?  

This means that the model will predict **two outputs per city**:  
- **Tech Hub?** ✅ Yes / ❌ No  
- **Affordable?** ✅ Yes / ❌ No  

These classifications will help categorize cities into **one of four possible groups**:  
1. **Tech-Friendly & Affordable** (✅ Tech Hub, ✅ Affordable)  
2. **Tech-Friendly but Expensive** (✅ Tech Hub, ❌ Not Affordable)  
3. **Affordable but Not Tech-Friendly** (❌ Not a Tech Hub, ✅ Affordable)  
4. **Not Suitable** (❌ Not a Tech Hub, ❌ Not Affordable)  

By **splitting this into two outputs**, we make it possible to analyze and improve predictions independently for **both Tech Growth and Affordability** while still allowing for a final classification into the four groups.  

---

## **2. Features (Input Variables)**  

To classify cities based on both **tech growth** and **financial comfort**, we will include the following input features:  

Since this is a lot of datasets and we want to narrow these factors down, each factor we will form into an Index

### **A. Urbanization Factors**  
- **Population Density**: Higher densities indicate urban environments.  
- **Urbanization Growth Rate**: Measures how quickly a city is expanding in terms of population.  

### **B. Tech Hub Factors**  
- **Number of Tech Companies**: Startups + large tech firms in the city.  
- **Tech Job Growth Rate**: Increase in tech-related jobs over time.  
- **Average Entry-Level Tech Salaries**: Indicates how lucrative the tech sector is for new professionals.  
- **Venture Capital Investment**: Amount of VC funding going into startups in the city.  
- **Tech Conferences & Meetups**: Measures how active the local tech community is.  
- **Tech Talent Pool**: Number of tech graduates and professionals available for hiring.  

### **C. Financial & Affordability Factors**  
- **Cost of Living Index**: Measures overall expenses, including rent, food, and utilities.  
- **Entry-Level Salary in Tech**: Used to determine purchasing power.  
- **Income-to-Housing Ratio**: Compares income with average housing costs.  
- **Income-to-Tax Ratio**: Measures tax burden on entry-level salaries.  
- **Rent & Housing Market Conditions**: Analyzes affordability of real estate for young professionals.  

---

## **3. Target (Output Variables - Multi-Output Classification)**  

The goal is **not to classify cities into just one label**, but instead to use **two binary classifications**:  

1. **Tech Hub Classification (Y1)**  
   - ✅ Yes → The city is considered a growing tech hub.  
   - ❌ No → The city does not have a strong tech sector.  

2. **Affordability Classification (Y2)**  
   - ✅ Yes → The city is financially suitable for entry-level tech professionals.  
   - ❌ No → The city is unaffordable.  

These two outputs together define one of the four final city categories:  
| Tech Hub? | Affordable? | Final Classification |
|-----------|------------|----------------------|
| ✅ Yes | ✅ Yes | **Tech-Friendly & Affordable** |
| ✅ Yes | ❌ No | **Tech-Friendly but Expensive** |
| ❌ No | ✅ Yes | **Affordable but Not Tech-Friendly** |
| ❌ No | ❌ No | **Not Suitable** |

Since there are **two independent but related targets**, we must use a **MultiOutputClassifier**, which allows us to train one model for **both outputs simultaneously**.  

---

## **4. Machine Learning Models for Multi-Output Classification**  

Since we are predicting **two related but independent outputs**, we need a **Multi-Output Classification Model**.  

### **1. Logistic Regression (Baseline Model)**
- Simple, interpretable, works well for **linearly separable** data.  
- Regularization with **Ridge (L2)** or **Lasso (L1)** can improve generalization.  

```python
from sklearn.linear_model import LogisticRegression
from sklearn.multioutput import MultiOutputClassifier

# Base classifier
logistic = LogisticRegression()
multi_logistic = MultiOutputClassifier(logistic)

multi_logistic.fit(X_train, [y_tech_hub, y_affordability])
```

---

### **2. Decision Tree Classifier**
- Works well with **non-linear** data.  
- Easy to interpret using **feature importance**.  
- Prone to **overfitting** unless depth is controlled.  

```python
from sklearn.tree import DecisionTreeClassifier

# Base classifier
tree = DecisionTreeClassifier(max_depth=5)
multi_tree = MultiOutputClassifier(tree)

multi_tree.fit(X_train, [y_tech_hub, y_affordability])
```

---

### **3. Random Forest Classifier (Best for Accuracy & Stability)**
- **Ensemble method** → Reduces overfitting of individual decision trees.  
- Handles **both linear & non-linear relationships** well.  
- Computes **feature importance**, helping us identify key factors.  

```python
from sklearn.ensemble import RandomForestClassifier

# Base classifier
random_forest = RandomForestClassifier(n_estimators=100, max_depth=10)
multi_rf = MultiOutputClassifier(random_forest)

multi_rf.fit(X_train, [y_tech_hub, y_affordability])
```

---

## **5. Model Evaluation & Metrics**  

Since this is a **Multi-Output Classification** problem, we evaluate the model using metrics for **each target separately** and also combined:  

1. **Accuracy (Overall & Per Output)**  
2. **Precision, Recall, and F1-Score** for each output (Tech Hub, Affordability)  
3. **Confusion Matrix** for each output  
4. **Feature Importance** (For Decision Tree & Random Forest)  

Example: Evaluating accuracy for both outputs separately  
```python
from sklearn.metrics import accuracy_score

# Predictions
y_pred = multi_rf.predict(X_test)

# Evaluate each target separately
tech_hub_accuracy = accuracy_score(y_test_tech_hub, y_pred[:, 0])
affordability_accuracy = accuracy_score(y_test_affordability, y_pred[:, 1])

print(f"Tech Hub Classification Accuracy: {tech_hub_accuracy:.2f}")
print(f"Affordability Classification Accuracy: {affordability_accuracy:.2f}")
```

---

## **6. Full Pipeline for Training & Deployment**  

1. **Data Collection & Cleaning**  
   - Gather city data (tech industry stats, financial conditions).  
   - Handle missing values using imputation.  
   - Normalize numerical values (Min-Max Scaling).  

2. **Feature Engineering**  
   - Create new meaningful ratios (e.g., **Income-to-Rent Ratio**).  
   - One-Hot Encode categorical variables (city names, states).  

3. **Model Training**  
   - Split the dataset into training/testing (80/20).  
   - Train multiple models (Logistic, Decision Tree, Random Forest).  

4. **Hyperparameter Tuning**  
   - Optimize **Random Forest (depth, n_estimators, max_features)**.  

5. **Evaluation & Deployment**  
   - Choose **best model** based on test accuracy.  
   - Convert model to API (Flask/FastAPI).  
   - Build interactive dashboard (Streamlit/Tableau).  

---

## **Final Model Choice**
| Model | Handles Multi-Output? | Works with Non-Linear Data? | Best for Large Datasets? |
|------------|-------------------|----------------------|-------------------|
| **Logistic Regression** | ✅ Yes | ❌ No | ✅ Yes |
| **Decision Tree** | ✅ Yes | ✅ Yes | ❌ No |
| **Random Forest** | ✅ Yes | ✅ Yes | ✅ Yes |

---
### **Project Summary:**

This project aims to classify cities based on **two key factors**:  
1. **Tech Hub Classification** (Is the city a growing tech hub?)
2. **Affordability Classification** (Is the city affordable for entry-level tech workers?)

The approach involves:
- **Data Collection**: Gathering information about cities' tech growth and financial conditions, including population density, tech job growth, cost of living, and more.
- **Feature Engineering**: Creating new features like income-to-rent ratios, and scaling/encoding variables for better model performance.
- **Modeling**: Using **MultiOutputClassifier** with models like **Logistic Regression**, **Decision Tree**, and **Random Forest** to predict both tech growth and affordability.
- **Evaluation**: Assessing model performance with metrics like **accuracy**, **precision**, and **recall** for each target (Tech Hub & Affordability), plus feature importance for insights.

### **Key Techniques & Tools**:
- **Machine Learning Models**: Logistic Regression, Decision Tree, Random Forest.
- **Evaluation Metrics**: Accuracy, Precision, Recall, F1-Score.
- **Tools**: Python, Scikit-learn, MultiOutputClassifier, Data Preprocessing, Feature Engineering.

The final goal is to categorize cities into one of four groups:  
- **Tech-Friendly & Affordable**  
- **Tech-Friendly but Expensive**  
- **Affordable but Not Tech-Friendly**  
- **Not Suitable**  

This classification will help tech professionals make informed decisions about relocating to cities that align with their career goals and financial situation.

