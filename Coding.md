## **7. Updated Machine Learning Models for Multi-Output Classification**
import numpy as np
import pandas as pd
from sklearn.preprocessing import MinMaxScaler

# Sample data
```python
data = {
    'Area': ['Area 1', 'Area 2', 'Area 3'],
    'Employment': [0.8, 0.7, 1.0],  # Normalized Employment
    'Wages': [0.9, 0.6, 0.85],  # Normalized Wages
    'Employment_per_1k_jobs': [0.7, 0.8, 1.0],  # Normalized Employment per 1,000 Jobs
    'Location_Quotient': [1.2, 1.1, 1.3],  # Normalized Location Quotient
    'Job_Growth_Rate': [0.6, 0.8, 0.9]  # Normalized Job Growth Rate
}

# Convert the data into a pandas DataFrame
df = pd.DataFrame(data)

# Define weights (these can be adjusted)
weights = {
    'Employment': 0.20,
    'Wages': 0.30,
    'Employment_per_1k_jobs': 0.15,
    'Location_Quotient': 0.20,
    'Job_Growth_Rate': 0.15
}

# Normalize the data (assuming the data is not normalized yet)
scaler = MinMaxScaler()

# Normalize the relevant columns (excluding the 'Area' column)
columns_to_normalize = ['Employment', 'Wages', 'Employment_per_1k_jobs', 'Location_Quotient', 'Job_Growth_Rate']
df[columns_to_normalize] = scaler.fit_transform(df[columns_to_normalize])

# Calculate the Tech Friendly Index for each area using a weighted sum
df['Tech_Friendly_Index'] = (
    weights['Employment'] * df['Employment'] +
    weights['Wages'] * df['Wages'] +
    weights['Employment_per_1k_jobs'] * df['Employment_per_1k_jobs'] +
    weights['Location_Quotient'] * df['Location_Quotient'] +
    weights['Job_Growth_Rate'] * df['Job_Growth_Rate']
)

# Display the DataFrame with the calculated Tech Friendly Index
print(df[['Area', 'Tech_Friendly_Index']])
```

We will use a multi-output model strategy designed to classify cities based on two primary outputs: Tech Hub Classification and Affordability Classification.

###

```python
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
from sklearn.linear_model import LogisticRegression
from sklearn.tree import DecisionTreeClassifier
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import accuracy_score, precision_score, recall_score, f1_score, roc_auc_score, confusion_matrix

# Split data into training and test sets
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Standardize features
scaler = StandardScaler()
X_train = scaler.fit_transform(X_train)
X_test = scaler.transform(X_test)

# Logistic Regression Model
log_reg = LogisticRegression()
log_reg.fit(X_train, y_train)
y_pred_log = log_reg.predict(X_test)

# Decision Tree Model
dtree = DecisionTreeClassifier()
dtree.fit(X_train, y_train)
y_pred_tree = dtree.predict(X_test)

# Random Forest Model
rf = RandomForestClassifier()
rf.fit(X_train, y_train)
y_pred_rf = rf.predict(X_test)
```

---

## **8. Metrics to Measure Model Performance**

```python
# Evaluate model performance
models = {'Logistic Regression': y_pred_log, 'Decision Tree': y_pred_tree, 'Random Forest': y_pred_rf}

for model, y_pred in models.items():
    print(f"{model} Performance:")
    print("Accuracy:", accuracy_score(y_test, y_pred))
    print("Precision:", precision_score(y_test, y_pred))
    print("Recall:", recall_score(y_test, y_pred))
    print("F1 Score:", f1_score(y_test, y_pred))
    print("ROC-AUC:", roc_auc_score(y_test, y_pred))
    print("Confusion Matrix:\n", confusion_matrix(y_test, y_pred))
    print("\n" + "-"*50 + "\n")
```

---

## **9. How the Models and Metrics Guide Decision-Making**

By implementing machine learning models, we classify cities based on these two primary aspects—Tech Hub and Affordability—ensuring that new tech professionals have actionable insights when considering relocation decisions. The project integrates a technical approach with real-world impact, making it valuable for various stakeholders.


