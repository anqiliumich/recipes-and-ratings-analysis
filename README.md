# Cooking Up Insights: Analyzing Recipes and Ratings Data

**Name**: Angela Li  
**Email**: anqili@umich.edu
**Github**: [(Click Me!)](https://github.com/anqiliumich/recipes-and-ratings-analysis)

---

## Introduction

### Background
This dataset contains recipes and ratings scraped from **Food.com**, a popular online platform for sharing and discovering recipes. The dataset was originally collected for a recommender systems research paper and includes data spanning from 2008 onward. It offers a wealth of information, including recipe preparation details, nutritional values, and user feedback in the form of ratings and reviews.

The data is split into two parts:
1. **Recipes Dataset**:
   - Contains details about recipes, including preparation time, number of ingredients, steps, and nutritional information.
2. **Interactions Dataset**:
   - Includes user reviews and ratings, providing insights into recipe performance.

---

### Question
**What factors influence the calorie content of recipes?**

This analysis seeks to identify key recipe attributes—such as preparation time, number of ingredients, and specific nutritional components—that affect the total calorie count of a recipe. By analyzing the relationship between these factors and calorie content, we can uncover trends that define high-calorie versus low-calorie recipes.

---

### Why This Question Matters
Understanding calorie content can:
- Help home cooks and recipe developers design meals that meet specific dietary goals.
- Inform users about which recipe attributes contribute to higher or lower calorie counts.
- Enhance recipe recommendation systems by including calorie considerations for health-conscious users.

---

### Dataset Information

The dataset contains the following key columns:

#### **Recipes Dataset**:
- **`name`**: Recipe name.
- **`minutes`**: Total time required to prepare the recipe.
- **`tags`**: Categories and attributes assigned to the recipe (e.g., "vegetarian", "low-calorie").
- **`nutrition`**: List of nutritional values: 
  - Calories
  - Total fat
  - Sugar
  - Sodium
  - Protein
  - Saturated fat
  - Carbohydrates.
- **`n_steps`**: Number of steps in the recipe preparation process.
- **`n_ingredients`**: Number of ingredients required for the recipe.

#### **Interactions Dataset**:
- **`recipe_id`**: Unique identifier for each recipe.
- **`rating`**: User-provided rating for the recipe (from 1 to 5).

---

### Brainstorming Questions

1. **What is the relationship between preparation time (`minutes`) and calories?**
   - Do quicker recipes (shorter preparation times) tend to have fewer calories?
   
2. **How does the number of ingredients (`n_ingredients`) correlate with calories?**
   - Do recipes with more ingredients generally have higher calorie counts?

3. **What types of recipes are the most calorie-dense?**
   - Analyze based on `tags` (e.g., "comfort food", "vegetarian", "low-calorie").

4. **Does recipe complexity (`n_steps`) influence calorie content?**
   - Are recipes with more steps (indicative of complexity) higher in calories?

5. **How do nutritional factors such as sugar, fat, or protein correlate with total calories?**
   - Explore the relationships between specific nutritional components and total calorie content.

6. **What is the distribution of calorie content across all recipes?**
   - Are recipes skewed toward lower calorie values, or is there a wide range of calorie counts?

---

# Data Cleaning and Exploratory Data Analysis

## Introduction

This section explores the cleaned dataset and key trends through univariate and bivariate visualizations. Missing values are addressed using imputation techniques, ensuring the dataset is consistent and complete for analysis.

---

## Data Cleaning

We performed the following data cleaning steps to prepare the dataset for analysis:

1. **Merged Datasets**:
   - Combined the `recipes` and `interactions` datasets using a left join to align recipe details with user ratings.

2. **Replaced Ratings of 0 with NaN**:
   - Ratings of 0 were treated as invalid or missing data, as they do not represent genuine user feedback. These were replaced with `NaN`.

3. **Calculated Average Ratings**:
   - Grouped user ratings to compute an average rating for each recipe, summarizing overall user satisfaction.

4. **Extracted Nutritional Information**:
   - Split the `nutrition` column into individual fields for calories, fat, sugar, sodium, protein, saturated fat, and carbohydrates, enabling finer-grained analysis.

5. **Imputed Missing Values**:
   - Filled missing values in nutritional columns and `average_rating` with their respective column means to retain all rows in the dataset.

### Cleaned Dataset Preview
Below is the head of the cleaned dataset:

| id  | name         | minutes | n_steps | n_ingredients | average_rating | calories | total_fat | sugar | sodium | protein | saturated_fat | carbohydrates |
|-----|--------------|---------|---------|---------------|----------------|----------|-----------|-------|--------|---------|---------------|----------------|
| 123 | Recipe Name1 | 25      | 6       | 8             | 4.5            | 250.0    | 8.0       | 5.0   | 300.0  | 10.0    | 2.5           | 35.0           |
| 456 | Recipe Name2 | 45      | 12      | 10            | 4.7            | 320.0    | 12.0      | 6.0   | 500.0  | 20.0    | 3.0           | 50.0           |

---

### Univariate Analysis

In this section, we analyze the distributions of key nutritional attributes, particularly focusing on **calories** and **sodium**, as these are directly relevant to our overarching question: "What factors influence the calorie content of recipes?"

---

#### Calories Distribution (Filtered)

The histogram below visualizes the calorie distribution after filtering extreme outliers (greater than the 99th percentile). The majority of recipes contain between 200 and 500 calories. There is a noticeable long tail for recipes with higher calorie counts, which likely represents more indulgent or complex dishes.

<iframe
  src="assets/calories_distribution_filtered.html"
  width="800"
  height="600"
  frameborder="0">
</iframe>

---

#### Sodium Distribution (Filtered)

The sodium content distribution reveals that most recipes fall under 50% of the daily recommended sodium intake (PDV%). A significant drop-off is observed as sodium content increases, suggesting that most recipes are designed to be moderate in sodium.

<iframe
  src="assets/sodium_distribution_filtered.html"
  width="800"
  height="600"
  frameborder="0">
</iframe>

---

### Insights

- **Calories**: Recipes with moderate calorie counts dominate the dataset, indicating a preference for balanced meals. This trend may reflect a user preference for recipes that are practical for everyday consumption.
- **Sodium**: Sodium levels are also relatively low in most recipes, suggesting a focus on health-conscious cooking.

These findings set the stage for further analysis into how various recipe attributes, such as ingredients and preparation methods, influence calorie content.


## Bivariate Analysis

### Calories vs. Total Fat (Filtered)
The scatter plot below shows the relationship between calories and total fat percentage (PDV%). A positive trend is visible, indicating that recipes with higher total fat content tend to have more calories. This is expected as fat is calorie-dense. This visualization answers our question about how nutritional attributes correlate with calorie counts, suggesting a direct relationship between fat content and caloric value.

<iframe
  src="assets/calories_vs_total_fat.html"
  width="800"
  height="600"
  frameborder="0">
</iframe>

---

### Calories by Number of Ingredients (Binned)
The box plot below displays the distribution of calorie counts across recipes grouped by the number of ingredients (binned). Recipes with more ingredients tend to have a higher median calorie count. However, the wide range of calories within each bin suggests that other factors also significantly contribute to caloric content.

<iframe
  src="assets/calories_by_num_ingredients.html"
  width="800"
  height="600"
  frameborder="0">
</iframe>

## Interesting Aggregates

### Average Nutritional Content by Number of Ingredients

The table below summarizes the average calories, protein, total fat, sugar, sodium, and carbohydrates grouped by the number of ingredients. Recipes with more ingredients tend to have higher nutritional values, reflecting the inclusion of richer or more diverse components.

| Ingredient Range   | Calories | Protein (PDV%) | Total Fat (PDV%) | Sugar (PDV%) | Sodium (PDV%) | Carbohydrates (PDV%) |
|--------------------|----------|----------------|------------------|--------------|---------------|----------------------|
| 0-5                | 336.71   | 20.33          | 24.43           | 81.00        | 24.29         | 11.77               |
| 6-10               | 401.71   | 30.60          | 30.62           | 62.85        | 26.68         | 12.87               |
| 11-15              | 495.22   | 40.73          | 37.71           | 69.68        | 32.11         | 15.62               |
| 16-20              | 601.77   | 52.93          | 47.01           | 73.56        | 42.27         | 17.95               |
| 21+                | 769.57   | 68.49          | 60.45           | 101.07       | 69.66         | 22.85               |

---

### Average Calories by Number of Ingredients

The pivot table below shows the average calories grouped by the number of ingredients. Recipes with more ingredients tend to have higher caloric values, likely reflecting the inclusion of richer and more varied components.

| Ingredient Range   | Calories |
|--------------------|----------|
| 0-5                | 336.71   |
| 6-10               | 401.71   |
| 11-15              | 495.22   |
| 16-20              | 601.77   |
| 21+                | 769.57   |


## Imputation of Missing Values

### Missing Values Overview
Before imputation, the dataset contained missing values in the following columns:
- **`description`**: Missing descriptions likely occurred during data collection or due to incomplete user submissions.
- **`cooking_time_range`**: Missing values were due to an incomplete derivation process based on `minutes`.
- **`name`**: A single recipe was missing a name, potentially due to a data entry error.

The table below summarizes the number of missing values before and after imputation:

| Column              | Missing Before Imputation | Missing After Imputation |
|---------------------|---------------------------|--------------------------|
| `description`       | 70                        | 0                        |
| `cooking_time_range`| 1                         | 0                        |
| `name`              | 1                         | 0                        |

### Imputation Technique
- For **`description`**, missing values were replaced with the placeholder `"No description provided"`. Since this column is not central to our analysis, this ensures consistency without affecting results.
- For **`cooking_time_range`**, missing values were recalculated based on the `minutes` column. This derived column is important for grouped analysis, and the imputation ensures its completeness.
- For **`name`**, the missing value was replaced with the placeholder `"Unknown Recipe"`. As this column is primarily used for recipe identification and not analysis, this imputation prevents issues without impacting outcomes.

### Visualization: Cooking Time Range Distribution After Imputation
The bar chart below displays the distribution of recipes by `cooking_time_range` after imputation. The imputation step ensured that all recipes were categorized into appropriate cooking time ranges based on their preparation time. This step was crucial for grouped analyses in later sections.

<iframe
  src="assets/cooking_time_range_distribution.html"
  width="800"
  height="600"
  frameborder="0">
</iframe>

### Justification for Imputation Technique
Imputation was applied selectively:
1. For variables directly related to calories (e.g., nutritional columns), imputation was unnecessary since there were no missing values.
2. Other imputations ensured the dataset’s usability but were not critical to answering our main research question.
- **Description**: A placeholder ensures the dataset remains consistent, even though this column is not central to our research question.
- **Cooking Time Range**: The recalculation based on `minutes` ensures logical consistency and avoids missing data in grouped analyses.
- **Name**: Using a placeholder prevents issues with indexing or identification while maintaining dataset integrity.

# Framing a Prediction Problem
The goal of this analysis is to **predict the calorie count** of recipes based on their nutritional components.

### Problem Type
This is a **regression problem**, as the target variable (`calories`) is continuous.

### Features and Target
- **Target Variable**: `calories` (measured as a continuous numerical value).
- **Features**:
  - `protein`: Protein content as a percentage of the daily value (PDV%).
  - `total_fat`: Total fat content as a percentage of the daily value (PDV%).
  - `sugar`: Sugar content as a percentage of the daily value (PDV%).
  - `sodium`: Sodium content as a percentage of the daily value (PDV%).
  - `carbohydrates`: Carbohydrate content as a percentage of the daily value (PDV%).

### Justification
- **Regression Problem**: The target variable `calories` is continuous.
- **Relevance**: The selected features directly relate to key nutritional factors influencing calorie content.
- **Availability**: These features are always available at the time of prediction, as they are derived from a recipe’s nutritional breakdown.

### Dataset Shape
The dataset includes **83,782 recipes** and the following features:
- Target: `calories`
- Predictors: `protein`, `total_fat`, `sugar`, `sodium`, `carbohydrates`.

### Evaluation Metrics
To evaluate the predictive model’s performance, we will use:
1. **Root Mean Squared Error (RMSE)**:
   - Provides a sense of overall prediction error, weighted more towards larger errors.
2. **Mean Absolute Error (MAE)**:
   - Offers insight into the average error magnitude.
3. **R² Score**:
   - Explains the proportion of variance in calorie count that can be predicted by the selected features.

## Baseline Model

### Model Description

The baseline model is a **Linear Regression model** designed to predict the calorie content of a recipe based on simple nutritional information. This model utilizes two **quantitative features** that are directly related to calories: sugar content and sodium content.

#### **Features in the Model**
1. **Quantitative Features**:
   - `sugar`: Sugar content in Percent Daily Value (PDV%).
   - `sodium`: Sodium content in PDV%.
   - Both features are numerical, requiring no special encoding but requiring preprocessing for scaling.

2. **Ordinal Features**:
   - None.

3. **Nominal Features**:
   - None.

4. **Target Variable**:
   - `calories`: Calorie content, the response variable, measured as a continuous numerical value.

### Preprocessing Steps

- **Imputation**: Missing values in `sugar` and `sodium` were handled using the mean imputation strategy to avoid issues with incomplete data.
- **Scaling**: Both features were standardized using `StandardScaler` to ensure they were on comparable scales, as linear regression can be sensitive to the magnitude of features.

### Model Implementation

The preprocessing steps (imputation and scaling) and model training were implemented using a single `sklearn` pipeline for streamlined reproducibility. The data was split into training (80%) and testing (20%) sets to evaluate the model’s ability to generalize to unseen data.

### Model Performance

The model's performance was evaluated using the following metrics:

1. **Root Mean Squared Error (RMSE)**:
   - Train RMSE: **466.84**
   - Test RMSE: **425.44**
   - **Interpretation**: The model’s predictions deviate significantly from actual calorie values, indicating that this simple model struggles to capture the variance in calorie content.

2. **R² Score (Coefficient of Determination)**:
   - Train R²: **0.4797**
   - Test R²: **0.4840**
   - **Interpretation**: The model explains only ~48% of the variance in calorie values, leaving over half of the variance unexplained.

### Is This a Good Baseline Model?

This is a **poor baseline model**, as it underperforms in both explanatory power (R²) and prediction accuracy (high RMSE). The low R² score suggests that the features chosen (`sugar` and `sodium`) are insufficient to predict calories effectively on their own.

However, as a baseline model, it provides:
- A **starting point** for improvement.
- A **benchmark** against which more complex models can be evaluated.

### Opportunities for Improvement

1. Introduce additional features, such as fat and carbohydrates, to improve predictive performance.
2. Explore feature engineering to derive new variables, such as the ratio of sugar to sodium, or transformations to normalize skewed distributions.
3. Investigate non-linear models, such as Random Forests or Gradient Boosting, which may better capture complex relationships between features and calories.

## Final Model

### Model Description
The final model is designed to predict the calorie content of recipes using nutritional information and engineered features. This model builds upon the baseline model by incorporating additional features and using a more advanced algorithm with hyperparameter tuning to improve predictive performance.

#### Features in the Model
1. **Quantitative Features**:
   - `protein`: Protein content in PDV% (Percent Daily Value).
   - `total_fat`: Total fat content in PDV%.
   - `sugar`: Sugar content in PDV%.
   - `sodium`: Sodium content in PDV%.
   - `carbohydrates`: Carbohydrate content in PDV%.
2. **Engineered Features**:
   - `protein_fat_ratio`: The ratio of protein to fat in a recipe. This feature captures the balance between macronutrients, which influences calorie content.
   - `log_sodium`: The logarithmic transformation of sodium content. This feature accounts for diminishing effects of sodium at higher levels and makes the data more normally distributed.
3. **Target Variable**:
   - `calories`: Calorie content, the response variable, measured as a continuous numerical value.

### Preprocessing and Modeling Algorithm
- **Preprocessing**:
  - **Scaling**: `StandardScaler` was applied to the quantitative features to ensure uniform scaling for the model.
  - **Quantile Transformation**: `QuantileTransformer` was used on the engineered features (`protein_fat_ratio` and `log_sodium`) to normalize their distributions.
  - **Imputation**: Missing values were imputed using the mean strategy.
- **Modeling Algorithm**:
  - **XGBoost**: A gradient-boosted decision tree model was chosen for its ability to handle non-linear relationships and interactions between features. The model was trained using GPU acceleration (`tree_method='hist'`) for efficiency.
  - **Hyperparameter Tuning**: A grid search with cross-validation was conducted to optimize key hyperparameters:
    - `n_estimators`: Number of trees.
    - `learning_rate`: Step size shrinkage to prevent overfitting.
    - `max_depth`: Maximum depth of a tree.
    - `subsample`: Fraction of samples used for training each tree.

### Best Hyperparameters
After grid search, the best parameters were:
- `n_estimators`: 200
- `learning_rate`: 0.2
- `max_depth`: 5
- `subsample`: 0.8

### Model Performance

| Metric          | Training Set | Test Set  |
|-----------------|--------------|-----------|
| **RMSE**        | 61.0425      | 180.7139  |
| **R² Score**    | 0.9911       | 0.9069    |

- The **Final Model** demonstrates significant improvement over the **Baseline Model**, with higher R² scores and lower RMSE values on both the training and test sets. This improvement is attributed to the inclusion of engineered features and the use of a more sophisticated algorithm.

### Why These Features Are Good for Prediction
- **Protein and Fat Balance**: The `protein_fat_ratio` directly relates to calorie computation since calories are derived from macronutrients.
- **Log Transformation**: The `log_sodium` feature accounts for diminishing returns in sodium's contribution to calorie differences, reflecting real-world patterns in recipes.

### Visualization of Model Performance
Below is a scatter plot showing the predicted vs. actual calorie values for the test set:

<iframe
  src="assets/predicted_vs_actual_calories_plot.html"
  width="800"
  height="600"
  frameborder="0">
</iframe>

This visualization illustrates the model's accuracy, with points clustering around the diagonal line (`y = x`), indicating strong predictive performance.

### Conclusion
The final model effectively predicts calorie content, significantly outperforming the baseline model. By leveraging feature engineering, advanced modeling techniques, and hyperparameter optimization, this model achieves robust performance while maintaining interpretability.

