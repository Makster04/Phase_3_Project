```python
iimport pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import LabelEncoder
from sklearn.linear_model import LogisticRegression
from sklearn.tree import DecisionTreeClassifier
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import classification_report

# Step 1: Load data
df = pd.read_csv('Final_Data.csv')

# Step 2: Preprocess data (you can adjust as needed)
# Handling missing values, if any (for simplicity, let's drop rows with missing values)
df = df.dropna(subset=['Financial_Comfort_Index', 'Tech_Friendly_Index'])

# Step 3: Define the thresholds (example thresholds, adjust as needed)
tech_threshold = 9500  # Adjusted Tech-Friendly threshold (based on your data analysis)
finance_threshold = 35000  # Adjusted Financial Comfort threshold (based on your data analysis)

# Step 4: Classify Tech Hub and Affordable columns based on thresholds
df['Tech Hub?'] = df['Tech_Friendly_Index'].apply(lambda x: 1 if x > tech_threshold else 0)
df['Affordable?'] = df['Financial_Comfort_Index'].apply(lambda x: 1 if x > finance_threshold else 0)

# Step 5: Define the Final Classification based on the combination of Tech Hub and Affordable
def final_classification(row):
    if row['Tech Hub?'] == 1 and row['Affordable?'] == 1:
        return "Tech-Friendly & Affordable"
    elif row['Tech Hub?'] == 1 and row['Affordable?'] == 0:
        return "Tech-Friendly but Expensive"
    elif row['Tech Hub?'] == 0 and row['Affordable?'] == 1:
        return "Affordable but Not Tech-Friendly"
    else:
        return "Not Suitable"

df['Final Classification'] = df.apply(final_classification, axis=1)

# Step 6: Check the distribution of the 'Final Classification' before encoding
print("Final Classification Distribution:")
print(df['Final Classification'].value_counts())

# Ensure there are at least two classes for classification
if len(df['Final Classification'].value_counts()) < 2:
    print("Error: Not enough classes in the target variable for classification.")
else:
    # Step 7: Encode the 'Final Classification' for machine learning models
    label_encoder = LabelEncoder()
    df['Final Classification Encoded'] = label_encoder.fit_transform(df['Final Classification'])

    # Step 8: Prepare features and target variables
    X = df[['Tech_Friendly_Index', 'Financial_Comfort_Index']]  # Features
    y = df['Final Classification Encoded']  # Target

    # Step 9: Split the data into training and testing sets
    X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42, stratify=y)

    # Step 10: Train the Logistic Regression Model
    logreg = LogisticRegression(max_iter=10000)  # max_iter increased for convergence
    logreg.fit(X_train, y_train)

    # Step 11: Make predictions and evaluate the model
    logreg_predictions = logreg.predict(X_test)

    # Print classification report for Logistic Regression
    print("Logistic Regression Classification Report:")
    print(classification_report(y_test, logreg_predictions))

    # Step 12: Optionally train other models (Decision Tree and Random Forest)
    # Decision Tree Classifier
    dt_classifier = DecisionTreeClassifier(random_state=42)
    dt_classifier.fit(X_train, y_train)
    dt_predictions = dt_classifier.predict(X_test)
    print("Decision Tree Classification Report:")
    print(classification_report(y_test, dt_predictions))

    # Random Forest Classifier
    rf_classifier = RandomForestClassifier(random_state=42)
    rf_classifier.fit(X_train, y_train)
    rf_predictions = rf_classifier.predict(X_test)
    print("Random Forest Classification Report:")
    print(classification_report(y_test, rf_predictions))

```

