# RecommendationSystem
Recommendation System using PySpark

I built a hybrid recommendation system utilizing Yelp dataset for which I first decided to use model-based CF as the primary recommender for its better performance over item-based CF.
First I tried to improve model-based CF by adding more features.
One thing I found out is that feature engineering is very important.
For example, I first use one hot encoding to add "categories" of business.json.
However, there are 1000+ different categories.
As a result, adding those dummy variables directly to the model will slow down the training process and did not improve the model's performance.
So I used PCA to conduct dimensionality reduction and only kept the top 10 pca components as the features.
This resulted in about 0.002 improvement in RMSE.
On the other hand, I tried to utilize the power of item-based CF by implementing a feature-augmented CF.
I did so by adding the prediction as a feature to the model-based CF.
And that is the best model I had up to the deadline.

Other recommender systems I tried but wasn't very successful:
Use K-means to cluster the data and train model-based CF on each cluster (make predictions by first assign active user-business pair to nearest cluster)
--> One possible reason why this method is not working is because to do K-means clustering, all the points are naively represented by a point in Euclidean space
For certain type of business (mainly restaurants), collect extra features for these businesses (e.g., GoodforKids) and train two models: one for that type of businesss and one for all businesses
--> This method is not working probably because the exclusion of some valuable information from other businesses in the first model (which is about 1/4 of the training data)
