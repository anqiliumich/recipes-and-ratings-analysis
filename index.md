# Recipes and Ratings 🍽️

**Name**: Angela Li

**Website Link**: [Insert your website link here]

---

## Introduction

### Background
This dataset contains recipes and ratings scraped from **Food.com**, a popular online platform for sharing and discovering recipes. The dataset was originally collected for a recommender systems research paper and includes data spanning from 2008 onward. It offers a wealth of information, including recipe preparation details, nutritional values, and user feedback in the form of ratings and reviews.

The data is split into two parts:
1. **Recipes Dataset**:
   - Contains details about over 200,000 recipes, including preparation time, number of ingredients, steps, and nutritional information.
2. **Interactions Dataset**:
   - Includes over 1,000,000 user reviews and ratings, providing insights into recipe performance.

### Question
**What makes a recipe highly rated?**

This analysis aims to uncover the key features that contribute to a recipe's popularity, such as preparation time, number of ingredients, and cuisine type. The results can provide valuable insights for home cooks, recipe developers, and platforms like Food.com to optimize their content and recommendations.

### Why This Question Matters
Understanding what makes a recipe successful can:
- Help recipe developers craft more appealing recipes.
- Guide home cooks to create dishes that are well-received by others.
- Aid in building more effective recipe recommendation systems.

### Dataset Information
The dataset contains the following key columns:
- **Recipes Dataset**:
  - `name`: Recipe name.
  - `minutes`: Time required to prepare the recipe.
  - `tags`: Categories and attributes assigned to the recipe.
  - `nutrition`: List of nutritional values: calories, total fat, sugar, sodium, protein, saturated fat, and carbohydrates.
  - `n_steps`: Number of steps in the recipe.
  - `n_ingredients`: Number of ingredients in the recipe.
- **Interactions Dataset**:
  - `rating`: User rating for the recipe.

With this information, we aim to explore what makes recipes not only enjoyable but also successful in terms of user ratings.
