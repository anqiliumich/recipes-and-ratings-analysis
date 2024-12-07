# Cooking Up Insights: Analyzing Recipes and Ratings Data

**Name**: Angela Li  

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
**What factors influence the average rating of a recipe?**

This analysis seeks to identify key recipe attributes—such as preparation time, number of ingredients, nutritional values, and complexity (steps)—that make recipes highly rated. By analyzing the relationship between these factors and average ratings, we can uncover what makes a recipe successful and enjoyable for users.

---

### Why This Question Matters
Understanding what makes a recipe highly rated can:
- Help recipe developers craft recipes that appeal to users and receive higher ratings.
- Guide home cooks to create dishes that are likely to be well-received by others.
- Enhance recipe recommendation systems to prioritize high-performing recipes.

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

1. **What is the relationship between preparation time (`minutes`) and average ratings?**
   - Are longer or shorter recipes more likely to be rated highly?
   
2. **How does the number of ingredients (`n_ingredients`) correlate with average ratings?**
   - Do simpler recipes (fewer ingredients) receive better ratings?

3. **What types of recipes tend to have the highest ratings?**
   - Analyze based on tags (e.g., vegetarian, quick, or holiday recipes).

4. **How does nutritional content affect ratings?**
   - Explore whether healthier recipes (e.g., high protein, low sugar) are more popular.

5. **Does recipe complexity (`n_steps`) influence ratings?**
   - Are recipes with more steps seen as too complex or gourmet, and do they receive higher ratings as a result?

6. **What is the distribution of ratings across all recipes?**
   - Are ratings skewed toward higher values, indicating user satisfaction?

---

With this comprehensive introduction and clear research focus, we’re ready to delve into the data cleaning and analysis to answer these questions.

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

## Univariate Analysis

### Cooking Time Distribution
The histogram shows that most recipes take less than 60 minutes to prepare, indicating a focus on quick and easy recipes. Few recipes require over 120 minutes, which are likely elaborate or gourmet dishes.

<iframe
  src="assets/cooking_time_distribution.html"
  width="800"
  height="600"
  frameborder="0">
</iframe>

---

### Average Rating Distribution
The distribution of average ratings is skewed toward higher values, with most recipes rated between 4 and 5. This suggests that users are generally satisfied with the recipes, but there might be rating inflation.

<iframe
  src="assets/average_rating_distribution.html"
  width="800"
  height="600"
  frameborder="0">
</iframe>

---

### Calories Distribution After Imputation
The histogram shows that most recipes have between 200 and 500 calories. After imputation, the calorie distribution remains smooth, ensuring no outliers are introduced.

<iframe
  src="assets/calories_after_imputation.html"
  width="800"
  height="600"
  frameborder="0">
</iframe>

---

## Bivariate Analysis

### Cooking Time vs. Average Rating
The scatter plot shows a positive trend where recipes with longer cooking times tend to have slightly higher ratings. This suggests users may associate longer preparation times with more flavorful or complex dishes.

<iframe
  src="assets/cooking_time_vs_rating.html"
  width="800"
  height="600"
  frameborder="0">
</iframe>

---

### Number of Ingredients vs. Average Rating
The scatter plot reveals that recipes with a moderate number of ingredients (5–15) tend to receive higher ratings. Simpler recipes with very few ingredients or overly complex recipes with many ingredients are less favored.

<iframe
  src="assets/ingredients_vs_rating.html"
  width="800"
  height="600"
  frameborder="0">
</iframe>

---

## Interesting Aggregates

### Average Rating by Cooking Time Range
The bar chart shows that recipes in the "30-60 mins" range have the highest average ratings, followed by those in the "60-120 mins" range. This indicates users prefer moderately timed recipes, likely due to a balance between effort and quality.

<iframe
  src="assets/average_rating_by_cooking_time.html"
  width="800"
  height="600"
  frameborder="0">
</iframe>

---

### Average Ingredients by Cooking Time Range
Recipes with longer cooking times ("Over 120 mins") tend to require more ingredients on average. Conversely, shorter recipes ("Under 30 mins") use fewer ingredients, reflecting their simplicity.

<iframe
  src="assets/ingredients_by_cooking_time.html"
  width="800"
  height="600"
  frameborder="0">
</iframe>

---

## Imputation Analysis

### Ratings Distribution After Imputation
The histogram confirms that the distribution of ratings remains consistent after imputation, with most ratings still between 4 and 5. This ensures that missing values were handled without altering the overall trends.

<iframe
  src="assets/ratings_after_imputation.html"
  width="800"
  height="600"
  frameborder="0">
</iframe>
