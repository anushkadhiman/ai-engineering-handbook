# Probabilty

Probability is a measure of the likelihood that an event will occur, represented as a number between 0 (impossible) and 1 (certain). It is calculated by dividing the number of favorable outcomes by the total number of possible outcomes. Probability is used to quantify uncertainty in various fields like risk management, finance, and weather forecasting.

**Key Concepts of Probability**

- Scale: Ranges from 0 (0%) to 1 (100%), often expressed as a fraction, decimal, or percentage.
- Formula: $P(\text{Event}) = \frac{\text{Number of favorable outcomes}}{\text{Total number of possible outcomes}}$.
- Sample Space: The set of all possible outcomes of a random experiment (e.g., $\{1,2,3,4,5,6\}$ for a six-sided die).
- Events: A specific outcome or subset of the sample space (e.g., rolling an even number: $\{2,4,6\}$).
- Independent Events: The outcome of one event does not affect the probability of another.

**Common Examples**

- Coin Toss: A fair coin has a 0.5 or 50% probability of landing on heads.
- Rolling a Die: The probability of rolling a specific number (e.g., a 4) is $\frac{1}{6}$.
- Marbles in a Bag: If a bag has 3 red and 2 yellow marbles, the probability of drawing a yellow marble is $\frac{2}{5}$ or 40%.

**Types of Probability**

- Theoretical Probability: Based on reasoning or calculation (e.g., 50/50 chance for a coin toss).
- Experimental Probability: Based on data collected from experiments or historical trends.
- Subjective Probability: Based on personal belief, experience, or judgment.

**Applications:**

Probability is used extensively in everyday life and professional fields, including weather forecasting, stock market analysis, and calculating insurance premiums.

---

# Statistics

Statistics is the science of collecting, organizing, analyzing, interpreting, and presenting data to uncover trends, make informed decisions, and reduce uncertainty. It utilizes mathematical techniques to turn raw data into insights, divided primarily into descriptive statistics (summarizing data) and inferential statistics (drawing conclusions about a population from a sample).

**Key Concepts and Types of Statistics**

- Descriptive Statistics: Summarizes data through measures of central tendency (mean, median, mode) and dispersion (variance, standard deviation).
- Inferential Statistics: Uses sample data to test hypotheses, make predictions, and draw conclusions about a larger population, such as through linear regression or ANOVA.
- Data Types:
  - Qualitative: Non-numerical, categorical data (e.g., color, brand).
  - Quantitative: Numerical data, including discrete (counted) and continuous (measured) values.

**Data Collection Methods**

- Surveys/Questionnaires: Gathering data directly from respondents (primary data).
- Experiments: Conducting controlled tests to observe the effects of changing variables.
- Observational Studies: Analyzing existing data, such as records or behaviors, without intervening.

**Common Applications**

- Business: Market research, trend forecasting, and quality control.
- Healthcare: Epidemiology, clinical trials, and medical research (often called biostatistics).
- Science/Engineering: Modeling complex systems, analyzing measurement errors, and testing scientific theories.
- Government: Analyzing population data, economic trends, and census statistics.

---

## Data

Data is raw, unorganized facts, figures, and symbols that are collected to be processed, analyzed, and used to make informed decisions. It serves as the basis for information in both human and computing contexts, ranging from text and numbers to audio, video, and images, and is commonly stored in databases.

- Definition: Data is information translated into a format that is efficient for movement and processing, often in binary form for computers.
- Types:
  - Quantitative: Measurable or countable numbers and statistics.
  - Qualitative: Descriptive information, such as labels or text, that cannot be easily measured.
  - Structured: Organized format, such as tables, rows, and columns.
  - Unstructured: Raw data without a predefined format, making up most data generated today.

- Applications: Data is used in data analytics to identify trends, in machine learning for modeling, and in business for daily decision-making.
- Life Cycle: It is collected from various sources, processed, and often transformed via data pipelines (e.g., ETL) for analysis

Data is crucial for developing, organizing, and improving systems and AI.

---

## Mean, median, and mode

Mean, median, and mode are measures of central tendency used to identify the "center" or typical value of a numerical data set.

- Mean: The average, found by summing all values and dividing by the total count.
- Median: The middle value when data is sorted in numerical order.
- Mode: The value that appears most frequently in the set.

**Key Details and Definitions**

- Mean (Average):
  - $\frac{\text{Sum of Data Points}}{\text{Total Number of Data Points}}$.
  - Highly sensitive to outliers.

- Median (Middle):
  Arranging data from smallest to largest and finding the middle value. If there is an even number of values, take the average of the two middle numbers. It is not sensitive to outliers.
- Mode (Most Common):
  The number that appears most often. A dataset can have one mode, no mode, or multiple modes.

**Example Dataset:** $\{1, 3, 3, 5, 8\}$

- Mean: $(1+3+3+5+8) \div 5 = 20 \div 5 = 4$
- Median: $3$ (The sorted middle number)
- Mode: $3$ (It appears twice)

**When to Use Which**

- Mean: Best for symmetric data without extreme outliers.
- Median: Best for skewed data or datasets with large outliers.
- Mode: Best for categorical data or finding the most common item.

---

## Variance and standard deviation

Variance and standard deviation measure how data spreads around the mean. Variance ($\sigma^2$) is the average of squared differences from the mean, providing a "squared" unit value. Standard deviation ($\sigma$) is the square root of variance, returning the measurement to the original data's units, making it more interpretable.

**Key Differences**

- Definition: Variance is the average of squared deviations, whereas standard deviation is the square root of that average.
- Units: Variance is in squared units (e.g., $m^2$), while standard deviation is in the same units as the data (e.g., $m$).
- Interpretation: Standard deviation is often preferred to understand the actual spread of data because it is in the same scale as the mean.

**Formulas**

- Population Variance (): $\sigma^2 = \frac{\sum (X_i - \mu)^2}{N}$
- Sample Variance (): $s^2 = \frac{\sum (x_i - \bar{x})^2}{n-1}$
- Standard Deviation ( or ): $\sqrt{\text{Variance}}$

**Key Details**

- Significance: A low standard deviation indicates data points are close to the mean, while a high standard deviation indicates a wide spread.
- Sample vs. Population: When calculating sample variance, dividing by $n-1$ (Bessel's correction) instead of $N$ provides an unbiased estimate of the population variance.
- Zero Variance: If all data points are the same, the variance and standard deviation are zero.

Example Calculation
For data set: {5, 5, 9, 9, 9, 10, 5, 10, 10}

1. Mean (): $\frac{5+5+9+9+9+10+5+10+10}{9} = 8$
2. Differences from mean: -3, -3, 1, 1, 1, 2, -3, 2, 2
3. Squared differences: 9, 9, 1, 1, 1, 4, 9, 4, 4
4. Sum of squared differences: 42
5. Sample Variance (): $\frac{42}{9-1} = \frac{42}{8} = 5.25$
6. Standard Deviation (): $\sqrt{5.25} \approx 2.29$

---

## Covariance and correlation

Covariance and correlation measure how variables move together, with covariance indicating the direction of the linear relationship (positive/negative) and correlation indicating both direction and strength (normalized between -1 and +1). Covariance is unit-dependent and affected by scale, while correlation is scale-invariant and standardized.

**Covariance**
Covariance measures the total variation of two random variables from their expected values.

- Significance: Tells us if variables increase or decrease together ($>0$) or move in opposite directions ($<0$).
- Units: The unit is the product of the units of the two variables.
- Range: $-\infty$ to $+\infty$.
- Formula: $\text{cov}(X, Y) = \frac{\sum (X_i - \bar{X})(Y_i - \bar{Y})}{n-1}$.

**Correlation**
Correlation is a standardized form of covariance, often known as the Pearson correlation coefficient, which quantifies the linear strength of the relationship.

- Significance: Measures the strength and direction. A value of +1 implies a perfect positive relationship, -1 a perfect negative relationship, and 0 no linear relationship.
- Units: Unitless (dimensionless).
- Range: -1 to +1.
- Formula: $\rho_{XY} = \frac{\text{cov}(X, Y)}{\sigma_X \sigma_Y}$ (Covariance divided by the product of standard deviations).

Correlation is superior for determining the strength of a relationship because it is standardized, whereas covariance is mainly used to understand the direction of movement, often in financial portfolio diversification.

---

## Marginal probability

Marginal probability is the unconditional likelihood of a single event occurring, independent of other variables. It represents the probability of a subset of variables, calculated by summing (for discrete variables) or integrating (for continuous) the joint probability distribution over all possible values of the irrelevant, ignored variables.

**Key Aspects of Marginal Probability**

- Unconditional: Unlike conditional probability, it does not depend on another event.
- Marginalization Process: To find the marginal probability of event $X$, you sum the joint probabilities $P(X, Y)$ across all possible values of $Y$.
  - Discrete Formula: $P(X=x) = \sum_{y} P(X=x, Y=y)$.
  - Continuous Formula: $f_X(x) = \int f_{X,Y}(x,y) dy$.

- "Marginal" Origin: The term comes from the practice of calculating these probabilities by summing joint probability tables along rows or down columns and placing the results in the table's margins.

**Example**: If you have a joint probability table of selling clothing, the marginal probability of selling shoes (regardless of whether it's in New York or California) is found by summing the joint probability of "shoes + New York" and "shoes + California".

- Marginal: $P(A)$ (e.g., probability of picking a red card).
- Joint: $P(A \text{ and } B)$ (e.g., probability of picking a red four).
- Conditional: $P(A|B)$ (e.g., probability of a card being red given it is a four).

---

## Joint probability

Joint probability is the statistical likelihood of two or more events occurring simultaneously, denoted as $P(A \text{ and } B)$ or $P(A, B)$. It measures the intersection of events. If events are independent, the joint probability is calculated by multiplying their individual probabilities: $P(A \cap B) = P(A) \times P(B)$.

**Key Aspects of Joint Probability:**

- Definition: The probability of both Event A and Event B occurring together.
- Formula (Independent Events): $P(A \text{ and } B) = P(A) \times P(B)$.
- Formula (Dependent Events): $P(A \text{ and } B) = P(A) \times P(B|A)$, where $P(B|A)$ is the conditional probability of $B$ given $A$.
- Range: The value lies between $0$ and $1$.
- Examples:
  - Independent: Flipping a coin twice and getting Heads both times: $P(H1) \times P(H2) = 0.5 \times 0.5 = 0.25$.
  - Dependent: Drawing two cards without replacement.

**Joint Probability Distributions:**
For random variables, a joint probability distribution (or density function for continuous variables) gives the probability that each variable falls within a certain range.

- Discrete: $\sum \sum P(X, Y) = 1$.
- Continuous: $\int \int f_{XY}(x, y) \,dx\,dy = 1$.

**Marginal vs. Joint Probability**

- Joint Probability is the intersection of two events (e.g., probability of being young AND having high income).
- Marginal Probability is the probability of a single event ignoring the other (e.g., probability of being young), Duke University.

---

## Conditional probability

Conditional probability is the likelihood of an event occurring, given that another related event has already taken place. It updates the probability of an event based on new information,
denoted as $P(A|B)$ ("probability of $A$ given $B$") and
calculated as $P(A|B) = \frac{P(A \cap B)}{P(B)}$, provided $P(B) > 0$.

**Key Concepts and Formula**

- Definition: It measures the probability of event $A$ occurring, knowing that event $B$ has already occurred.
- Formula: $P(A|B) = \frac{P(A \text{ and } B)}{P(B)}$.
- Components:
  - $P(A|B)$: Conditional probability of $A$ given $B$.
  - $P(A \cap B)$ or $P(A \text{ and } B)$: Joint probability of both events occurring.
  - $P(B)$: Marginal probability of event $B$ occurring.

- Independence: If $A$ and $B$ are independent, $P(A|B) = P(A)$.

**Examples**

- Cards: The probability of drawing a second heart from a deck, given that the first card drawn was a heart, is $\frac{12}{51}$.
- Weather/Traffic: The probability of a traffic accident ($A$) given that it is raining ($B$).
- Dice: If two dice are thrown and the sum is 7, the probability that a 3 appeared at least once.

**Visual Representation**
A Venn diagram illustrates this by restricting the focus from the entire sample space to only the area where event $B$ has occurred. Within this restricted space ($B$), the probability of $A$ is the intersection of $A$ and $B$ relative to $B$.

**Applications**
Conditional probability is widely used in:

- Insurance: Calculating risk based on specific conditions.
- Machine Learning/Data Science: Bayesian algorithms.
- Economics & Politics: Forecasting based on events.
- Medical Testing: Calculating the probability of having a disease given a positive test result.

---

## Bayes' Theorem

Bayes' Theorem is a mathematical formula used to calculate the probability of an event based on prior knowledge of conditions related to that event, updating initial beliefs (priors) with new evidence to find the posterior probability. It is essential for determining conditional probabilities, often expressed as

$P(A|B) = \frac{P(B|A) \times P(A)}{P(B)}$.

**Key Components**

- (Posterior Probability): The probability of hypothesis $A$ being true, given the evidence $B$.
- (Likelihood): The probability of the evidence $B$ given that hypothesis $A$ is true.
- (Prior Probability): The initial probability of hypothesis $A$ before seeing the evidence.
- (Marginal Likelihood): The total probability of the evidence.

**Key Applications**

- Medical Testing: Calculating the true likelihood of having a disease after a positive test result, considering false positives.
- Machine Learning: Used for predictive modeling and developing Bayesian techniques to estimate unknown parameters.
- Data Analysis: Updating models based on new data or information.

**Example:**
If the probability of rain is $15\%$ ($P(A)$) and it is cloudy in the morning $25\%$ of the time ($P(B)$), and it is cloudy in the morning given that it rains $80\%$ of the time ($P(B|A)$), Bayes' theorem can calculate the probability of rain given that it is cloudy ($P(A|B)$).

---
