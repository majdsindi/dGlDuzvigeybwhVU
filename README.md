# PROJECT SUMMARY
## Background:
This data comes from a startup company in the logistics and delivery domain. Customer happiness is at the forefront of this company’s mission. The company has recently did a satisfaction survey to a select customer cohort. This is a subset of that survey’s data.

## Data Description:
Y = target attribute (Y) with values indicating 0 (unhappy) and 1 (happy) customers

**X1** = my order was delivered on time

**X2** = contents of my order was as I expected

**X3** = I ordered everything I wanted to order

**X4** = I paid a good price for my order

**X5** = I am satisfied with my courier

**X6** = the app makes ordering easy for me

Attributes **X1** to **X6** indicate the responses for each question and have values from 1 to 5 where the smaller number indicates less and the higher number indicates more towards the answer.


## Goals:

**1.**	Predict if a customer is happy or not based on the answers they give to the survey.

**2.**	Identify which features are the most influential in predicting customer happiness.

## Discussion:

My analysis began with Exploratory Data Analysis (EDA) to understand the distribution of customer ratings (**X1-X6**) and their relationship with the overall happiness (**Y**). My first key observations are:

**•**	**X1**, **X5**, and **X6** show clear trends for happy and unhappy customers. These are expected to have the most influence. This is further supported by the Pearson correlation matrices, providing a quantitative measure of these observations. This indicates that the most influential part of the business model on customer happiness is the delivery of goods. **X1 (order delivered on time)** and **X6 (satisfied with courier)** both allude to the same thing: courier service, which is expected to be where customer happiness is tied to.

**•	X2**, **X3**, and **X4** had more mixed distributions, where influence on happiness is more nuanced and will not be easy to detect with how small the dataset is. This does not mean that these aspects are not important, more so they are more nuanced and do not directly correlate to customer happiness.


To identify top-performing models, *LazyClassifier* was used, revealing that *NearestCentroid*, *AdaBoostClassifier*, *LinearSVC*, and *LogisticRegression* were among the highest-performing models with all features. 
Due to the random nature of performing the test/train split of the data, I performed an iterative search to find the best seed where the models performed best. I tested 9000 seeds and ran *LazyPredict* for each one, noting the top performing models. *Nearest Centroid Classifier* coming out on top with an accuracy score of 92%.


Subsequent attempts to improve performance using *VotingClassifier* and *StackingClassifier* did not yield significant gains, suggesting that ensemble methods, in this specific context, did not add substantial value over individual classifiers.


Given the goal of identifying influential features, two primary feature selection methods were utilized:

**•**	**Manual RFE-like approach with *NearestCentroid***: This iterative method, which evaluated model performance after dropping combinations of features, consistently highlighted X1 and X5 as the most critical features. Models performing poorly (low accuracy) frequently resulted from combinations where X1 or X5 were among the dropped features.

**•**	**Univariate Feature Selection using *SelectKBest* with *f_classif***: This statistical test-based approach also ranked **X1** and **X5** highest, further confirming their strong individual correlation with the target variable (**Y**).


Finally, the selected top models (*NearestCentroid*, *AdaBoostClassifier*, *LinearSVC*, and *LogisticRegression*) were re-trained using only X1 and X5 to confirm their influence. The results were:

**•**	*AdaBoostClassifier* improved its accuracy from approximately 0.833 (with all features) to 0.88 (with **X1** and **X5**). This is a strong indicator that for this model, **X1** and **X5** are indeed the most discriminative features, and other features might be less relevant.

**•**	*NearestCentroid*, *LinearSVC*, and *LogisticRegression* experienced a decrease in accuracy when limited to X1 and X5 (from ~0.833-0.917 to 0.77-0.81). While still performing reasonably, this suggests that for these models, the other features (**X2, X3, X4, X6**) did contribute to their overall performance, but to a lesser extent than **X1** and **X5** since the performance drop was not significant.


Overall, the consistent identification of **X1** and **X5** as highly influential features across multiple analysis techniques strongly supports their importance in determining customer happiness.


# RECOMMENDATIONS

The comprehensive analysis of the dataset unequivocally points to X1 (my order was delivered on time) and X5 (I am satisfied with my courier) as the two most influential features determining customer happiness (**Y**).

**1.	Prioritize faster delivery:**

Efforts to enhance customer happiness should primarily focus on improving the timeliness of order deliveries (**X1**). This can be achieved by improving the communication of the expected delivery time to maintain customer expectations. Alternatively, enhancing logistical systems and delivery timelines to adhere to pre-advertised delivery times would achieve a better score.

**2.	Ensure courier portrays the company positively:**

Customers are not satisfied with the courier. This could be due to a multitude of reasons such as lack of professionalism or friendliness in delivery, like leaving packages in non-safe places. Ensuring customers are satisfied with the specific courier and the way they portray the company will achieve better customer happiness. This could be investigated further via a more courier-specific survey.

