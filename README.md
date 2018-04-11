
# Facebook Text Extraction Challenge


# 1.	Understanding the problem
- The dataset represents the information from user posts across the different stack websites like Stack OverFlow, Stats OverFlow, Math Overflow etc.
-	Dataset tells about the title , body  and tags (multiple categories in which the problem is classified) associated with each of the post
-	Purpose: Build the NLP model to effectively classify the user posts into the tags 

# 2.	Data Cleaning
-	Data contains huge number of duplicates so eliminate them while training the model. There is very high overlap between the train and the test data, so keeping that into consideration while making a prediction
-	Remove all the HTML tags from the body 
-	Remove all the codes from the body because they don't add any value to our prediction 
-	Remove all the stop words from the body and the title
-	Tokenize the body and title using RegexTokenizer on a regex pattern which eliminates all values except alphanumeric values and "#,+"(because of heavy presence of C++, C# in the data)
-	Tried performing Stemming on the body , but stemming does not add any value to our model because stemming does not yield any concrete output on technical tags

# 3.	Data Transformation
-	Assumption: Title is more important in making the prediction of the tags than the body
-	Created a synthetic variable called body_title i.e. combination of cleaned body and title in the ratio of 1:2

# 4.	Data Exploration
-	On average, a post contains 2-3 tags based on 10,000 rows sample
-	There are 6124 unique tags based on 10,000 rows sample
-	Count of tags is logarithmically distributed , with few tags (like c++, c#) being repeated frequently across many rows

# 5.	Building the Model
-	I tried understand the trend and the spread of the data by using unsupervised learning such as :
"	K-Means Clustering
"	Gaussian Mixture Clustering (Analyzing the probabilities of belong to a cluster)
"	Topic Modelling i.e. latent dirichlet allocation (LDA) to make the prediction on the topics
"	FP-Growth (Frequent Pattern)

# K-Means Clustering
- Classifying the combined body title into a cluster and understanding the data spread where the data falls in the cluster
- Classified each rows (1000rows) into 100 clusters with around 864 rows falling into cluster 16

To further understand the clustering distribution in performed Gaussian Mixture Clustering (GMM) , where I analyzed probability of each row falling into the cluster

# Topic Modelling i.e. latent dirichlet allocation (LDA)
-	Classifying the rows into topic of 10
-	Output did not align much with tags we had to predict 
-	Training on large amount of  data will help us predict the topics corresponding to the data

# Multilabel Classifier
-	Build the One vs Rest Classifier to predict tags and F1 score using different models i.e. Linear SVC, Logistic Regression and Decision tree

# FP-Growth
-	Tried identifying association rules with the data in the body, title combined column (each entity in the rows was unique) but the output coming up was showing no confidence rules and associations
-	The association rules obtained can be leverage to further predict and improve the accuracy
