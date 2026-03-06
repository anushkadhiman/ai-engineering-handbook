1. What Is Machine Learning?

- learning patterns from data
- without explicit rule-based programming
- uses statistical models + optimization
- trained using loss minimization
- generalizes to unseen data

2. Applications of Machine Learning
   - Analyzing images of products on a production line to automatically classify them
   - Detecting tumors in brain scans: semantic image segmentation problem
   - Automatically classifying news articles: natural language processing (NLP) problem
   - Automatically flagging offensive comments on discussion forums: text classification, using the NLP tools.
   - Summarizing long documents automatically
   - Creating a chatbot or a personal assistant
   - Forecasting your company’s revenue next year, based on many performance metrics: This is a regression task (i.e., predicting values)
   - Detecting credit card fraud: This is anomaly detection, which can be tackled using isolation forests, Gaussian mixture models, or autoencoders
   - Segmenting clients based on their purchases so that you can design a different marketing strategy for each segment: This is clustering, which can be achieved using k-means, DBSCAN, and more.
   - Representing a complex, high-dimensional dataset in a clear and insightful diagram: This is data visualization, often involving dimensionality reduction techniques.
   - Recommending a product that a client may be interested in, based on past purchases: This is a recommender system.

3. Types of Machine Learning Systems
   - Supervised Learning: The model is trained on labeled data (input-output pairs) to make predictions.
   - Unsupervised Learning: The model identifies patterns and structures in unlabeled data without predefined outcomes.
   - Semi-Supervised Learning: This approach uses a small amount of labeled data in combination with a large amount of unlabeled data.
   - Self-supervised learning: This is a subset of unsupervised learning creates its own supervisory signals (labels) from unlabeled data by solving "pretext tasks" like predicting missing parts.
   - Reinforcement Learning: An agent learns to make decisions through trial and error by interacting with an environment and receiving rewards or penalties.

4. Supervised Learning
   - Classification: Predicts a discrete category or class label. Examples: Detecting spam in emails, medical diagnosis, and image recognition.
   - Regression: Predicts a continuous numerical value. Examples: Forecasting stock prices, predicting house prices, and weather forecasting.

5. Unsupervised Learning
   - Clustering: Groups similar data points into clusters based on shared attributes. Examples: Customer segmentation for marketing, social network analysis, and image compression.
   - Dimensionality Reduction: Reduces the number of features in a dataset while preserving essential information to make the data more manageable and easier to visualize. Examples: Data visualization, and reducing genetic variables in bioinformatics.
   - Association: Discovers rules that describe large portions of the data. Examples: Market basket analysis to identify products frequently bought together, like purchasing bread and butter.

6. Batch learning and Online learning
   - Batch learning trains models on the entire dataset at once, making it ideal for stable, offline data, but it requires full retraining for updates.
   - Online learning trains incrementally on data streams (individually or mini-batches), allowing for real-time adaptation, lower memory usage, and continuous improvement without retraining from scratch. However, susceptible to "catastrophic interference" (forgetting old patterns); harder to maintain.

7. Instance based vs Model based learning
   - Instance-based learning (e.g.,k-NN) memorizes training data and makes predictions based on similarity to new inputs, functioning as "lazy" learning, ideal for small, dynamic datasets.
   - Model-based learning (e.g., linear regression) trains a model to generalize patterns from data, resulting in faster, more efficient predictions for large, static datasets.

8. Main Challenges of Machine Learning
   - Data Issues: Poor quality, insufficient data, or lack of diversity causing bias.
   - Overfitting/Underfitting: Models either failing to learn patterns (underfitting) or memorizing noise (overfitting), leading to poor performance on new data.
   - Scalability and Resources: High computational costs and difficulty scaling models for large, real-time datasets.
   - Interpretability: Difficulty in explaining how complex "black box" models make decisions, crucial for trust in industries like healthcare.
   - Data Security and Privacy: Protecting sensitive data used for training.
   - Feature Engineering: The time-intensive process of selecting relevant data features.

9. Training, Testing and Validation dataset
   - data is divided into three distinct sets, each serving a specific purpose in building and evaluating a reliable model; helps ensure the model generalizes well to new, unseen data and prevents common issues like overfitting.
   - Training Set: the largest portion of the dataset, the model uses to learn patterns and relationships. During training, the algorithm repeatedly adjusts its internal parameters (like weights in a neural network) to minimize errors based on this data. A diverse training set is crucial for effective learning.
   - Validation Set: used during the model development phase to provide an unbiased evaluation of the model's performance while fine-tuning its hyperparameters (e.g., the learning rate or number of layers), helping in model selection and serving as an early stopping signal to prevent overfitting to the training data.
   - Test Set: This is a completely separate, "held-out" portion of the data used only once at the very end of the process to assess the final, tuned model's performance on truly unseen data; provides the most reliable estimate of the model's real-world generalization ability.

10. Hyperparameter Tuning and Model Selection
    - are critical steps for building robust machine learning models by identifying the best algorithm and optimizing settings that control the learning process. Selection involves comparing models (e.g., SVM, Random Forest) via cross-validation, while tuning adjusts parameters like learning rate or regularization to minimize error, prevent overfitting, and improve performance.
    - For model selection: Evaluate models based on performance metrics (e.g., accuracy, precision, F1-score, AUC-ROC); use cross-validation (e.g., k-fold) to avoid overfitting and ensure generalization; balance model complexity with interpretability and avoid choosing a model that is too simple (underfitting) or too complex (overfitting).
    - For Hyperparameter Tuning: Use techniques like Grid Search: Exhaustively searches through a predefined subset of hyperparameters; Random Search: Randomly samples combinations of hyperparameters, often faster than grid search; Bayesian Optimization: A probabilistic model to find the best hyperparameters, often more efficient than grid/random search.

11. What is end-to-end machine learning (ML) project?
    - Problem Definition and Planning:
      Define the Business Problem: Clearly understand the objective (e.g., predicting customer churn, detecting fraud) and the value the solution will provide.
      Establish Metrics: Agree on both model performance metrics (e.g., accuracy, F1 score, RMSE) and business metrics (e.g., cost savings, customer satisfaction).
    - Data Engineering:
      Data Collection/Ingestion: Gather raw data from various sources (databases, APIs, logs).
      Data Cleaning and Validation: Handle missing values, remove duplicates, and check for data quality issues and outliers.
      Exploratory Data Analysis (EDA): Analyze data to understand patterns, relationships, and anomalies, often using visualizations like histograms and correlation heatmaps.
      Data Preprocessing and Feature Engineering: Transform the data into a machine-friendly format, which may involve scaling, encoding categorical variables, or creating new features. The processed data is then split into training, validation, and test sets.
    - ML Model Engineering:
      Model Training and Selection: Choose and train suitable algorithms based on the problem and data characteristics (e.g., Linear Regression, Random Forest, Neural Networks).
      Hyperparameter Tuning: Optimize model performance by finding the best configuration parameters (hyperparameters).
      Model Evaluation: Assess the model's performance on unseen validation data using the predefined metrics to ensure it generalizes well and meets objectives.
      Model Packaging and Registration: Save the final model (e.g., using pickle or joblib) and its metadata into a model registry for versioning and later use.
    - Deployment and MLOps:
      Model Deployment: Integrate the model into the production environment so it can handle real-time or batch prediction requests. Common methods involve containerization (using Docker) and cloud platforms like AWS SageMaker.
      Monitoring and Maintenance: Continuously track the model's performance in production to detect issues like data or model drift. Use feedback loops to trigger model retraining as needed.
      Automation (CI/CD/CT): Implement continuous integration, delivery, and training pipelines to automate the workflow and ensure reproducibility and efficiency.

12. Classification in machine learning:
    - a supervised learning technique that categorizes input data into predefined classes or labels based on training examples. By learning relationships between input features and target outcomes, models predict categorical labels for new data, such as distinguishing "spam" from "not spam".
    - Types of Classification:
      Binary: Two possible classes (e.g., Yes/No, Spam/Ham).
      Multiclass: More than two classes (e.g., classifying images as cat, dog, or bird).
      Multilabel: Each input can be assigned multiple labels.
      Ordinal: Classes have a specific order or rank
    - Common Classification Algorithms: Logistic Regression (used for binary classification), Decision Trees, Random Forest, Support Vector Machines (SVM), K-Nearest Neighbors (KNN), Naive Bayes
    - Real-World Applications: Spam Detection: Filtering emails; Healthcare: Disease diagnosis or patient risk identification; Image Recognition: Identifying objects in photos; Fraud Detection: Identifying fraudulent bank transactions; Sentiment Analysis: Determining if text is positive, negative, or neutral.
13. Performance metrics in machine learning:
    - are quantitative measures used to evaluate, compare, and optimize model effectiveness, ensuring they generalize well to new data.
    - Key metrics include accuracy, precision, recall, and F1-score for classification, and mean squared error (MSE) or root mean squared error (RMSE) for regression.
    - Key Classification Metrics:
      Accuracy: The ratio of correctly predicted observations to the total observations.
      Precision: The ratio of correctly predicted positive observations to total predicted positives, critical when false positives are costly.
      Recall (Sensitivity): The ratio of correctly predicted positive observations to all actual positives.
      F1-Score: The harmonic mean of precision and recall, useful for imbalanced datasets.
      Confusion Matrix: A table summarizing true positives, true negatives, false positives, and false negatives.
      ROC-AUC: Measures the ability of a binary classifier to distinguish between classes across thresholds.
    - Key Regression Metrics
      Mean Absolute Error (MAE): Average of the absolute differences between predicted and actual values.
      Mean Squared Error (MSE): Average of the squared differences, heavily punishing large errors.
      Root Mean Squared Error (RMSE): The square root of MSE, providing error in the same unit as the target variable.
    - Choosing the Right Metric: Balanced Data: Accuracy is often sufficient; Imbalanced Data: Use Precision, Recall, F1-Score, or AUC-ROC; Regression: Use RMSE or MAE based on whether large errors need to be heavily penalized (RMSE) or not (MAE).
14. Precision-Recall Curve:
    - It visualizes the trade-off between precision (exactness) and recall (completeness) for binary classifiers at various decision thresholds. As the threshold changes, increasing precision typically lowers recall (fewer false positives, more false negatives), and vice versa. It is crucial for imbalanced datasets, where a higher curve towards the top-right indicates superior model performance.
    - Axes: Recall is typically plotted on the x-axis, and Precision is on the y-axis.
    - Trade-off Behavior: A model with high precision usually has low recall, while a model with high recall often has lower precision. The curve helps determine the best threshold for a specific use case (e.g., maximizing precision for spam detection or maximizing recall for disease detection).
    - Imbalanced Data: Unlike the ROC curve, the PR curve is better suited for datasets where the positive class is rare, as it ignores the number of true negatives.
    - AUC-PR (Area Under the Curve): The area under the PR curve, or the Average Precision (AP), provides a single metric to summarize the classifier's performance, ranging from 0 to 1.
    - Ideal Classifier: An ideal model plots a curve that reaches the top-right corner (100% recall, 100% precision).
    - Model Comparison: It allows for comparing different models to see which offers a better balance for specific requirements.
    - Threshold Optimization: It helps visualize the impact of changing the decision threshold on the trade-off between false positives and false negatives.
    - Performance Visualization: The curve provides a comprehensive view of performance, especially when accuracy is misleading due to class imbalance.
15. ROC curve:
    - A Receiver Operating Characteristic (ROC) curve is a graphical plot that illustrates the diagnostic ability of a binary classifier across all threshold levels. It plots the True Positive Rate (Sensitivity) on the y-axis against the False Positive Rate (1 - Specificity) on the x-axis, providing a comprehensive visualization of the trade-off between sensitivity and specificity.
    - Ideal Performance: The curve should bend towards the top-left corner, indicating high sensitivity and low false positive rate.
    - AUC (Area Under the Curve): A scalar value ranging from 0 to 1 that summarizes the model's performance; higher values indicate better classifier performance.
    - Random Guessing: Represented by a 45-degree diagonal line (AUC = 0.5).
    - Threshold Independence: The ROC curve shows performance across all possible classification thresholds.
    - Applications: Commonly used in machine learning for binary classification, medical diagnostics, and signal detection.
    - An AUC of 1.0 represents a perfect model, while an AUC of 0.5 indicates a model that performs no better than random

16. Error analysis
    - is the systematic process of examining and understanding the errors made by a machine learning model to identify patterns, diagnose root causes, and develop a strategic plan for improvement. It shifts focus from aggregate performance metrics (like overall accuracy) to specific instances of failure to ensure robust and reliable model performance, especially in real-world production environments.
    - Beyond Aggregate Metrics: A single accuracy score (e.g, 90%) can be misleading as performance might not be uniform across different subgroups (cohorts) of data.
    - Systematic vs. Random Errors: The goal is to find systematic error patterns (e.g., a dog classifier consistently misclassifying white dogs as cats) rather than random, one-off mistakes.
    - Actionable Insights: The main purpose is to gain insights that suggest specific, high-impact improvements, such as gathering more data for underrepresented cases, feature engineering, or adjusting the model architecture.
    - The Error Analysis Process
      1. A typical error analysis follows an iterative process:
      2. Collect a Sample of Errors: Gather a representative set of data points from the development or test set where the model made incorrect predictions.
      3. Manually Examine and Categorize: Manually inspect the misclassified examples to identify common themes or patterns. For a cat/dog classifier, you might find errors related to: Blurry images, Specific breeds (e.g., dog breeds that look like cats), Incorrectly labeled data (label noise) in the original dataset
    - Quantify Error Types: Use a spreadsheet to count the frequency of each error category. This helps determine which issues, if addressed, would yield the largest performance gain.
    - Prioritize and Implement Improvements: Focus efforts on the error categories that have the highest impact or are most frequent. Potential fixes include:
      1. Data Enhancement: Collecting more data for underperforming cohorts or fixing mislabeled data.
      2. Feature Engineering: Creating new features tailored to the identified problem areas.
      3. Model Adjustment: Trying a different model architecture or adjusting hyperparameters.
    - Re-evaluate: Retrain the model with the changes and repeat the error analysis process to see the impact of your interventions and uncover new issues.
    - Tools and Techniques
      1. Confusion Matrix: A standard visualization for classification problems to understand the types of correct and incorrect predictions (e.g., false positives/negatives).
      2. Error Trees/Heatmaps: Visual tools (like those in Azure Machine Learning's Responsible AI dashboard) that automatically break down errors across different feature dimensions to highlight problematic data cohorts.
      3. Model Interpretability (LIME/SHAP): Techniques used to understand which features most influenced a specific prediction, helping to diagnose individual errors.
      4. Counterfactual Analysis: Generating synthetic adversarial examples to test the model's robustness and identify vulnerabilities.

#### Feature selection

Feature selection is a critical preprocessing step in machine learning that involves choosing a relevant subset of original features to build a model. Unlike feature extraction, which creates new variables through transformation, feature selection keeps a subset of the existing ones to improve accuracy, reduce training time, and enhance model interpretability.
Core Feature Selection Methods
Methods are generally categorized into three supervised groups and various unsupervised techniques:
Filter Methods: These evaluate features based on their intrinsic properties (like correlation or variance) independently of any machine learning algorithm.
Univariate Examples: Chi-Square test (categorical data), ANOVA (numerical input/categorical output), and Information Gain.
Multivariate Examples: Minimal Redundancy Maximal Relevance (mRMR) and Correlation-based Feature Selection (CFS).
Wrapper Methods: These use a specific model to evaluate subsets of features by training and testing iteratively.
Techniques: Forward Selection (adding features one-by-one), Backward Elimination (removing features), and Recursive Feature Elimination (RFE).
Embedded Methods: These integrate feature selection directly into the model training process.
Techniques: L1 Regularization (Lasso), which shrinks less important coefficients to zero, and Tree-based Importance (e.g., Random Forest or Gradient Boosting).
Unsupervised Methods: Used when labels are unavailable, focusing on data structure rather than target correlation.
Techniques: Principal Component Analysis (PCA), t-SNE, and Autoencoders.
