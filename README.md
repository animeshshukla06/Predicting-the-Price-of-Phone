The file involves the case study of predicting the price of a mobile phone using the phone's specifications as independent features (data has been collected from Kaggle). Here, I have done a lot of analysis and preprocessing of data since there were a lot of missing values and depending upon the proportion of missing values, we choose suitable techniques for dealing with them. This is a brief post focusing on all aspects of Life Cycle of Data Science Project starting from detailed data preprocessing steps, model building, model evaluation, checking whether the model is underfitting or overfitting to getting the prediction and confidence Intervals for training data.
In the notebook, you would get a brief idea of how to preprocess the data and steps involved for data preprocessing:
		○ Dealing with missing values based upon the proportion of missing values for different features.
		○ Run various Statistical Test to understand the dependence of one feature to the other and further we can deal with the missing values.
		○ If missing values are quite large, then you might need to use Machine Learning Algorithms solely to deal with it: In such a case, model is trained on the non-null data with the feature having missing values as target feature.
		○ Univariate Outlier Detection: Boxplots, IQR, Z-score are the common ways to detect univariate outliers in data and deal with them using appropriate technique.
		○ Multivariate Outlier Detection: Mahalanobis Distance is commonly used for detecting multivariate outliers in data. Further, we can also use some unsupervised Anomaly Detection to flag the possible multivariate outliers. I have used Local Outlier Factor and Isolation Forest algorithms (discussed   In brief later on) to get an idea of multivariate outliers in our data.
    Try finding relationships between the dependent feature and independent features separately, since it indicates the mathematical relationship between them and hence, once it has been understood, we can transform any one of the feature.
    
    
Further, after dealing with all of the missing values, outliers and performing respective transformations, we move ahead with Feature Selection. Remember to scale the features beforehand. The way I go ahead with Feature Selection is:
		○ Use ANOVA to observe if any of the independent categorical feature is explaining some variance of the numerical target feature.
		○ If the result of ANOVA is significant: choose that particular categorical feature and move ahead encoding the categories of that categorical feature. 
		○ Further, if the categories are less, (approximately less than 10), then you can directly encode them using One hot Vectors or Ordinal Encoding, whatever the case may be.
		○ However, if there exists a lot of categories, then we should choose the top 10 categories based upon the frequency of each category and encode them.
		○ For independent numerical features, we can use different feature selection techniques such as:
			§  'f_regression' which computes the correlation between each independent and dependent feature and computes F-value using the correlation score, which is further illustrated by 'p_value'. If the p-value<0.05, then we reject the null hypothesis and the feature is considered to be a significant predictor.
			§ 'mutual_information' which computes a dependency score between each independent and dependent feature. The independent features which have high score are referred to as important features and vice versa.


We the move to Model Building and the most important points to consider while building the model:
		○ The features which are selected during Feature Selection Step, we now should compute the correlation among independent features so as to not to choose two independent features which have high correlation among them else the problem of multicollinearity would arise and the error terms would get correlated.
		○ Then, try building the model. I have trained a multiple linear regression model.
		○ Now to understand the worth of your model, you should have some technique to evaluate it. For example, in Linear Regression, after building the model, we evaluate if the residuals follow the following assumptions of Linear Regression:
			§ Linearity
			§ Normality of Residuals
			§ Homoscedasticity of Residuals
			§ No Autocorrelation among the Error Terms
		○ These 4 assumptions should meet in order to claim that you model is good. If any of them are not sufficed, then you must investigate the problem in your model.
