## Ranking-Oriented Product Recommendations

**Core Goal:** Identify products with a substantial count of ratings, focusing on popular choices for new customers, and addressing the 'Cold Start' challenge.

**Outputs:** Recommend the top 5 products with a minimum of 50 or 100 ratings/interactions.

**Approach:**
1. Calculate the average rating for each product.
2. Count the overall ratings for each product.
3. Construct a DataFrame using these metrics and organize it by average rating.
4. Develop a function to extract the top 'n' products with a specified minimum number of interactions.

## Collaborative Filtering Based on Similarity

**Principal Aim:** Deliver personalized and relevant recommendations to users.

**Outputs:** Suggest the leading 5 products based on interactions of similar users.

**Approach:**
1. Transform user IDs into values from 0 to 1539 for simplicity.
2. Craft a function to find analogous users:
   - Compute the similarity score between the target user and each user using cosine_similarity, then sort the scores.
   - Extract the analogous user IDs and their similarity scores, excluding the original user.
3. Develop a function to generate user recommendations:
   - Use the previous function to obtain comparable users for the specified user ID.
   - Retrieve product IDs associated with the original user's interactions (observed_interactions).
   - For each similar user, identify 'n' products they've interacted with but the original user hasn't, thus offering recommendations.

## Model-Driven Collaborative Filtering

**Core Objective:** Provide tailored recommendations based on user history while addressing sparsity and scalability challenges.

**Outputs:** Suggest the top 5 products for a specific user.

**Approach:**
1. Transform the product ratings matrix into a compressed sparse row (CSR) matrix for efficiency.
2. Apply singular value decomposition (SVD) to the CSR matrix, reducing it to 50 latent features.
3. Compute projected ratings for all users using SVD (U matrix, sigma matrix, and Vt matrix).
4. Store the predicted ratings in a DataFrame mirroring the original matrix.
5. Develop a function to recommend products based on rating predictions:
   - Retrieve the user's ratings from the interactions_matrix.
   - Obtain the user's predicted ratings from the preds_matrix.
   - Create a DataFrame with actual and predicted ratings, including product names.
   - Filter the DataFrame to include unrated products.
   - Sort the DataFrame by predicted ratings in descending order.

**Model Evaluation:**
1. Compute the mean rating for all products and predicted ratings.
2. Assemble an RMSE_df DataFrame with average actual and projected ratings.
3. Calculate the RMSE by taking the square root of the mean squared errors between average actual and projected ratings. The squared parameter within the mean_squared_error function controls whether to output RMSE.
