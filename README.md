# Clustering market segments with K-means and Factor analysis

![segmentation](https://user-images.githubusercontent.com/96744665/148271272-daf7de98-c4b0-48e2-840e-350995c5e75b.jpg)
## [Dashboard](https://public.tableau.com/app/profile/gabriele.frattini/viz/MarketSegmentation_16395789417390/Dashboard)

***

## Introduction
In the context of clustering, the quality of variables will determine the quality of clusters. Variables that are irrelevant and trivial may hurt the discriminatory power of clustering technqiues and give less reliable results. In this project I’ll be using a dataset with 25 different customer features to perform my analysis on.
The goal of this article is not only to gain insights from market segmentation applied to customer data, but also to examine the results of k-means clustering applied to the original data and then on the data transformed to fewer dimensions with factor analysis.

***

## Project Summary
- Built a dashboard for the business to monitor their customer data
- Identified four different market segments on the original data
-Identified five generalized segments from factor scores
- Recommended products to market to the different target groups
- Presented pros & cons with clustering on dimension-reduced data

***

## Clustering on the original data

I performed k-means clustering on the original data, except it was standardized since the alghoritm is sensetive to different units of measurement scales.
To evaluate the quality of different cluster sizes we can compute a silhouette score which is as a measure of how similar an object is to its own cluster compared to other clusters.
Four seems to be the optimal amount of clusters since the silhouette scores for each cluster are above average and have the most unform sizes.

![silhouette_viz1](https://user-images.githubusercontent.com/96744665/148271353-9ef93707-2557-40fc-89d6-d5fd29469bdb.png)

***

## Market segments

![cluster1](https://user-images.githubusercontent.com/96744665/148271399-273fb2fc-15b9-43a3-98f9-39d30630face.jpg)

- Lower income families that have low spending habits but patterns of high web visits per month.
- The current product stock is not relevant enough for this cluster, my recommendations are to collect data about searches on our website from this group and sell more relevant products, potentially family- and children related products


![cluster2](https://user-images.githubusercontent.com/96744665/148271465-05eb6857-d10a-4d88-88d3-2e800e43a872.jpg)

- Higher-income earners without children, our most profitable group that preferebly purchases products in-store or by catalog. Could be considered a more “old-school” group of customers that don’t like to shop on the internet
- Continoue to distribute catalogs and allocate products in physical stores since there is still a big market for this


![cluster3](https://user-images.githubusercontent.com/96744665/148271531-55241573-2e67-4da9-a1d2-e609a882f387.jpg)

- Older customers with families that has been customers for a longer time. This group purchases mostly online but also in-store and responds very well with products on deals. Also has a particular interest for wine and gold.

- Market more discounted wine- and gold products towards this cluster to increase sales.


![cluster4](https://user-images.githubusercontent.com/96744665/148271598-217ba312-ffdc-4ed7-bc6c-55d40a46ae5e.jpg)

- High-income earners without children, are well diversited in spending and our most successful group in terms of marketing campaigns. Strongest patterns in wine- and meat purchases.

- Research what products were being used during campaign five and one analyze further why this group has responded so well in particular to these two campagins

![kmeans_first](https://user-images.githubusercontent.com/96744665/148271660-3196b6f2-2438-4df9-b9ae-fe005b72c47b.png)

***

## Pre-processing the data with factor analysis

The point of doing a factor analysis here is to reduce noise in the data by searching for underlying factors that reproduces the intra-relationships as accuratly as possbile, but in fewer dimensions.

Factor scores can then be obtained for each row on each factor using a least squared regression which takes in to account the correlation between factors and factor loadings and can thus be interpreted as numerical values that represents a customer’s relative standing on a certian factor.

Clustering on the dimension-reduced data then has the amazing potential to reveal the same clusters but on a data that needs fewer variables and is of higher quality.

Would the business also be interested in building ML-models in the future with customer features as predictors, the business could benefit from reduced risk of overfitting and complexity in the models.

***

## Extraction & rotation

Factor loadings were extracted with principal axis factoring and then rotated to make the loadings more interpretable.

There are mainly two types of rotation methods, first are orthogonal rotations, that searches for a linear combination of factors such that the variance of the loadings are maximized. The other are oblique rotations, that allow the factors to take any position in the factorial space and thus allowing them to correlate to each other. Since the dimensions in our data are of related contruct, oblimin and promax rotations were used after factor extraction.

From a scree-plot I decided to extract four factors that could explain 47% of the variance. In order words, to reduce the dimensions from 25 to 4 we had to sacrifice 53% of the variability in the data. This is obviously going to effect the true structure of the data and “blur” some of the relationships but it’s the sacrifice we are willing to make in order to proceed the analysis.


### Factors interpretation

- Factor 1 are variables that accounts for profits, sales and spending habits
- Factor 2 accounts for wine-purchases and marketing campaigns and their success-rates
- Factor 3 is describing loyality, families and customers that shops online with discounted prices
- Factor 4 is describing a correlation only with market campagin 3, this seems to be an effect of removing potential multicollinearity between this campagin and the other four that could not be revealed in the original data

![factor_loadings](https://user-images.githubusercontent.com/96744665/148271998-55c60d04-77b3-4190-adb6-4584c0d81fcf.png)

***

## Clustering on factor scores

Five clusters seems to be the mest optimal given the silhouette scores for each cluster are above average and have the most unform sizes.

![silhouette_viz2](https://user-images.githubusercontent.com/96744665/148272055-a6b0c0e0-68de-4607-81a9-067487ece211.png)


## Redefining our clusters

- cluster 1 have very low spending habits and have not responded well to our market campaigns.
- Cluster 2 are high-income earners with high spending habits, no children or smaller families and did not respond well on market campagin three.
- Cluster 3 are families that preferebly shops online and on discounted products.
- Cluster 4 have the strongest spending habits and have responded very well to all market campagins.
- Cluster 5 are low-income earners and have weak spending habits but have responded particularly well to market campagin three. A further analysis is needed to find out what has been done different in this campaign and why it did so well in this cluster

![cluster_on_factors](https://user-images.githubusercontent.com/96744665/148272226-8aa0a92c-6ba7-4f79-b6d1-35e47d4e83d9.png)

***

## Conclusion
Clustering on the original data gave us very insightful and specific descriptions to each of the different segments which could led to more accurate marketing towards these groups.

On the other hand, the trade-off for 50% variance were greater and clearer seperation among clusters which gave more reliable but also generalized descriptions of the clusters, with less risk of overfitting the data.

In terms of the best method, it’s hard to say because they both have their pros & cons. A point that has not been covered in this article is the reproducibilty among the given clusters which could be further studied to determine the optimal method.
