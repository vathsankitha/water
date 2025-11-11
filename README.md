WEEK 1

//TITLE:

"Water Usage Monitoring System"

//PROBLEM STATEMENT:

Many households and organisations do not have a systematic mechanism to monitor and analyse their water consumption.
Without regular tracking and alerts, excessive or inefficient usage goes unnoticed — resulting in water wastage, higher bills, potential leaks, and undermining sustainability efforts.

//PROPOSED SOLUTION:

Design a database‑driven system that:
Registers users (households or industries) with their details (user ID, name, address, type).
Logs water consumption records for each user on a daily/weekly/monthly basis (date, volume in litres).
Stores threshold guidelines for each user (e.g., expected monthly consumption for a household of X members).
Generates alerts when a user’s consumption exceeds the threshold (e.g., sends message, flags in system).
Supports queries and reporting such as:
Identify users who exceeded their threshold this month.
Trend of consumption per user (increasing/decreasing).
Comparison of consumption between users of the same type or region.
Helps users and administrators take action (e.g., detect leaks, encourage conservation behaviour, optimise usage).


WEEK 2

1. Data Overview and Summary Statistics:

What we did: We loaded the AguaH.csv dataset, inspected its general information (df.info()), viewed descriptive statistics (df.describe()), checked for missing values (df.isnull().sum()), and examined its shape.
Theory: This initial step is crucial for understanding the dataset's structure, data types, and identifying immediate issues like missing data or skewed distributions. df.info() provides insights into column types and non-null counts, while df.describe() offers statistical summaries (mean, std, min, max, quartiles) for numerical features, which helps in understanding their central tendency, spread, and potential outliers.
2. Exploratory Data Analysis (EDA) and Visualization:

What we did: We visualized the distributions of categorical columns (USO2013, TU, M) using bar plots and numerical columns (DC, UL, and selected f.1_ columns) using histograms and KDE plots.
Theory: EDA is about gaining insights into the data's characteristics. Visualizations help us:
Understand Distributions: Histograms and KDE plots show the frequency distribution of numerical variables, revealing their shape, center, and spread. This helps detect skewness, modality, and outliers.
Identify Patterns: Bar plots for categorical variables show the counts of each category. This helps understand the prevalence of different categories.
Legend Explanation: Labels and legends on plots ensure clarity, indicating what each element represents, which is vital for effective communication of findings.
3. Feature Engineering and Preprocessing:

What we did:
Created a copy of the DataFrame (df_processed).
Identified numerical (f.1_ columns, DC, UL) and categorical columns (USO2013, TU, M).
Imputed missing numerical values using the median. This is preferred over the mean for skewed data as it is less sensitive to outliers.
Imputed missing values in the categorical column 'M' using the mode (most frequent category), a standard practice for categorical imputation.
Applied one-hot encoding to categorical features, converting them into a numerical format suitable for machine learning models, specifically using drop_first=True to avoid multicollinearity.
Scaled numerical features using StandardScaler, which transforms data to have a mean of 0 and a standard deviation of 1. This is important for many ML algorithms (like those based on distance or gradients) as it prevents features with larger ranges from dominating the learning process.
Theory: This phase transforms raw data into a format suitable for machine learning. Key concepts include:
Missing Value Imputation: Handling missing data is critical to avoid errors or biased results. Median and mode imputation are simple, effective strategies when sophisticated methods aren't required.
Categorical Encoding: Machine learning models typically require numerical input. One-hot encoding converts categorical labels into a binary vector representation, preserving information without implying an ordinal relationship.
Feature Scaling: Scaling ensures that all features contribute equally to the model, preventing features with larger numerical values from disproportionately influencing results.
4. Model Selection and Training:

What we did:
Defined 'f.1_DIC_15' as the target variable (y) and the remaining columns as features (X).
Split the data into training (80%) and testing (20%) sets using train_test_split with random_state=42 for reproducibility.
Selected and trained a RandomForestRegressor model.
Theory:
Target and Features: Identifying the target variable is the foundation of supervised learning; features are the predictors.
Data Splitting: Splitting data into training and testing sets is fundamental to evaluate a model's generalization capability. The model learns from the training data and its performance is assessed on unseen test data to estimate how it will perform on new, real-world data.
RandomForestRegressor: This is an ensemble learning method that builds multiple decision trees during training and outputs the mean prediction of the individual trees. Its strengths include high accuracy, robustness to overfitting (due to averaging), and handling non-linear relationships. Setting n_jobs=-1 leverages all CPU cores for faster training, crucial for larger datasets.
5. Model Evaluation and Refinement:

What we did: We used the trained RandomForestRegressor to make predictions on the test set and evaluated its performance using Mean Absolute Error (MAE), Mean Squared Error (MSE), Root Mean Squared Error (RMSE), and R-squared (R2).
Theory: Evaluating a model is crucial to understand how well it performs. For regression tasks:
MAE: Measures the average magnitude of the errors in a set of predictions, without considering their direction. It's robust to outliers.
MSE & RMSE: Both penalize larger errors more significantly. RMSE is often preferred as it's in the same units as the target variable, making it more interpretable than MSE.
R-squared (R2): Represents the proportion of the variance in the dependent variable that is predictable from the independent variables. A higher R2 indicates a better fit, with a value of 1 meaning the model explains all the variance.
