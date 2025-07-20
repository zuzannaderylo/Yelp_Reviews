# Big Data Processing for Yelp Reviews Analysis

This project explores the Yelp Academic Dataset (6M+ reviews) using PySpark to perform large-scale data processing, text analysis, and machine learning. The goal is to understand how authenticity language is used in restaurant reviews, and to build a model that predicts review ratings.

## Repository Structure

| File | Description |
|------|-------------|
| `Assignment.ipynb` | Jupyter notebook with complete work for the assignment, including data exploration, text analysis, and ML model using PySpark |
| `README.md` | This file |

## Project Overview

- **Dataset**: [Yelp Academic Dataset](https://www.yelp.com/dataset) - includes business, user, and review data in JSON format (~6 million reviews total)
- **Goal**: Analyze the use of authenticity-related language in Yelp reviews across different cuisines and regions, and build a machine learning model to predict review ratings.
- **Techniques used**:
  - PySpark DataFrame Queries
  - Text Analysis
  - Statistical Analysis
  - Supervised Machine Learning (Spark MLlib)

## What I Did
The project was divided into three main sections:

### 1. Data Exploration & PySpark Queries
Using PySpark DataFrames, I wrote a series of queries to understand the structure and content of the Yelp dataset. These queries included:
- Counting the total number of reviews
- Finding businesses with 5-star ratings and at least 500 reviews
- Identifying “influencers” (users with more than 1000 reviews)
- Listing businesses reviewed by more than 5 influencers
- Calculating the average rating per user and sorting them by rating

### 2. Authenticity Language Analysis
In this section, I examined how authenticity-related words (e.g., “authentic”, “genuine”, “traditional”, “real”, “legitimate”) are used in reviews:
- Flagged reviews that contained any of the predefined authenticity terms
- Calculated the percentage of reviews containing such terms
- Grouped review content by cuisine type and geographic location (state and city) to analyze where and how often authenticity language was used
- Investigated how often authenticity terms co-occurred with negative sentiment words (e.g., “dirty”, “cheap”, “kitsch”, “simple”)
- For broader analysis, these cuisines were grouped into three regional clusters: Asian, South American, and European, to compare proportions of authenticity and negative sentiment language across regions
- Computed multiple ratios to assess patterns of sentiment and cultural bias

All text processing was done using PySpark string and filter operations. I used cube aggregation for multi-level grouping across cities and states.

### 3. Review Rating Prediction (Machine Learning)
For the final part, I trained a regression model to predict a review’s star rating using Spark MLlib:
- Engineered features based on review text, presence of authenticity and negative language, business attributes, and location
- Applied text tokenization and hashing for review content
- Used `StringIndexer` and `VectorAssembler` for building feature vectors
- Split the data into training and test sets
- Trained a Linear Regression model to predict star ratings
- Evaluated model performance using Root Mean Squared Error (RMSE)

⚠️ Note: The entire project was executed on UCloud, a high-performance computing platform that provided a ready-to-use Spark environment and access to the full Yelp dataset (~8 GB). The setup was given for me on Big Data Management Course. Running the notebook outside this environment may require substantial local configuration.

## Results Summary
- Approximately 23% of Yelp reviews contained authenticity-related terms
- Authenticity language appeared most frequently in reviews of specific cuisines such as Mexican, Italian, and Japanese
- The co-occurrence of authenticity and negative language was similarly distributed across Asian, South American, and European cuisines, suggesting no strong bias in this dataset
- A regression model was trained to predict review star ratings using Spark MLlib. It achieved a Root Mean Squared Error (RMSE) of approximately 3.19e-15, indicating an almost perfect fit on the test data

## Limitations
- The regression model achieved an extremely low RMSE (~3.19e-15), which may suggest data leakage or an overly simple modeling scenario. This result is likely not generalizable, and highlights the need for more robust data splitting and evaluation.
- Regression may not be the best modeling approach for this problem, since Yelp star ratings are discrete and ordinal. A classification model might better capture the structure of the target variable and provide more interpretable results.
- Authenticity-related language was identified using a manually curated list of keywords (e.g., “authentic”, “real”, “genuine”), which may have introduced both false positives and missed expressions of authenticity. For example, the word “real” might appear in neutral contexts like “real nice”..
- Negative sentiment detection also relied on a simple keyword list, which limits nuance and coverage. Some negative or sarcastic tones may not be captured by this approach.
- Cuisine categories were manually grouped into broad regional clusters (Asian, South American, European). This method may have missed specific cuisines or introduced categorization bias.
- The project was conducted in a distributed computing environment (UCloud), which included preloaded data and a configured Spark cluster. Reproducing the project locally requires extra setup and data handling.

## Future Improvements
- Implement a classification model (e.g., Logistic Regression or Random Forest) to predict star ratings more appropriately, using F1-score or accuracy as evaluation metrics.
- Use cross-validation and stricter train-test splitting methods to prevent data leakage and ensure fair model evaluation.
- Replace static keyword lists with more advanced NLP techniques.
- Automate cuisine grouping using business metadata or unsupervised clustering (e.g., topic modeling based on business names or categories) to avoid manual errors.
- Perform error analysis on the model predictions to understand where and why it fails - which could guide feature improvements.

This project was my first large-scale Spark analysis, so some modeling choices or assumptions may need refining in future iterations. Nonetheless, it reflects a solid starting point and working pipeline from data processing to prediction.

## Tools & Technologies
- Python
- Pandas, NumPy
- PySpark
- Spark MLlib
- Jupyter Notebook
- UCloud

## Author
**Zuzanna Emilia Derylo**  
📧 zuzia.derylo@gmail.com
🔗 [LinkedIn Profile](https://www.linkedin.com/in/zuzannaderylo/)
🔗 [GitHub Profile](https://github.com/zuzannaderylo)

---

*This project was part of a Big Data Management course at IT University of Copenhagen (2025).*
