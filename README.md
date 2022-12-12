# Sales-Forecast-for-Walmart
Walmart is one of the largest retailers in the world and it is very important for them to
have accurate forecasts for their sales in various departments. Since there can be many factors
that can affect the sales for every department, it becomes imperative that we identify the key
factors that play a part in driving the sales and use them to develop a model that can help in
forecasting the sales with some accuracy.

## DataSet
For this project, we have used the dataset available from ‘Walmart Store Sales Forecasting’
project that was available on Kaggle.
It basically housed three major files, the
test data, the train data and the features data set.
There were around 420,000 rows for the training set which made processing it very hard
In this dataset, we have weekly sales data for 45 stores and
99 departments for a period of 3 years. In addition, we had store and geography specific
information such as store size, unemployment rate, temperature, promotional markdowns etc.

## Challenges
The key issues that we have faced in this analysis is
the large dataset that resulted into several computational challenges because of which we had
to modify our approach in addressing the problem. We also faced significant challenges in
identifying the right variables on which the analysis could be conducted
In this project, we conducted multiple linear regression to predict the future sales. There were
several different factors that we analyzed in our regression model starting with a full model with
all the variables and then moving towards a reduced model by eliminating insignificant variables.
We used several different exploratory analyses to identify the key variables for our regression
equation such as correlation plots, heatmaps, histograms etc.
Few other time series forecasting models could have been used as the weekly sales is highly
dependent on the past year. Moreover, ARIMA modelling techniques like exponential
smoothening and holt winters could have helped us capture the seasonality in the model in a
better way. Furthermore, ARIMAX model would have enabled us to have an accurate time series
model based on previous weeks of data as well as factor in few important variables like holiday
and department type to get an even better accuracy.

## Approach
As our first step we focused on merging the data sets to get all the factors which could help us in
predicting the weekly sales. Post that we spent some time identifying the erroneous entries in
data, descriptive statistics indicated towards the possibility of negative sales value in the data. To
confirm and revalidate the same we plotted a normalized histogram, if we look closely we can
see that there are some values which lie on the negative side of zero indicating negative sales.
Therefore, we sanitized our data to drop these erroneous values to minimize the impacts of them
on our analysis.

![Picture1](https://user-images.githubusercontent.com/110618663/207133466-40ffc220-cec2-4883-9393-942b7152f6d3.png)

As our next step we created a full model consisting of majority of variables available with us, to
facilitate this we created lagged variable based on timeframe (weekly lag sales), as we believe
that this would help us capture the inherent attributes of particular store type and department.
Moreover, we created dummy variables out of the categorical values given in the data set (e.g.,
department and type). The main intent behind creating them was to factor in some departments
which perform very differently from the rest. If we take a closer look at the heat map and the
scatter plot of mean weekly sales vs T-Statistics we can safely conclude that dept 38, 95 and 92
play a pivotal role in predicting future sales. Consequently, we decided to include them in our
regression variables.

![Picture2](https://user-images.githubusercontent.com/110618663/207133683-553d41b1-8bae-43c6-9cd2-52ae6912c042.png)

![Picture3](https://user-images.githubusercontent.com/110618663/207133766-2ae19544-38b8-4d91-aeb7-8e09fd57fe6b.png)
![Picture4](https://user-images.githubusercontent.com/110618663/207133799-d46f4ef3-9e90-4923-8a3e-6a8982eb605b.png)

We also did various descriptive statistics. We saw the correlation matrix and found that size and
department are correlated with weekly sales.
We did clustering based on Type of store and Weekly sales and found 3 clusters (based on elbow
plot we decided the number of clusters). With these insights, we did the reduced model of linear
regression.

![Picture5](https://user-images.githubusercontent.com/110618663/207133965-aa56ea60-3fc8-489d-8d46-2156cbb0a350.png)
![Picture6](https://user-images.githubusercontent.com/110618663/207134043-7f08d3f9-d037-4f16-ba7b-050d0e852c3d.png)

## RESULTS
We found the regression equation when we don’t use promotional markdown variables as:
𝑊𝑒𝑒𝑘𝑙𝑦 𝑠𝑎𝑙𝑒𝑠 = 247.396 – (845.53 * ℎ𝑜𝑙𝑖𝑑𝑎𝑦) + 9.979 * 𝑇𝑒𝑚𝑝𝑒𝑟𝑎𝑡𝑢𝑟𝑒
+ 0.9067 * 𝑊𝑒𝑒𝑘𝑙𝑦 𝑆𝑎𝑙𝑒𝑠 𝑙𝑎𝑔 + 698.93 * 𝑇𝑦𝑝𝑒_𝐴 + 5.613 * 𝑇𝑦𝑝𝑒_𝐵
− 457.146 * 𝑇𝑦𝑝𝑒_𝐶 + 2363.138 * 𝑊𝑒𝑒𝑘_50 + 6783.568 * 𝑊𝑒𝑒𝑘_51
+ 5074.345 * 𝐷𝑒𝑝𝑡_95 + 5462.166 * 𝐷𝑒𝑝𝑡_92 + 4289.939 * 𝐷𝑒𝑝𝑡_38
The accuracy of this model is found to be 84.56%.
When we use promotional markdown in the regression equation, the regression equation is:
𝑊𝑒𝑒𝑘𝑙𝑦 𝑠𝑎𝑙𝑒𝑠 = 37.195 – (852.324 ∗ ℎ𝑜𝑙𝑖𝑑𝑎𝑦) + 9.827 ∗ 𝑇𝑒𝑚𝑝𝑒𝑟𝑎𝑡𝑢𝑟𝑒 + 0.929
∗ 𝑊𝑒𝑒𝑘𝑙𝑦 𝑆𝑎𝑙𝑒𝑠 𝑙𝑎𝑔 + 523.328 ∗ 𝑇𝑦𝑝𝑒_𝐴 − 72.719 ∗ 𝑇𝑦𝑝𝑒_𝐵 − 413.414
∗ 𝑇𝑦𝑝𝑒_𝐶 + 2256.694 ∗ 𝑊𝑒𝑒𝑘_50 + 6673.006 ∗ 𝑊𝑒𝑒𝑘_51 + 4280.914
∗ 𝐷𝑒𝑝𝑡_95 + 4809.748 ∗ 𝐷𝑒𝑝𝑡_92 + 3575.849 ∗ 𝐷𝑒𝑝𝑡_38 + 0.0938
∗ 𝑀𝑎𝑟𝑘𝑑𝑜𝑤𝑛 − 3.881𝑒 − 6 ∗ 𝑀𝑎𝑟𝑘𝑑𝑜𝑤𝑛 ∗ 𝑤𝑒𝑒𝑘𝑙𝑦_𝑠𝑎𝑙𝑒𝑠_𝑙𝑎𝑔
We get accuracy as 84.53% in this model. We find that the regression co-efficient for interaction
variable (markdown ∗ weekly_sales_lag) is miniscule. The regression co-efficient for markdown
is also low at 0.0938. These both again confirm the fact that Markdowns given at Walmart are
not significantly impacting the sales. They will have to overhaul the Markdowns given and try
new markdowns.
The residual plot shows that the errors are random and there is no pattern in that. Hence there
is no heteroscedasticity.

![Picture7](https://user-images.githubusercontent.com/110618663/207134161-83647479-c26e-46bc-9de9-61ce75e9516c.png)
The above plot shows that the residuals have fairly similar variance. Hence we can say that the
data is not having heteroscedasticity.

![Picture8](https://user-images.githubusercontent.com/110618663/207134227-9757bb9f-50df-44b2-9650-c5047bc41ab5.png)

From the above plot, we find that the residuals are normally distributed. Hence both normality
and homoscedasticity are there. Therefore, we can use the regression equation without any
transformations.

![Picture9](https://user-images.githubusercontent.com/110618663/207134344-54f1a6b1-586c-4e83-9993-e813f7a13f69.png)

The next major hurdle is the K-Means algorithm. As we know, adding new data points to existing
cluster won’t require a lot of iterations. Also, now that we have calculated the important
departments, we will monitor the same departments for a long time.
The most important factor in time complexity is the running time of the linear regression. Linear
regression takes O(c2n) time complexity as can be seen from the graph below. This might create
a problem when the data size doubles. So, we do use iterative linear regression. In this process,
use the current coefficients as the latest estimate of beta and we update them based on each
new incoming row.
We have also taken care of the situation when the data comes in batches. As can be seen in the
commented code in the time complexity block, we can find the updated estimate per batch in a
single step.

![Picture10](https://user-images.githubusercontent.com/110618663/207134444-3c2c8b70-073a-473d-b299-a11f4e927c89.png)

The next analysis we did was profiling. Based on our analysis, length computation and assignment
are the two main time-consuming factors. As both of these are internal commands, we conclude
that the code is indeed currently optimal. We also tried minimal use of loops in our code and
tried to find more efficient alternatives such as shift and map.

## CONCLUSION
In conclusion, we find that our regression equation is quite accurate (84.5% accuracy) in
predicting the weekly sales. Walmart can use it to forecast the sales better. They need to focus
on the inventory planning of key departments like 38,92 and 95. They need to overhaul the
Markdowns that are given currently as they are not having the intended impact on sales. They
need to focus on the year-end inventory as week 51 and 52 play a crucial part in predicting sales.

Our regression is having a high accuracy and the scatter plot confirms this:








