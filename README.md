# arya-ai-sample

## Description
Our task at hand is to perform binary classification. We are provided with two files where one is the training set and the other is he testing set. There are 3910 rows and 58 columns in the training set. The last column indicats the labels and the reamining indicate the features. There are only two sets of labels present and they are encoded as 0 and 1 respectively. The testing contains 691 rows and only 57 columns. This is because the testing set does not contain any labels. The columns names aren't descriptive and are named as X1 till X57. 

## Exploratory data analysis
On printing the top rows of both the sets we see that many of the cells contain zeros. When we search for null values, we find that there aren't any. This could also mean that the zeros are used to represent missing values, but we cannot be sure. When we print the basic statistics, we can see that almost all the quartile values are zeros. There is a high possibility that both the feature matrices are sparse. All the data points are high dimensional and this makes it difficult to visualize the data. That's why, we'll stick visualizing the train data using parallel coordinates plot. 
![image](https://user-images.githubusercontent.com/83799967/135743428-a67c1e82-dca2-4fcf-b0fb-8111bafca1d2.png)
We are able to efficiently plot the columns from X1 to X57 using this technique. Points belonging to class 0 are coloured in blue whereas the remaining in green. Notice that most of the values till X53 have the value of zero and then there is an abrupt increment in the values. beyond this column.

## Feature engineering
Since not all features are of the same scale and so we must standardize the values. Otherwise, the model interpretation may turn out to be sub-optimal. Since this high dimensional matrix is sparse and may potentially contain correlated columns, reducing the dimensionality improves the computation time and also model performance. For this purpose, we shall be using singular vector decomposition. Using this technique, our large feature matrix can be factorized into three smaller matrices. Now finding the optimal number of features that can explain most the data variance is difficult. Most of the convential technique take a heuristic approach where the variance explained in visualized and compared. This is the step where we obtain the optimum value using the hard threshold technique. Given below are the set of equations introduced for this technique-

![image](https://user-images.githubusercontent.com/83799967/135745400-f64cd8ae-c225-4342-8951-7d20fa4ba75c.png)

The value of m and n represent the dimensions of the data matrix. ![image](https://user-images.githubusercontent.com/83799967/135746036-a9286700-08a2-4157-b912-0d51eda6e15c.png) is an approximation used when the noise level ![image](https://user-images.githubusercontent.com/83799967/135745696-cd0024ab-8b44-4b28-a22a-4fdf5e75bbb5.png) is unknown. ![image](https://user-images.githubusercontent.com/83799967/135745735-e5480724-4c1f-4b79-a2d6-839cacf4f2a3.png) represents the median of the singular values given in the central matrix and ![image](https://user-images.githubusercontent.com/83799967/135745876-20e5dca0-89dc-4b92-a817-10728c7d049f.png) represents the threshold value. We find the optimal value to be 3. This means that three features can represent the entire data matrix. 

## Machine learning
Gradient boosted decision trees is a good machine learning algorithm that can efficiently capture the underlying pattern of the data. That's why we will be using it for the training and prediction purpose. The best parameters are obtained using randomized search cross validation. The entire data set is divided into 4 folds for this purpose. As required, accuracy is the performance metric used for scoring. With the maximum decision tree depth as 5 and the number of estimators as 110, we are able to clock the accuracy value of 0.877. We'll now use these parameters to predict the test data.




