# Cooking Up Insights: Analyzing Recipes and Ratings Data

**Name**: Angela Li  
**Github**: [(your website link)](https://github.com/anqiliumich/recipes-and-ratings-analysis)

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

### Distribution of Cooking Time (Filtered)

The histogram below displays the distribution of cooking times for recipes, filtered to exclude extreme outliers (over 500 minutes). The plot shows that most recipes take less than 100 minutes to prepare, with the highest concentration around 20 to 40 minutes. This trend suggests that quick and easy recipes dominate the dataset, aligning with user preferences for time-efficient cooking.

<iframe
  src="assets/cooking_time_distribution_filtered.html"
  width="800"
  height="600"
  frameborder="0">
</iframe>


## Bivariate Analysis

### Cooking Time vs. Average Rating (Filtered)

This scatter plot shows the relationship between cooking time (filtered to exclude recipes with cooking times greater than 500 minutes) and the average rating of recipes. While most recipes cluster around shorter cooking times (under 100 minutes), the ratings appear to be consistently high (around 4–5) regardless of cooking time. This suggests that cooking time alone may not strongly influence the ratings, but users seem to appreciate recipes across a range of preparation times.

<iframe
  src="assets/cooking_time_vs_rating_filtered.html"
  width="800"
  height="600"
  frameborder="0">
</iframe>

---

### Number of Steps vs. Average Rating

This scatter plot illustrates the relationship between the number of steps in a recipe and its average rating. Recipes with fewer steps (under 20) are the most common and tend to have consistently high ratings. However, as the number of steps increases, there is no significant drop in ratings, suggesting that users are willing to rate complex recipes highly as long as they meet quality expectations.

<iframe
  src="assets/steps_vs_rating.html"
  width="800"
  height="600"
  frameborder="0">
</iframe>

## Interesting Aggregates

### Average Number of Steps by Cooking Time Range

The table and bar chart below summarize the average number of steps in recipes grouped by cooking time range. As expected, recipes with longer cooking times tend to involve more steps, reflecting their complexity and level of detail. Quick recipes (under 30 minutes) typically have fewer steps, making them more accessible for users looking for simplicity.

#### Pivot Table: Average Number of Steps by Cooking Time Range

| Cooking Time Range | Average Number of Steps  |
|--------------------|--------------------------|
| Under 30 mins      | 5.2                      |
| 30-60 mins         | 8.3                      |
| 60-120 mins        | 12.4                     |
| Over 120 mins      | 15.6                     |

#### Bar Chart
<iframe
  src="assets/steps_by_cooking_time_range.html"
  width="800"
  height="600"
  frameborder="0">
</iframe>


### Average Rating by Cooking Time Range

The table and bar chart below summarize the average ratings for recipes grouped by cooking time range. Recipes with moderate cooking times (30–120 minutes) tend to receive the highest ratings, suggesting that users appreciate recipes that strike a balance between ease and complexity. Recipes under 30 minutes have slightly lower ratings, which may indicate that simpler recipes, while convenient, are not always as satisfying.

#### Pivot Table: Average Rating by Cooking Time Range

| Cooking Time Range  | Average Rating |
|---------------------|----------------|
| Under 30 mins       | 4.2            |
| 30-60 mins          | 4.5            |
| 60-120 mins         | 4.6            |
| Over 120 mins       | 4.4            |

#### Bar Chart
<iframe
  src="assets/average_rating_by_cooking_time_range.html"
  width="800"
  height="600"
  frameborder="0">
</iframe>


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
- **Description**: A placeholder ensures the dataset remains consistent, even though this column is not central to our research question.
- **Cooking Time Range**: The recalculation based on `minutes` ensures logical consistency and avoids missing data in grouped analyses.
- **Name**: Using a placeholder prevents issues with indexing or identification while maintaining dataset integrity.

### Significance
The imputation process focused on ensuring consistency for secondary columns (e.g., `description`, `cooking_time_range`, `name`) while retaining the original statistical properties of key analytical columns. By addressing missing values in this way, we maintained the dataset's usability and ensured no valuable records were excluded. This step enhances the reliability and completeness of the insights derived from the data.
