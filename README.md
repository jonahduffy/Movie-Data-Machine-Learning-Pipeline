# Movie Data Machine Learning Pipeline

An end-to-end data engineering and machine learning pipeline that extracts NoSQL movie data to analyze the statistical relationship between professional critic scores and general audience reception. 

## Project Overview
This project investigates whether professional critic scores (Metacritic) are a statistically significant predictor of general audience reception (IMDB). Additionally, it deploys a Natural Language Processing (NLP) transformer model to analyze movie plot descriptions, highlighting the contextual biases present in sentiment analysis models trained on social media data.

### Key Objectives:
1. **Data Engineering:** Securely connect to a MongoDB Atlas cluster to extract and merge semi-structured datasets (`imdb` and `metacritic`).
2. **Statistical Modeling:** Perform an Ordinary Least Squares (OLS) regression analysis to quantify the variance in audience ratings.
3. **Machine Learning:** Utilize a Hugging Face neural network to classify the emotional sentiment of movie descriptions.

## Technology Stack
* **Database:** MongoDB Atlas, `pymongo`
* **Data Manipulation:** `pandas`
* **Statistical Analysis:** `statsmodels` (OLS Regression)
* **Machine Learning:** Hugging Face `transformers` (`twitter-xlm-roberta-base-sentiment`)
* **Data Visualization:** `matplotlib`, `seaborn`
* **Security:** `dotenv`, `certifi` (for secure SSL credential management)

## Key Insights & Findings

### 1. Regression Analysis: The Critic-Audience Gap
The OLS regression model mapped Metacritic scores against IMDB user ratings for the year 2015 ($n = 286$).
* **Results:** The model yielded an $R^2$ value of `0.528` and a p-value of `0.000`. 
* **Conclusion:** Critic scores are a highly statistically significant predictor of audience ratings. However, because critics only explain roughly 53% of the variance in audience reception, it is clear that general viewers evaluate films using additional metrics (e.g., franchise loyalty, genre appeal, visual spectacle) outside of traditional critical standards.

### 2. AI Sentiment Analysis: Contextual NLP Bias
The Hugging Face sentiment pipeline successfully processed the text descriptions of all movies in the dataset. However, the results revealed a fascinating limitation in deploying social media-trained NLP models on creative text.
* **Observation:** The model universally flagged highly-rated action and thriller films (such as *The Martian* and *Mad Max: Fury Road*) as having "Negative" sentiment.
* **Conclusion:** Because the model equates conflict-oriented vocabulary ("stranded," "wasteland," "assassin") with genuine negative hostility, it fundamentally misinterprets standard cinematic plot devices. This highlights the necessity of contextual model selection in machine learning deployments.

## Data Security Note
For security purposes, the database credentials and MongoDB connection URI used in this project are managed via hidden environment variables. If you are cloning this repository to run locally, you will need to provision your own MongoDB cluster and supply a local `.env` file containing your `MONGO_URI`.

---
**Author:** Jonah Duffy  
**Academic Focus:** Data Management and Analytics
