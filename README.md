Customer Survival Analysis and Churn Prediction


Customer attrition, also known as customer churn, customer turnover, or customer defection, is the loss of clients or customers.

Telephone service companies, Internet service providers, pay TV companies, insurance firms, and alarm monitoring services, often use customer attrition analysis and customer attrition rates as one of their key business metrics because the cost of retaining an existing customer is far less than acquiring a new one. Companies from these sectors often have customer service branches which attempt to win back defecting clients, because recovered long-term customers can be worth much more to a company than newly recruited clients.

Predictive analytics use churn prediction models that predict customer churn by assessing their propensity of risk to churn. Since these models generate a small prioritized list of potential defectors, they are effective at focusing customer retention marketing programs on the subset of the customer base who are most vulnerable to churn.

In this project I aim to perform customer survival analysis and build a model which can predict customer churn. I also aim to build an app which can be used to understand why a specific customer would stop the service and to know his/her expected lifetime value.

Final Customer Churn Prediction App

<img width="1920" height="1116" alt="image" src="https://github.com/user-attachments/assets/167336c1-73d9-40c7-b6fa-62d36623c7f9" />

Project Organization
.
├── Images/                             : contains images
├── static/                             : plots to show gauge chart, hazard and survival curve, shap values in Flask App 
│   └── images/
│       ├── hazard.png
│       ├── surv.png
│       ├── shap.png
│       └── new_plot.png
├── templates/                          : contains html template for flask app
│   └── index.html
├── Customer Survival Analysis.ipynb    : Survival Analysis kaplan-Meier curve, log-rank test and Cox-proportional Hazard model
├── Exploratory Data Analysis.ipynb     : Data Analysis to understand customer data
├── Churn Prediction Model.ipynb        : Random Forest model to predict customer churn
├── app.py                              : Flask App
├── app-pic.png                         : Final App image  
├── explainer.bz2                       : Shap Explainer
├── model.pkl                           : Random Forest model
├── survivemodel.pkl                    : Cox-proportional Hazard model
├── requirements.txt                    : requirements to run this model
├── Procfile                            : procfile for app deployment
├── LICENSE.md                          : MIT License
└── README.md                           : Report

Customer Survival Analysis

Survival Analysis: Survival analysis is generally defined as a set of methods for analyzing data where the outcome variable is the time until the occurrence of an event of interest. The event can be death, occurrence of a disease, marriage, divorce, etc. The time to event or survival time can be measured in days, weeks, years, etc.

For example, if the event of interest is heart attack, then the survival time can be the time in years until a person develops a heart attack.

Objective: The objective of this analysis is to utilize non-parametric and semi-parametric methods of survival analysis to answer the following questions.

How the likelihood of the customer churn changes over time?
How we can model the relationship between customer churn, time, and other customer characteristics?
What are the significant factors that drive customer churn?
What is the survival and Hazard curve of a specific customer?
What is the expected lifetime value of a customer?
Kaplan-Meier Survival Curve:

<img width="400" height="280" alt="image" src="https://github.com/user-attachments/assets/0393663b-814b-449c-929d-49e3acc9d047" />


From above graph, we can say that

AS expected, for telcom, churn is relatively low. The company was able to retain more than 60% of its customers even after 72 months.
There is a constant decrease in survival probability probability between 3-60 months.
After 60 months or 5 years, survival probability decreases with a higher rate.
Log-Rank Test:

Log-rank test is carried out to analyze churning probabilities group wise and to find if there is statistical significance between groups. The plots show survival curve group wise.

  <img width="300" height="150" alt="image" src="https://github.com/user-attachments/assets/e14b64dc-4db1-4e03-ade7-3e1acc913ef8" />  

<img width="300" height="150" alt="image" src="https://github.com/user-attachments/assets/944a5e94-8ad3-4671-9826-ee9288e34669" />
 
From above graphs we can conclude following:

Customer's Gender and the phone service type are not indictive features and their p value of log rank test is above threshold value 0.05.
If customer is young and has a family, he or she is less likely to churn. The reason might be the busy life, more money or another factors.
If customer is not enrolled in services like online backup, online security, device protection, tech support, streaming Tv and streaming movies even though having active internet service, the survival probability is less.
The company should traget customers who opt for internet service as their survival probability constantly descreases. Also, Fiber Optilc type of Internet Service is costly and fast compared to DSL and this might be the reason of higher customer churning.
More offers should be given to customers who opt for month-to-month contract and company should target customers to subscribe for long-term service.
If customer's paying method is automatic, he or she is less likely to churn. The reason is in the case of electronic check and mailed check, a customer has to make an effort to pay and it takes time.

Survival Regression: I use cox-proportional hazard model to perform survival regression analysis on customer data. This model is used to relate several risk factors or exposures simultaneously to survival time. In a Cox proportional hazards regression model, the measure of effect is the hazard rate, which is the risk or probability of suffering the event of interest given that the participant has survived up to a specific time. The model fits the data well and the coefficients are shown below.

<img width="700" height="400" alt="image" src="https://github.com/user-attachments/assets/4b9e6a0a-6cc8-4a60-8d18-1ef6f3236389" />


Using this model we can calculate the survival curve and hazard curve of any customer as shown below. These plots are useful to know the remaining life of a customer.

 <img width="300" height="200" alt="image" src="https://github.com/user-attachments/assets/65b82a5e-a2bd-4c64-b335-8b67293133a5" />
<img width="300" height="200" alt="image" src="https://github.com/user-attachments/assets/c6e484ef-e8c6-4d01-afd8-85f3068d5b4c" />


Customer Lifetime Value:

To calculate customer lifetime value, I would multiply the Monthly charges the customer is paying to Telcom and the expected life time of the customer.

I utilize the survival function of a customer to calculate its expected life time. I would like to be little bit conservative and consider the customer is churned when the survival probability of him is 10%.

Customer Churn Prediction
I aim to implement a machine learning model to accurately predict if the customer will churn or not.

Analysis
Churn and Tenure Relationship:
<img width="700" height="400" alt="image" src="https://github.com/user-attachments/assets/045c5987-94c2-45d6-bb3d-57356de52c4a" />



As we can see the higher the tenure, the lesser the churn rate. This tells us that the customer becomes loyal with the tenure.

Tenure Distrbution by Various Services:
<img width="300" height="200" alt="image" src="https://github.com/user-attachments/assets/24c6c866-204d-4e73-8f70-6febd2bd6b7b" />



When the customers are new they do not opt for various services and their churning rate is very high. This can be seen in above plot for Streaming Movies and this holds true for all various services.

Internet Service By Contract Type:

<img width="553" height="372" alt="image" src="https://github.com/user-attachments/assets/96702144-920b-453f-8a15-2fc1cea0733b" />


Many of the people of who opt for month-to-month Contract choose Fiber optic as Internet service and this is the reason for higher churn rate for fiber optic Internet service type.

Payment method By Contract Type:

<img width="500" height="300" alt="image" src="https://github.com/user-attachments/assets/67b45811-7c17-4b86-963c-25244a8c95bb" />


People having month-to-month contract prefer paying by Electronic Check mostly or mailed check. The reason might be short subscription cancellation process compared to automatic payment.

Monthly Charges:
<img width="300" height="150" alt="image" src="https://github.com/user-attachments/assets/9954578e-27f6-4834-9792-b32874951f22" />



As we can see the customers paying high monthly fees churn more.

Modelling
For the modelling, I will use tress based Ensemble method as we do not have linearity in this classification problem. Also, we have a class imbalance of 1:3 and to combat it I will assign class weightage of 1:3 which means false negatives are 3 times costlier than false positives. I built a model on 80% of data and validated model on remaining 20% of data keeping in mind that I do not have data leakage. The random forest model has many hyperparameters and I tuned them using Grid Search Cross Validation while making sure that I do not overfit.

The final model resulted in 0.62 F1 score and 0.85 ROC-AUC. The resulting plots can be seen below.

 <img width="700" height="400" alt="image" src="https://github.com/user-attachments/assets/2f36b5d6-d188-41d3-becd-1eafb26ddfbc" />
<img width="500" height="300" alt="image" src="https://github.com/user-attachments/assets/7b38f6a5-94ee-44b0-9383-9787a55d9f71" />


From the feature importance plot, we can see which features govern the customer churn.

Explainability
We can explain and understand the Random forest model using explainable AI modules such as Permutation Importance, Partial Dependence plots and Shap values.

Permutation Importance shows feature importance by randomly shuffling feature values and measuring how much it degrades our performance.
 
<img width="400" height="300" alt="image" src="https://github.com/user-attachments/assets/adba33c6-c06d-49ad-86d1-69aba42816b6" />
<img width="300" height="200" alt="image" src="https://github.com/user-attachments/assets/db5e66c5-8abc-4a29-84ea-245f266481d2" />

Partial dependence plot is used to see how churning probability changes across the range of particular feature. For example, in below graph of tenure group, the churn probability decreases at a higher rate if a person is in tenure group 2 compared to 1.
 
<img width="700" height="400" alt="image" src="https://github.com/user-attachments/assets/314e70f3-3af8-447b-93db-291c4746c96a" />
<img width="500" height="300" alt="image" src="https://github.com/user-attachments/assets/743ccc0d-6485-4eba-9026-3e953a43f245" />
 

Shap values (SHapley Additive exPlanations) is a game theoretic approach to explain the output of any machine learning model. In below plot we can see that why a particual customer's churning probability is less than baseline value and which features are causing them.

<img width="1577" height="366" alt="image" src="https://github.com/user-attachments/assets/f4823299-f720-40f6-b535-6959633860cb" />

