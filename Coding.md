## **7. Updated Machine Learning Models for Multi-Output Classification**

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


