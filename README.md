# Emerging Tech Cities

## Overview
### Business and Data Understanding

#### Business Problem
Many entry-level tech professionals and startup groups are relocating to cities with growing tech industries, but job opportunities and financial sustainability remain major concerns.

#### Primary Stakeholders
- **Tech Professionals:** Seeking financially sustainable and career-friendly cities.
- **Tech Startups:** Evaluating locations with robust tech growth potential and manageable costs.

#### Objective
Develop classification models to identify cities that:
- Have strong and growing tech sectors.
- Offer ample entry-level job opportunities.
- Provide financial sustainability considering entry-level salaries and cost of living.

#### Data Understanding
Two primary indices were developed using multiple datasets:

- **Tech-Friendliness Index:**
  - Employment per 1,000 jobs (weighted at 25%)
  - Entry-level job availability (25%)
  - Layoffs per capita (10%)
  - Tech events and innovation ecosystem metrics (25%)
  - Average seven-year growth rate

- **Financial Comfort Index:**
  - Calculated by Entry Level Tech Wages divided by the sum of Cost of Living Index (multiplied by 100) and state taxes.

#### Target Variable
Classification variable representing cities categorized into five groups based on tech-friendliness and financial comfort:
- Mid Tech Friendly, Highly Financially Sustainable
- Highly Tech Friendly, Financially Challenging
- Low Tech Friendly, Financially Sustainable
- High Tech Friendly, Low Financial Comfort
- Other various combinations

**Challenges:**
- Missing values
- Imbalanced class distributions
- Inconsistent data across sources

## Modeling
Two key models identified for stakeholders:

### Decision Tree Model (for Tech Professionals)
- **Accuracy:** 0.9091
- Best suited to identifying financially manageable, tech-friendly cities.
- Strong recall and precision performance.

**Limitations:**
- Potential overfitting
- Limited dataset size
- Class imbalance

### Extra Trees Classifier (for Tech Startups)
- **Accuracy:** 0.9091
- Consistent performance with higher average precision (0.95).
- Ideal for identifying cities balancing tech potential and cost sustainability.

**Limitations:**
- Potential overfitting
- Limited dataset size
- Class imbalance

## Evaluation
Evaluations considered:
- Accuracy, precision, recall
- Consistent performance across multiple city categories

## Addressing Limitations

### Small Dataset
- Expand dataset via additional sources or synthetic data.
- Use advanced techniques to generalize model performance.

### Overfitting
- Implement regularization techniques (e.g., L2 regularization)
- Use pruning and ensemble methods (bagging, boosting)

### Class Imbalance
- Apply alternative evaluation metrics like F1-score and weighted precision/recall
- Use techniques like oversampling or undersampling

## Conclusion
The Decision Tree model effectively aids tech professionals in identifying optimal cities, while the Extra Trees Classifier provides robust recommendations for tech startups, ensuring both tech potential and economic viability. Further refinement with additional data and regularization techniques will enhance generalizability and accuracy.



