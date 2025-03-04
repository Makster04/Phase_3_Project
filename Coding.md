```python
import pandas as pd
import numpy as np
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
from sklearn.linear_model import LogisticRegression
from sklearn.tree import DecisionTreeClassifier
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import accuracy_score, precision_score, recall_score, f1_score, roc_auc_score, confusion_matrix

# Load datasets
tech_data = pd.read_excel("Tech_Hub_Data.xlsx")
affordability_data = pd.read_excel("Affordability_Data.xlsx")

# Merge datasets on 'Area_Name'
df = pd.merge(tech_data, affordability_data, on='Area_Name', how='inner')

# Define features (X) and targets (Y1: Tech Hub, Y2: Affordability)
X = df.drop(columns=['Area_Name', 'Tech_Hub', 'Affordable'])
Y1 = df['Tech_Hub']  # Binary classification (Yes/No)
Y2 = df['Affordable']  # Binary classification (Yes/No)

# Standardize the features
scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)

# Split data into training and testing sets
X_train, X_test, Y1_train, Y1_test = train_test_split(X_scaled, Y1, test_size=0.2, random_state=42)
X_train, X_test, Y2_train, Y2_test = train_test_split(X_scaled, Y2, test_size=0.2, random_state=42)

# Logistic Regression
log_reg = LogisticRegression()
log_reg.fit(X_train, Y1_train)
Y1_pred_log = log_reg.predict(X_test)

# Decision Tree Classifier
decision_tree = DecisionTreeClassifier()
decision_tree.fit(X_train, Y1_train)
Y1_pred_tree = decision_tree.predict(X_test)

# Random Forest Classifier
random_forest = RandomForestClassifier(n_estimators=100, random_state=42)
random_forest.fit(X_train, Y1_train)
Y1_pred_forest = random_forest.predict(X_test)

# Evaluate models
def evaluate_model(y_true, y_pred, model_name):
    print(f"{model_name} Performance:")
    print(f"Accuracy: {accuracy_score(y_true, y_pred):.4f}")
    print(f"Precision: {precision_score(y_true, y_pred, pos_label='Yes'):.4f}")
    print(f"Recall: {recall_score(y_true, y_pred, pos_label='Yes'):.4f}")
    print(f"F1 Score: {f1_score(y_true, y_pred, pos_label='Yes'):.4f}")
    print(f"Confusion Matrix:\n{confusion_matrix(y_true, y_pred)}")
    print("----------------------------\n")

# Evaluate Tech Hub Classification Models
evaluate_model(Y1_test, Y1_pred_log, "Logistic Regression")
evaluate_model(Y1_test, Y1_pred_tree, "Decision Tree")
evaluate_model(Y1_test, Y1_pred_forest, "Random Forest")

# Repeat evaluation for Affordability Classification
evaluate_model(Y2_test, log_reg.predict(X_test), "Logistic Regression (Affordability)")
evaluate_model(Y2_test, decision_tree.predict(X_test), "Decision Tree (Affordability)")
evaluate_model(Y2_test, random_forest.predict(X_test), "Random Forest (Affordability)")
```

