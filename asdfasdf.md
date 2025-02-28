
# Phase 3 Project
---

### 1. **Problem Definition (Revised)**  
**Business Problem:**  
Your company observes that tech professionals, especially those entering the industry, are moving to cities with growing tech scenes. However, while these cities may have a burgeoning tech industry, the question remains: Do these cities offer accessible job opportunities for entry-level tech professionals? Your company wants to help new tech professionals identify cities that not only have a growing tech sector but also provide ample opportunities for first-entry tech talent, ensuring both career potential and financial comfort.

---

### 2. **Stakeholders:**

- **Tech Professionals (Target Audience)**  
  **Why they're a stakeholder:** They are the end-users who will benefit from identifying cities that offer career opportunities and accessibility for entry-level roles in the tech industry.
  
- **Tech Companies and Startups**  
  **Why they're a stakeholder:** Companies may be looking to expand or relocate to cities with a growing tech sector and accessible entry-level talent.
  
- **City Governments and Municipalities**  
  **Why they're a stakeholder:** Governments may want to attract and retain young tech talent to their cities by showcasing their affordability and potential for growth.
  
- **Real Estate Developers and Agents**  
  **Why they're a stakeholder:** Real estate agents and developers need to anticipate demand for housing from incoming tech professionals.
  
- **Local Economists and Data Analysts**  
  **Why they're a stakeholder:** They will analyze trends to help guide economic development policies or reports on job growth and affordability.
  
- **Government Agencies Focused on Employment and Economic Development**  
  **Why they're a stakeholder:** These agencies can use the insights to encourage the growth of entry-level job opportunities in cities with burgeoning tech sectors.

---

### 3. **Revised Goal:**  
The goal is to help new tech professionals find cities that offer strong career opportunities in the tech sector with ample opportunities for first-entry tech roles while also being financially sustainable.

---

### 4. **Project Route (Updated Approach)**

#### A. **Tech Hub Classification (Updated):**  
**New Focus:** Instead of just considering a city as a "growing tech hub," we’ll focus on whether the city provides specific opportunities for entry-level tech professionals. This includes factors like the volume of entry-level jobs, internship opportunities, training programs, and entry-level salary ranges.

- **Tech Hub Classification (Binary Output):**  
  - ✅ Yes: The city has a growing tech sector and offers ample opportunities for entry-level tech professionals.  
  - ❌ No: The city is not growing or does not offer sufficient opportunities for first-entry tech workers.

**Criteria for Tech Hub (Updated):**  
- **Number of Entry-Level Tech Jobs:** The volume of jobs specifically for entry-level tech professionals, such as junior developer roles, IT support, data analysts, etc.  
- **Availability of Tech Training Programs:** The presence of local boot camps, tech meetups, internships, and programs aimed at first-entry professionals.  
- **Entry-Level Salary Levels:** Cities offering competitive salaries for entry-level tech professionals while adjusting for cost of living.  
- **Employer Focus on Hiring Juniors:** Percentage of tech companies in the city specifically hiring junior tech talent and supporting early career professionals.

---

#### B. **Updated Features (Input Variables)**

**A. Urbanization Factors**  
- **Population Density**  
- **Urbanization Growth Rate**

**B. Tech Hub Factors (With Updated Focus on Entry-Level Opportunities)**  
- **Number of Entry-Level Tech Jobs and Growth Rate:** Focus on junior, intern, and trainee roles within the tech sector.  
- **Entry-Level Salary Levels:** The average salary for junior roles in tech.  
- **Tech Job Market Accessibility:** Metrics on how easy it is for first-entry workers to find jobs (based on job postings and hiring rates).  
- **Tech Employer Focus on Juniors:** Percentage of tech companies that explicitly seek junior talent, provide entry-level career growth, and focus on upskilling.  
- **Number of Tech Companies:** Startups + large tech firms in the city.  
- **Venture Capital Investment:** Amount of VC funding going into startups in the city.  
- **Tech Conferences & Meetups:** Measures how active the local tech community is.  
- **Tech Talent Pool:** Number of tech graduates and professionals available for hiring.

**C. Financial & Affordability Factors**  
- **Cost of Living Index**  
- **Entry-Level Salary in Tech**  
- **Income-to-Housing Ratio**  
- **Income-to-Tax Ratio**  
- **Rent & Housing Market Conditions**

---

### 5. **Updated Target (Output Variables)**

- **Tech Hub Classification (Y1)**  
  - ✅ Yes → The city offers growing tech job opportunities and resources for entry-level professionals.  
  - ❌ No → The city does not offer sufficient opportunities for new tech talent.

- **Affordability Classification (Y2)**  
  - ✅ Yes → The city is financially suitable for entry-level tech professionals.  
  - ❌ No → The city is unaffordable for an entry-level professional in the tech sector.

---

### 6. **Updated Machine Learning Models for Multi-Output Classification**

We will use the same multi-output model strategy, with models designed to classify cities based on two primary outputs: **Tech Hub Classification** and **Affordability Classification**.

- **Logistic Regression:**  
  - Will predict both **Tech Hub Classification** and **Affordability Classification** based on the newly adjusted features.

- **Decision Tree Classifier:**  
  - Will focus on predicting whether a city offers entry-level opportunities and affordability, based on non-linear relationships in the data.

- **Random Forest Classifier:**  
  - Will continue to be the preferred choice for accuracy and stability, especially in classifying cities into the four final categories.

---

### 7. **Final Classification (Updated)**

| **Tech Hub?** | **Affordable?** | **Final Classification** |  
|---------------|-----------------|--------------------------|  
| ✅ Yes        | ✅ Yes          | Tech-Friendly & Affordable |  
| ✅ Yes        | ❌ No           | Tech-Friendly but Expensive |  
| ❌ No         | ✅ Yes          | Affordable but Not Tech-Friendly |  
| ❌ No         | ❌ No           | Not Suitable              |

---

### 8. **Metrics to Measure Model Performance**

For each classification and model, we will measure the following metrics to evaluate performance:

- **Accuracy:** The overall percentage of correct classifications.  
- **Precision:** How many of the predicted positive classifications (Tech Hub or Affordable) were actually correct.  
- **Recall (Sensitivity):** How many of the true positive classifications were identified by the model.  
- **F1 Score:** The balance between precision and recall, ensuring that the model is not biased toward one metric.  
- **ROC-AUC:** Area under the ROC curve, which helps evaluate the performance of classification models at various thresholds.  
- **Confusion Matrix:** To visually inspect the true positives, false positives, true negatives, and false negatives.

---

### 9. **How the Models and Metrics Guide Decision-Making**

#### **Using the Models:**  
- **Tech Hub Classification Model:** This model helps determine whether a city is a viable option for entry-level tech professionals based on specific job opportunities and resources. It uses input factors such as entry-level job availability, salaries, and employer interest in hiring junior talent to identify whether a city is considered a "Tech Hub" for entry-level professionals.
  
- **Affordability Classification Model:** This model predicts if a city is affordable for entry-level tech workers, considering factors like the cost of living, housing market conditions, and salary-to-housing ratios. This guides decision-making by ensuring cities are not only good for career growth but also financially sustainable for newcomers to the tech industry.

#### **Using the Metrics:**  
- **Accuracy:** Ensures that the classification models are making reliable predictions. A high accuracy score means that the model is accurately classifying cities into "Tech Hub" and "Affordability" categories.
  
- **Precision and Recall:** These metrics will guide optimization efforts. For example, if precision is low for affordability, we may need to refine the financial features to ensure more accurate classification of affordable cities.
  
- **F1 Score:** By balancing precision and recall, the F1 score ensures that we don’t sacrifice one at the expense of the other, providing a well-rounded view of model performance.
  
- **ROC-AUC:** This helps evaluate the model's ability to discriminate between the two classes (Tech Hub vs. Non-Tech Hub and Affordable vs. Not Affordable) at different thresholds. A higher AUC means that the model is better at distinguishing between the different categories.

#### **Final Decision-Making:**  
The ultimate decision-making will be driven by these two classification outputs. The models will offer a clear breakdown of which cities are both tech-friendly and affordable, helping users (entry-level tech professionals) make informed relocation decisions based on career prospects and financial feasibility. 

---

### 10. **Summary of the Updated Model Approach:**

This project now centers on helping first-entry tech professionals by focusing on cities that offer both growing tech job opportunities and affordability. The **Tech Hub Classification** emphasizes entry-level job availability, training programs, and employer focus on juniors. The **Affordability Classification** ensures that these cities are financially accessible, evaluating cost of living, salaries, and housing affordability.

The models used will focus on classifying cities based on these two primary aspects—**Tech Hub** and **Affordability**—ensuring that new tech professionals have actionable insights when considering relocation decisions. The metrics will guide both model optimization and the interpretation of results for stakeholders.

---

This structure integrates both the technical approach with machine learning models and the real-world impact of these decisions on new tech professionals, ensuring that the project is both actionable and beneficial to the target audience.
