# Jabes_Phase_3_Project
This README contains the summerised details of Phase 3 project
# **<u>Project Title**
## **Dialing into Retention -**  ***Predicting Customer Churn at SyriaTel Using Machine Learning***

# Project Objective
This project aims to support SyriaTel, a leading telecommunications provider, in proactively reducing customer churn through predictive modeling. Churn remains a critical concern for the company, as each lost customer directly impacts recurring revenue and increases acquisition costs. By identifying which customers are at high risk of leaving, SyriaTel can target interventions more effectively, strengthen customer loyalty, and optimize resource allocation.

# **1. Understanding the Business Context**
### **<u>1.1. Brief Description of the Business**
SyriaTel currently lacks an efficient, data-driven method to anticipate customer churn. The existing approach is largely reactive, identifying churn only after it occurs—when it’s too late to intervene. 
The key business question this project seeks to answer is:
Can customer behavior and service usage patterns be used to accurately predict churn, enabling proactive engagement to retain at-risk customers?
Solving this problem will allow SyriaTel to shift from a reactive retention strategy to a proactive one, using predictive analytics to improve customer satisfaction, reduce revenue loss, and enhance operational efficiency.

### **<u>1.2. Stakeholders and Business Value**<u>
The primary stakeholders for this initiative are the **Customer Retention** and **Marketing teams**, who are directly responsible for minimizing churn and maximizing customer lifetime value. Secondary stakeholders include the **Call Center Operations team**, which handles customer grievances and service experiences, **Product Managers** designing service packages, and **Executive Leadership,** who require strategic insights to drive business performance. Each of these teams will benefit from the model’s ability to guide data-driven decisions and improve customer engagement strategies.

### **<u>1.3. The Business Question**
### 1.3.1 Key Business Question
The main business question that this project aim to address is:

- Can SyriaTel identify patterns in customer behavior and service usage that reliably predict churn, enabling proactive retention strategies?

### 1.3.2 The Specific Business Questions
1.	Which customers are most likely to churn?
2.	What are the main drivers of customer churn?
3.	How accurate is our churn prediction model?
4.	How can SyriaTel use these predictions to retain customers?
5.	What trade-offs exist between model complexity and interpretability?


### **<u>1.4 A Brief Description of the Chosen Dataset**
This project addresses customer churn prediction using the representative public Telco Customer Churn dataset (bigml_59c28831336c6604c800002a.csv;- applied as bigml_59) This dataset contains 3,333 customer records, each with 21 features covering demographics, account tenure, service usage, billing, and customer interactions. The target variable is binary churn status. Despite not being SyriaTel-specific, the dataset's structure mirrors typical telecom data, making it a relevant foundation for developing predictive models.

By analyzing this dataset with classification algorithms, the project aims to identify early indicators of customer churn. This process provides a potential blueprint for a predictive system that SyriaTel could adapt for its internal data. The dataset's realistic structure allows for the development of a practical solution for proactively managing customer attrition within a telecom context.

### **<u>1.5 The Project Approach Taken**
Step 1: Defining the Business Context and Problem.
 
Step 2: Data Exploration and Understanding
 
Step 3: Data Cleaning and Preprocessing
 
Step 4: Feature Selection and Engineering
 
Step 5: Model Building
 
Step 6: Model Evaluation
 
Step 7: Interpretation and Insights
 
Step 8: Recommendations and Next Steps

# **2. Data Exploration and Understanding**
The DataFrame we are working with contains a "churn" column, which is our target variable for prediction it has 3333 non-missing boolean values.
The DataFrame also includes other columns with different data types ie  8 floating-point numbers, 8 integers, and 4 objects

Preliminary check of the dataset reveals that there are no missing values across the 21 variables. this is a good sign since there is no need for imputation and hence the modeling process can proceed without the concern of Null data. It also ensures that feature interactions and statistical evelauation are based on full dataset.

Customer service calls exhibit very high outlier count, which could mean that either that some customers call excessively, maybe just before churning or due an operational issue e.g., poor service experiences. 
These may have predictive power and so we don’t necessarily have to remove them.

**Univariate Analysis**

This analysis explores the distribution of individual variables especially those related to customer behaviour. 

We will visualize distributions of numerical features, summarize categorical variables and be attentive to potential skewness and outliers. 

**b. Bivariate Analysis**

This analysis assesses how each feature relates to churn, which is the target variable.

# **3. Data Cleaning and Preprocessing**
The columns **phone number, state, and area code** are to be dropped as they offer little to no predictive value—being either unique identifiers, too high in cardinality, or lacking meaningful business relevance.

Within this Dataset there are two categorical features that need encoding:

- international plan (yes/no)
- voice mail plan (yes/no)

Since these are binary, Label Encoding (i.e., converting to 0 and 1) is sufficient and efficient.
In the dataset, the churn column is likely a Boolean which we converted to numeric (1 and 0). This ensures that the target variable is in a format compatible with classification models like logistic regression, decision trees, and random forests.


# **4. Feature Selection and Engineering**

By analyzing feature correlations and importance helps reduce redundancy and focus on the most predictive variables, improving model performance and interpretability. We used a simple Tree-Based Model,- Random Forest to estimate feature importance

# **5. Model Building**

**Logistic Regression Results**

Accuracy: 86.7% – The model correctly predicted 867 out of 1,000 cases.

ROC AUC: 0.82 – Fair discrimination between churners and non-churners.

Class Imbalance Issue:

Class 0 (Non-churn): Excellent performance with precision (0.89), recall (0.97), and F1-score (0.93).

Class 1 (Churn): Poor performance – only 27% recall. It misses most churners.

Conclusion: The model is biased toward the majority class and fails to capture churners effectively.

**Decision Tree Result**

Accuracy: 90.7% – Better than logistic regression overall.

ROC AUC: 0.83 – Slightly improved class separation.

Balanced Class Performance:

Class 0: Strong (precision 0.95, recall 0.94).

Class 1: Much better than logistic regression – recall improved to 73%, and F1-score is 0.70.

Conclusion: Decision Tree captures churners far better and is more balanced, making it a stronger model in this context

# **6. Model Evaluation**

Gradient Boosting now emerges as the top performer on the test set, exhibiting the highest accuracy and a superior F1-score, particularly for the positive class. This suggests it makes the most correct predictions overall and achieves a better balance between precision and recall for the minority class compared to the other models.

Random Forest remains a strong contender, with the second-best accuracy and a decent F1-score.

Decision Tree, despite a reasonable accuracy, still carries the risk of overfitting observed earlier.

Logistic Regression continues to show the weakest performance on the test set.

Compared to the other models, Gradient Boosting appears to be the most promising in terms of achieving a high accuracy while also maintaining a good balance between precision and recall, especially for the positive class. This makes it a strong candidate for the most balanced and effective model among those evaluated.


# **7. Interpretation and Insights**
To enhance model transparency, we visualized a simplified decision tree to illustrate how key customer attributes influence the model’s churn predictions.
The tree predicts customer churn based on a series of yes/no decisions using features like total day minutes, customer service calls, and voice mail plan.

**Key Predictors:**

Total day minutes is the most influential initial factor.

High total day minutes and absence of a voice mail plan are early indicators of churn.

The tree clearly shows the rules used to classify customers.

There is need for more evaluation on unseen data to check for overfitting.

In essence, the tree segments customers based on their usage and service interactions to identify those likely to churn.

# **8. Recommendations and Next Steps**

**1.Proposed targeted retention actions for high-risk customer segments.**

Based on the model’s identification of key churn drivers, SyriaTel can implement proactive retention strategies targeting customers most at risk of churning. These strategies may include:

- Offering personalized retention packages to customers with high daytime usage or frequent service complaints.

- Deploying loyalty programs for customers with high international call charges but no international plan.

- Providing priority customer service to those flagged with frequent service interactions.

**2. Suggested data collection improvements for future modeling**

To improve model performance and customer understanding, SyriaTel should enhance its data collection practices to capture richer customer insights. Some of the strategies may include:

- Tracking customer satisfaction ratings after service interactions.

- Recording usage patterns over time (time series data) rather than relying on single snapshots.

- Collecting feedback on pricing sensitivity or service quality perception through customer surveys.

**3. Recommend integration of the model into SyriaTel’s CRM or customer service platform.**

To operationalize these insights, SyriaTel should integrate the churn prediction model into its customer management workflows. This can be implented through:

- Embedding the model into the CRM system to flag high-risk customers in real-time.

- Alerting customer service agents to engage at-risk customers with pre-approved retention offers.

- Scheduling automated customer outreach via SMS, email, or calls for customers flagged by the model.





