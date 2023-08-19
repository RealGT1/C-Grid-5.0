# Ecommerce-product-recommendation-system

The Ecommerce Product Suggestion System is a sophisticated project that harnesses the power of machine learning to deliver tailor-made product recommendations to users based on their interaction history. By incorporating cutting-edge collaborative filtering and content-based filtering algorithms, this system dissects user behaviors and preferences, generating spot-on suggestions that heighten user satisfaction and drive up sales for e-commerce enterprises.

## Dataset

To uphold objectivity and circumvent any potential biases, the utilized dataset comprises Amazon's electronic product ratings. The dataset is intentionally stripped of headers, employing unique identifiers for both products and users to eliminate any prejudiced information.


## Approach

1) Ranking-Oriented Product Recommendations
Core Goal:

Identify products with the most substantial count of ratings.
Direct attention towards popular products for new customers.
Mitigate the 'Cold Start' predicament.
Outputs:

Suggest the foremost 5 products with a minimum of 50 or 100 ratings/interactions.
Approach:

Calculate the average rating for each product.
Tally the overall count of ratings for each product.
Construct a DataFrame using these metrics and arrange it based on the average rating.
Devise a function to extract the top 'n' products with a specified minimum number of interactions.


2) Collaborative Filtering Based on Similarity
Principal Aim:

Furnish users with personalized and pertinent recommendations.
Outputs:

Propose the leading 5 products grounded on interactions of akin users.
Approach:

Transform user IDs into values from 0 to 1539 (integer format) for convenience.
Craft a function to ascertain analogous users:
Compute the similarity score between the target user and each user in the interaction matrix using cosine_similarity; subsequently, catalog the scores and sort them.
Isolate the analogous user IDs and their associated similarity scores from the ranked list.
Exclude the original user and its corresponding similarity score, retaining the rest for analysis.
Develop a function for generating user recommendations:
Invoke the earlier function to acquire comparable users for the specified user ID.
Retrieve the product IDs associated with the original user's interactions (observed_interactions).
For each similar user, identify 'n' products they've interacted with but the original user hasn't, subsequently presenting these products as recommendations.

3) Model-Driven Collaborative Filtering
Core Objective:

Provide individualized recommendations based on user history, tackling the sparsity and scalability challenges that conventional collaborative filtering can encounter.
Outputs:

Suggest the finest 5 products for a specific user.
Approach:

Transform the matrix of product ratings into a compressed sparse row (CSR) matrix, enhancing memory efficiency by storing only non-zero values.
Perform singular value decomposition (SVD) on the CSR matrix, a dimensionality reduction technique that condenses the product ratings matrix into 50 latent features.
Compute projected ratings for all users via SVD, obtained by multiplying the U matrix, sigma matrix, and Vt matrix.
Capture the anticipated ratings within a DataFrame mirroring the original product ratings matrix. Users are represented in rows, while columns correspond to products; the DataFrame values indicate predicted ratings.
Construct a function to recommend products rooted in rating forecasts:
Retrieve the user's ratings from the interactions_matrix.
Acquire the user's projected ratings from the preds_matrix.
Construct a DataFrame incorporating both actual and anticipated ratings.
Incorporate a column for product names in the DataFrame.
Filter the DataFrame to encompass products the user hasn't yet rated.
Sort the DataFrame in descending order by predicted ratings.
Showcase the top num_recommendations products.

Model Evaluation:
Compute the mean rating for all products by dividing the aggregate rating sum by the total number of ratings.
Calculate the average rating for predicted ratings in a parallel manner.
Assemble an RMSE_df DataFrame containing mean actual and projected ratings.
Derive the root mean squared error (RMSE) of the SVD model by extracting the square root of the mean squared errors between average actual and projected ratings.
The squared parameter within the mean_squared_error function determines whether to output mean squared error (MSE) or RMSE. By setting squared to False, the function returns the RMSE, which entails squaring errors, averaging them, and finally taking the square root for RMSE computation.
