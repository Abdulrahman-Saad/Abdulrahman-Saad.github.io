## Introduction
Customers churn have been a concern to many companies throughout the years for many reasons. So in this project customers churn problems will be discussed, analyzed and finally solutions will be delivered to help companies keep the customers churn rate as low as possible. 

### What is Customer Churn?  
Customer churn term is often used in companies that provide services. And it refers to when a customer leaves a company that he was subscribed to or he was using their services. Here are some good examples to customer churn:  
1-	A customer closes his bank account  
2-	A customer leaves his telecommunication company and go to another  
3-	A customer cancels his subscription in online streaming service (Netflix account)  


### Why Companies Care About It?
Companies care about reducing the customer churn rate for one big reason. The reason is the fact that customer retention costs are much lower than customer acquisition costs and some studies claims that retention costs are 5 to 25 times lower than acquisition costs.
It can be concluded that if a company keeps a customer whose about to leave them. Costs will be greatly reduced. Because if they can’t keep the customer, they will have to bring new customer in his place and that will cost them much more.


### How to Prevent Customer Churn?
There are two ways to keep the customers. The first one is to give the customers offers after they decides to leave (e.g. a bank gives a customer an offer when he goes to them to close his account) and this way is not preferable. Because it doesn’t create a good relationship between the company and the customer, and there are many researches that talk about why this method is not good.


The second method is to give the customer a suitable offer before he decides to leave. According to the marketing researches this method is much better than the first one. Because it makes the customer feels that the company is giving him some special care. 


Since that the second method is the preferable one, companies should pursue this method. But in order to apply this method one final question should be answered. Which is why do customers leave companies. If this question is answered, companies could predict if a customer is going to leave them or not.


### Why Do Customers Leave Companies?
There are many reasons, but in this project two main reasons has been focused on, the first one is that the customers leave for **better prices**, and this is due to the offers that competitive companies make. The second reason is that the customers leave for **better quality**.


## Business Solution
After answering all the question above a business solution could be made. The solution is to use machine learning to predict weather a customer will leave or not. A solution can be built by training a prediction model about customers general attributes, the services that they were subscribed in, their monthly charges/usage and weather they churned or not. 


Those features have been chosen because they represent the reasons that have been mentioned above about why customers leave. The customers general attributes could give an indication if a competitive company have been targeting some categories of our customers for better prices. 


And the services that they were subscribed in and their monthly charges/usage could give an indication about weather the customer is experiencing a bad quality or not. 

## Objective
•	To build a classification model to predict whether a customer will churn or not in the telecommunication industry  
•	To find the interesting relationships between the target and the features that the model will present. To help in communicating the results to the marketing department so that they can make a suitable offers to the customers that are going to churn in the future. 

## One Important Takeaway
In order for the prediction model to have value. The customer’s monthly charges/usage features should not include the month that is prior to month that is being studied (the month that contain the information if a churn will happen or not). The figures below explain this point. (month 4 should not be taken into consideration)  


![Image test]({{ site.url }}/images/Wrong_way.png)  
![Image test]({{ site.url }}/images/Right_way.png)  


The reason that this month should not be taken into consideration although that it has valuable information is because a buffer time is needed for the marketing department to make offers to the customers that are going to churn. For example, if month 4 in figure above was taken into consideration the model will predict the customers that are going to churn in the next few days and that is not acceptable. 


## Methodology
![Image test]({{ site.url }}/images/metho.png)  

### Gathering the Data
The data has been downloaded from [Kaggle](https://www.kaggle.com/blastchar/telco-customer-churn) . And this dataset contains information about customers in a telecommunication company and weather they churned or not. 

### Cleaning the Data
•	The dataset had small number of observations that had null values and they have been deleted.   
•	The datatypes have been changed for the numerical features  

### EDA 
In this step all the features have been investigated in different methods with each label in the target variable. And a lot of interesting relationships have been founded. An example will be given for each method. 


#### Distributions
![Image test]({{ site.url }}/images/histo.png)  
The figure above shows the distribution of tenure with each label in the target. And it can be noticed from the figure that the customers who have churned had more smaller tenure values than the ones who didn’t. and it is very clear that the customers who had large tenure values most of them didn’t churn. although that the target labels are imbalanced, this is a valuable information


#### Boxplots
![Image test]({{ site.url }}/images/boxp.png)  
Boxplots have been drawn to see the five numbers (minimum, first quartile, median, third quartile and maximum) for each feature with each label in the target. And this plot gives nice information before jumping to the model.


#### Percentages
Status | Churned | Didn't Churn
------------ | -------------| -------------
Has fiber optic| 70%  | 35%
No fiber optic| 30%  | 65%

After looking at the percentages it seems that there is a high correlation between fiber optic service and the target. And it seems that there is problem with this service because it has high churn percentage

### Model building
Four different algorithms have been applied in the modeling and they are  
•	Logistic Regression  
•	Random Forest  
•	Naïve Bayes  
•	KNN  


After doing the necessary things to the dataset (e.g. scaling the data) and choosing the best hyperparameters for the models. We get the following validation accuracies results  
•	Logistic Regression = 0.8065  
•	Random Forest = 0.7982  
•	Naïve Bayes = 0.6675  
•	KNN = 0.77  

### Choosing the Best Model
After getting the best model for each algorithm a decision must be made to choose the best algorithm as our performing model. The decision will be made by using a cost function that will be determined. The reason for choosing the cost function is because none of the evaluation metrics (accuracy, precision, recall and F1) fit this problem specifically. 

#### The Cost Function
In this business problem the cost is the most important factor. And we have two types of costs in this business problem. the cost of keeping a customer and the cost of loosing a customer. As mentioned in the introduction that studies say that the cost of keeping a customer is 5 to 25 times less than loosing one. In this project a conservative approach will be taken, and we will assume that the retention costs are only 5 times lower than acquisition costs.


So, to evaluate the models that have been built, we must calculate the costs related to them. And this can be done by looking at:  
•	how many customers have churned and the model predicted that they will churn (TP)  
•	how many customers haven’t churned and the model predicted that they will churn (FP)   
•	how many customers have churned and the model predicted that they will not churn (FN)  


These values can be found in the confusion matrix as shown below. 
![Image test]({{ site.url }}/images/conf22.png)  


So we can calculate the cost function for each model:  
Cost (x) = TP (x) + FP (x) + 5*(FN) (x)  
By assuming x (the cost of keeping a customer) = 1 we get the following results  
•	Random Forest = 841 + 424 +654*5 = 4535  
•	Logistic Regression = 837 + 421 +658*5 = 4548  
•	Naive Bayes = 1120 + 1425 + 375*5 = **4420**   
•	KNN = 461 + 193 + 1034*5 = 5842   
It can be noticed that Naive Bayes model has the lowest cost. So it should be chosen as the performing model. 


### Testing
After choosing Naive Bayes to test our out of sample data we get the following results  
Accuracy = 0.67  
Recall = 0.74  
Precession = 0.43   

## Conclusion 
The model can be improved by considering more features/. Specially if the detailed monthly usage data was provided, a much better results would have been obtained. 


Evaluating the models by looking only at the accuracy is misleading if the target labels were imbalanced. For example, in my case the models that provided the lowest accuracy gave the best results. 


The results can be improved by balancing the target labels. By using SMOTE method for example. 
