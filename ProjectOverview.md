# **Project Proposal: Identifying Tech-Friendly and Affordable Cities for Entry-Level Tech Professionals**

## **1. Problem Definition (Revised)**

### **Business Problem:**

Your company observes that tech professionals, especially those entering the industry, are moving to cities with growing tech scenes. However, while these cities may have a burgeoning tech industry, the question remains: Do these areas offer accessible job opportunities for entry-level tech professionals? Your company aims to help new tech professionals identify cities that not only have a growing tech sector but also provide ample opportunities for first-entry tech talent, ensuring both career potential and financial comfort while matching their preferred living environment.

---

## **2. Stakeholders**

### **Primary Stakeholders:**

- **Tech Professionals (Target Audience)**
  - They are the end-users who benefit from identifying cities that offer career opportunities and accessibility for entry-level roles in the tech industry.
- **Tech Companies and Startups**
  - Companies looking to expand or relocate to cities with a growing tech sector and accessible entry-level talent.
- **City Governments and Municipalities**
  - Governments aiming to attract and retain young tech talent by showcasing their affordability and potential for growth.

### **Secondary Stakeholders:**

- **Real Estate Developers and Agents**
  - Anticipate demand for housing from incoming tech professionals.
- **Local Economists and Data Analysts**
  - Analyze trends to help guide economic development policies related to job growth and affordability.
- **Government Agencies Focused on Employment and Economic Development**
  - Utilize insights to encourage the growth of entry-level job opportunities in cities with burgeoning tech sectors.

---

## **3. Revised Goal**

The goal is to help new tech professionals find cities that offer strong career opportunities in the tech sector with ample opportunities for first-entry tech roles while also being financially sustainable.

---

## **4. Project Route (Updated Approach)**

### **A. Tech Hub Classification (Updated)**

Instead of just considering a city as a "growing tech hub," we focus on whether it provides specific opportunities for entry-level tech professionals. This includes:

- Volume of entry-level jobs
- Internship opportunities
- Training programs
- Entry-level salary ranges

#### **Tech Hub Classification (Binary Output):**

✅ Yes: The city has a growing tech sector and offers ample opportunities for entry-level tech professionals.\
❌ No: The city is not growing or does not offer sufficient opportunities for first-entry tech workers.

#### **Criteria for Tech Hub (Updated):**

- **Number of Entry-Level Tech Jobs:** The volume of jobs specifically for entry-level tech professionals, such as junior developers, IT support, and data analysts.
- **Entry-Level Salary Levels:** Competitive salaries adjusted for the cost of living.
- **Employer Focus on Hiring Juniors:** Percentage of tech companies hiring junior talent and supporting early career professionals.

---

## **5. Updated Features (Input Variables)**



### **B. Tech Hub Factors (With Updated Focus on Entry-Level Opportunities)**
Already made:
https://www.comptia.org/content/research/best-tech-cities-it-jobs 
https://www.cloudwards.net/top-tech-cities-us/#ranking-100-u-s-cities-for-tech-professionals

Data based on Numbers
https://www.numbeo.com/cost-of-living/
https://0sbs.com/map-of-us-tech-cities/
https://comptiacdn.azureedge.net/webcontent/docs/default-source/research-reports/comptia-state-of-the-tech-workforce-2024.pdf?sfvrsn=a8aa5246_2

- **Location Quotient Rank (no. IT job ads):** Reflects the concentration of IT job ads in a city, showing how strong the local tech job market is relative to other cities.
- **#IT Job Ads Rank:** This directly ties into the number of available IT job ads, indicating the size of the tech job market, especially relevant to entry-level professionals.
- **1-year % Job Growth Rank:** Shows short-term growth in tech job opportunities, highlighting cities with rapid expansion in entry-level tech jobs.
- **5-year % Job Growth Rank:** Provides long-term trends in job growth, helping predict sustained job opportunities in tech for entry-level professionals over the next several years.


### **C. Financial & Affordability Factors**
- **Cost of Living Index Rank:** Measures the cost of living in different cities, helping to evaluate whether they are financially feasible for entry-level tech professionals.
- **Cost of Living Adjusted Median Hourly Earnings Rank:** Combines salary levels with cost of living to assess the financial attractiveness of a city for entry-level tech professionals, showing whether salaries are competitive after adjusting for living costs.

---

## **6. Updated Target (Output Variables)**

### **Tech Hub Classification (Y1)**

✅ Yes → The city offers growing tech job opportunities and resources for entry-level professionals.\
❌ No → The city does not offer sufficient opportunities for new tech talent.

### **Affordability Classification (Y2)**

✅ Yes → The city is financially suitable for entry-level tech professionals.\
❌ No → The city is unaffordable for an entry-level professional in the tech sector.

---

## **7. Updated Machine Learning Models for Multi-Output Classification**

We will use a multi-output model strategy designed to classify cities based on two primary outputs: Tech Hub Classification and Affordability Classification.


### **Algorithms Used:**
- **Logistic Regression:** Predicts both Tech Hub Classification and Affordability Classification based on newly adjusted features.
- **Decision Tree Classifier:** Predicts whether a metropolitan area offers entry-level opportunities and affordability, considering non-linear relationships in the data.
- **Random Forest Classifier:** Preferred choice for accuracy and stability, especially in classifying metropolitan areas into the four final categories.

---

## **8. Final Classification (Updated)**
| Tech Hub? | Affordable? | Final Classification |
|-----------|------------|----------------------|
| ✅ Yes    | ✅ Yes     | Tech-Friendly & Affordable |
| ✅ Yes    | ❌ No      | Tech-Friendly but Expensive |
| ❌ No     | ✅ Yes     | Affordable but Not Tech-Friendly |
| ❌ No     | ❌ No      | Not Suitable |

---

## **9. Metrics to Measure Model Performance**
For each classification and model, we will evaluate the following:
- **Accuracy:** Measures the overall percentage of correct classifications.
- **Precision:** Measures how many predicted positive classifications were actually correct.
- **Recall (Sensitivity):** Measures how many true positive classifications were identified.
- **F1 Score:** Balances precision and recall.
- **ROC-AUC:** Evaluates the model's ability to distinguish between categories.
- **Confusion Matrix:** Provides insights into prediction errors.

---

## **10. How the Models and Metrics Guide Decision-Making**

### **Using the Models:**
- **Tech Hub Classification Model:** Identifies viable metropolitan areas for entry-level tech professionals.
- **Affordability Classification Model:** Ensures metropolitan areas are financially sustainable for new tech professionals.

### **Using the Metrics:**
- **Accuracy:** Ensures reliability.
- **Precision & Recall:** Optimize financial feature selection.
- **F1 Score:** Maintains balanced performance.
- **ROC-AUC:** Evaluates model effectiveness.
- **Confusion Matrix:** Identifies misclassifications.

---

## **11. Summary of the Updated Model Approach**
This project centers on helping first-entry tech professionals by focusing on cities that offer both growing tech job opportunities and affordability. The **Tech Hub Classification** emphasizes entry-level job availability, training programs, and employer focus on juniors, while the **Affordability Classification** ensures these metropolitan areas are financially accessible. 

By implementing machine learning models, we classify cities based on these two primary aspects—Tech Hub and Affordability—ensuring that new tech professionals have actionable insights when considering relocation decisions. The project integrates a technical approach with real-world impact, making it valuable for various stakeholders.

