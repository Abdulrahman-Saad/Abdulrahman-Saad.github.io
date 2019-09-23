## Introduction
Diamond is a solid form of carbon but what distinguishes it from other carbon based materials is that it has a unique atom structure (crystal structure). So, the atom structure made the diamonds look beautiful and thus it became an expensive material, and it is considered a luxurious material for most people. 
Since that diamonds are expensive, people don’t tend to buy them every day, they only buy them in special occasions. So when the time comes, and they decide to buy one they will not know every details about the diamonds. And that creates a problem, that problem is that people will not know how to determine the prices of diamonds. And that is normal because diamonds have a lot of features and people get confused between them. 
The big problem is that some diamonds traders use people ignorance about the diamonds feature to their benefit and they raise the prices of diamonds. And unfortunately, some people get ripped off because of this. But luckily there are solutions for this problem. the first one is reading about the diamonds and its features but that could be time consuming. The second one is to use the technology build a prediction model to predict the prices of diamonds by determining its features.  

## Business problem
Determining the price of diamonds needs experts and it is hard for people to determine it correctly and some diamonds shops could use this to rip off the people.
Also, the big diamonds traders could face a problem when they plan to buy a large amount of diamonds. It is difficult to determine the price of each piece of the diamonds. 

## Solution
The solution I am going to provide is linear regression model that predicts the diamond price based on certain features. So I will first investigate about the features that I will include in my model. And as I mentioned above that determining the price of the diamond is not easy and only experts could determine its price accurately, because they see more than a dozen feature in one diamond and then they determine its price.
But there is another way for the less expert people to determine the price. They call this way the 4 C’s, it is simply determining the price by looking to only four features, and they are the carat, color, cut and clarity. This method gives a nice result, not as accurate as the expert’s way but it does the job. And I am going to choose this way in my model.

## Methodology
After understanding the business problem and the solution that I am considering. I started working in the project and I can simplify this project by three phases. And they are web scraping, data exploring and building the model. I am going to mention them in detail in this section. 

### Web Scaping
This was the first step in the project. After understanding the business problem and the solution and some domain knowledge. I started gathering the data from James Allen website, I chose it because it provided all the information I needed, and it is also considered one of the leading in this field of business and they have reasonable prices. So it is nice to build my model upon its prices. I used python’s library BeautifulSoup to get the data I needed, and I scraped a total of 5,760 diamonds information

### Exploring the data
After gathering the data, I ended up with a large data frame as shown in the figure below.
![Image test]({{ site.url }}/images/dataf1.png)

So, in this step I started by cleaning the data and here are some of the things I did:  
•	Observing the plots of each feature and doing the necessary actions (e.g. box plot – remove the outliers).  
•	Check if there are null values.  
•	Check the levels of each categorical variable. (e.g. checking the levels of the currency – found out that there are multiple currencies while it should be one, so I had to unify them)  
After the data cleaning I started investigating the relationship between the variables by:  
•	Split the training and testing data sets.  
•	Observing the correlation (e.g. the carat had 0.91 correlation with the price).  
•	Observing the pair-wise plots. Here is an example in the figure below of one of the plots. It is between the carat and price and we can see that there is a linear relationship between them. And they might have a quadratic relationship. 

### Building the model
After cleaning and investigating the data we can now build the model. The approach that will be used is an iterating approach. I am going to build a base line model and then will try to improve on it then I will choose the best model. And I will evaluate the model by looking into two things and they are:  
•	R-squared and Adj R-squared for each model (the higher the better)  
•	The residuals plot for each model (point centered around zero and has constant variance is the best case)   

#### Baseline model
In this model I used only the numerical variable as my predictor (which is the carat) and used the price as my target. And I got the following result: 
•	R-squared = 0.819  
•	The residuals plot is shown in the figure below. And we can notice that the residuals are not evenly spread around zero and they have a non-constant variance  
![Image test]({{ site.url }}/images/baseline1.png)

#### The best model
After trying multiple models this was the best one in terms of R-squared and residuals plot. This model is different from the baseline model in three things: 
•	The carat value has been squared and added to a new column  
•	The color variable has been added to the model predictors  
•	The clarity variable has been added to the model predictors  
Note that the color and clarity are categorical-ordinal variables, so I had to transform them into integers by using label encoding. I didn’t consider the cut and shape because their p-values were more than alpha (0.05). and I got the following results:
•	R-squared = 0.932  
•	The residuals plot is shown in the figure below. And we can notice that the residuals are spread around zero, but they still have non-constant variance.  
![Image test]({{ site.url }}/images/best_model1.png)

## Results
In the results I am going test my best model with the testing data that I split earlier. First let’s see the equation of our model  
Price = -2814.11 + 1709.05*(carat) + 404.78*(color) + 305.27*(clarity) + 3972.92*(carat)2  
And when we apply this equation to the test data set. We get an R-squared = 0.92

## Limitations
This model didn’t have all the levels of the categorical variables.  
•	Color have only (f, e, d, g and h) levels  
•	Clarity have only (VS1, VVS2, VVS1 and IF)  

## Recommendations
After finishing this project, I would recommend the following point to however work in similar project  
•	Being careful by choosing the samples when scraping, to have a good model. So that you don’t need to over sample 

