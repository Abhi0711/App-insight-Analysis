# App Insights Unlocked --- Google Play Store EDA
## 1. Project Overview
**App Insights Unlocked** is an Exploratory Data Analysis (EDA) project
based on Google Play Store app data.

The objective of the project is to understand the factors associated
with app success, user satisfaction, popularity, and engagement. The
analysis explores app ratings, reviews, installs, size, price,
categories, genres, content ratings, and update patterns.

The project was designed from a business/data-analytics perspective to
answer questions such as:

-   What factors are associated with successful apps?
-   Which app categories have the highest user demand?
-   How do app size and price relate to ratings and installs?
-   How do free and paid apps differ?
-   What patterns can be observed in app updates?
-   Which genres and categories appear to perform strongly?

The original case study identifies **App Developers, Product Managers,
Marketing Teams, Senior Management, App Users, Advertisers, and
Technology Partners** as relevant stakeholders.

------------------------------------------------------------------------

## 2. Business Problem

A mobile-app company wants to use Google Play Store data to make better
product and marketing decisions.

The analysis focuses on:

1.  Identifying factors associated with high app ratings.
2.  Understanding popular categories and genres.
3.  Studying the relationship between installs, ratings, reviews, size,
    and price.
4.  Understanding differences between free and paid applications.
5.  Examining app-update behavior.
6.  Generating data-driven recommendations for future app development
    and optimization.

The case study specifically asks the analyst to develop success metrics
such as:

-   Average rating
-   Total installs
-   Number of reviews

and analyze these metrics against other variables.

------------------------------------------------------------------------

## 3. Dataset

The project uses the **Google Play Store Apps** dataset.

**Source:** Kaggle --- Google Play Store Apps dataset

The dataset contains information about applications available on the
Google Play Store.

### Main Columns

  Column             Description
  ------------------ ----------------------------------
  `App`              Name of the application
  `Category`         Application category
  `Rating`           Average user rating
  `Reviews`          Number of user reviews
  `Size`             Application size
  `Installs`         Number of installs
  `Type`             Free or Paid
  `Price`            Application price
  `Content Rating`   Intended age/content audience
  `Genres`           Application genre
  `Last Updated`     Date of the latest update
  `Current Ver`      Current application version
  `Android Ver`      Minimum Android version required

The case study also recommends converting fields such as `Installs` and
`Price` into appropriate numerical formats, removing duplicates,
standardizing text, and converting `Last Updated` into a datetime field.

------------------------------------------------------------------------

# 4. Tools & Technologies

## Programming Language

-   **Python**

## Libraries

### Pandas

Used for:

-   Loading the dataset
-   Data inspection
-   Missing-value handling
-   Duplicate detection/removal
-   Data transformation
-   Grouping and aggregation
-   Filtering
-   Correlation analysis
-   Creating derived columns

### NumPy

Used for:

-   Numerical operations
-   Handling missing values during preprocessing

### Matplotlib

Used for:

-   Histograms
-   Bar charts
-   Line charts
-   General data visualization

### Seaborn

Used for:

-   Box plots
-   Scatter plots
-   Line plots
-   Statistical visualization

## Development Environment

The notebook is implemented as a **Jupyter/Google Colab-style
notebook**, as indicated by the dataset path used in the notebook:

``` text
/content/googleplaystore.csv
```

------------------------------------------------------------------------

# 5. Project Workflow

The project follows an EDA workflow:

``` text
Raw Dataset
     ↓
Data Inspection
     ↓
Missing-Value Analysis
     ↓
Data Cleaning
     ↓
Duplicate Removal
     ↓
Data-Type Conversion
     ↓
Feature Transformation
     ↓
Exploratory Analysis
     ↓
Visualization
     ↓
Business Insights
     ↓
Recommendations
```

------------------------------------------------------------------------

# 6. Data Cleaning & Preprocessing

The notebook performs several preprocessing operations before analysis.

## 6.1 Missing Values

### Rating
### Current Version & Android Version
### Type
### Size

## 6.2 Duplicate Removal

## 6.3 Data-Type Conversion

## 6.4 Text Cleaning

## 6.5 Dataset Size After Cleaning

# 7. Exploratory Data Analysis

The analysis was divided into three levels:

-   Basic-level analysis
-   Medium-level analysis
-   Advanced-level analysis

------------------------------------------------------------------------

# 8. Key Insights

Based on the actual analysis performed in the notebook, the major
insights are:

### 1. Free apps dominate the dataset

There are 9,585 free apps compared with 762 paid apps.

This indicates that free distribution is the dominant model in this
dataset.

### 2. Overall user satisfaction is relatively high

The average rating is approximately **3.806/5**.

### 3. Popularity is not strongly related to rating

The correlation between installs and rating is only about **0.046**.

Therefore, a highly downloaded app is not automatically a highly rated
app.

### 4. Games have the highest total install volume

The Game category has more than **31.5 billion total installs** in the
cleaned dataset.

### 5. Communication is another major install category

Communication applications account for more than **24.1 billion total
installs**.

### 6. Highly rated does not necessarily mean highly successful

Several apps with 5.0 ratings have very small review and install counts.

This highlights the importance of considering:

-   Rating
-   Number of reviews
-   Installs
-   Engagement

together.

### 7. Everyone is the dominant content-rating segment

The largest content-rating group is `Everyone`, for both free and paid
applications.

### 8. App size varies considerably across categories

Games and several entertainment-oriented categories tend to have larger
average application sizes.

### 9. Facebook demonstrates the scale of review engagement

Facebook has approximately **78 million reviews** in the analyzed
dataset.

### 10. Install volume is concentrated in a relatively small set of categories

Game, Communication, Social, Productivity, and Tools are the five
categories with the highest aggregate installs.

------------------------------------------------------------------------

# 9. Challenges Faced

## Challenge 1 --- Handling Missing Values

The dataset contains missing values in important columns such as rating,
type, current version, Android version, and size.

Different columns require different treatment rather than simply
deleting every incomplete row.

**Approach used:**

-   Category-level median for missing ratings
-   Mode for missing app type
-   Row removal for missing version fields
-   Median for missing size values

------------------------------------------------------------------------

## Challenge 2 --- Converting Semi-Structured Numerical Data

Columns such as `Installs` and `Price` contain formatting characters
such as:

``` text
+
,
$
```

These characters prevent direct numerical analysis.

The project therefore required string cleaning before numerical
processing.

------------------------------------------------------------------------

## Challenge 3 --- App Size Formatting

The `Size` column contains values expressed using units such as MB and
KB as well as:

``` text
Varies with device
```

This makes standard numerical analysis difficult and requires careful
unit normalization.

------------------------------------------------------------------------

## Challenge 4 --- Rating Interpretation

Ratings are averages and do not contain information about how many users
contributed to the rating.

A 5.0 rating from a handful of users can look better than a 4.5 rating
from millions of users even though the second figure may provide much
stronger evidence of broad user satisfaction.

------------------------------------------------------------------------

## Challenge 5 --- Large Variation in Install Counts

Install values range across several orders of magnitude.

A normal linear-scale scatter plot can hide meaningful patterns.

The project therefore uses a logarithmic scale for the install axis in
the size-vs-installs analysis.

------------------------------------------------------------------------

## Challenge 6 --- Update-Frequency Analysis

The dataset is not a complete historical update log for every
application.

Therefore, calculating the time between updates is limited because many
apps do not have multiple historical update observations.

------------------------------------------------------------------------

# 10. Technical Limitations & Areas for Improvement

There are several areas where the current notebook could be improved.

## 10.1 Keep Rating as a Float

The notebook converts:

``` python
df['Rating'] = df['Rating'].astype(int)
```

This removes decimal information.

For example:

``` text
4.7 → 4
4.3 → 4
3.9 → 3
```

This can reduce analytical accuracy.

### Recommended improvement

Keep rating as a float:

``` python
df['Rating'] = df['Rating'].astype(float)
```

------------------------------------------------------------------------

## 10.2 Convert Price to Numeric

The notebook removes `$`, but the resulting `Price` column is not
converted into a numerical data type.

### Recommended improvement

``` python
df['Price'] = (
    df['Price']
    .replace('[\$,]', '', regex=True)
    .astype(float)
)
```

This would make price correlation, regression, price-range analysis, and
visualization easier.

------------------------------------------------------------------------

## 10.3 Normalize App Size Correctly

The current notebook transforms `M` and `k` using string replacement.

A better approach would explicitly convert:

-   MB → MB
-   KB → MB

using a consistent unit.

This avoids mixing values with different units.

------------------------------------------------------------------------

## 10.4 Improve Duplicate Handling

The project removes exact duplicate rows.

A stronger approach could also investigate duplicate app names and
determine whether they represent:

-   Multiple versions
-   Multiple categories
-   Duplicate records
-   Different snapshots

This is particularly important because app names can appear multiple
times.

------------------------------------------------------------------------

## 10.5 Improve Top-Rated App Analysis

Instead of simply selecting:

``` python
df.sort_values(by='Rating', ascending=False).head(10)
```

use a minimum-review threshold.

For example:

``` text
Rating >= 4.5
AND Reviews >= 1,000
```

This would produce a more meaningful high-quality-app benchmark.

------------------------------------------------------------------------

## 10.6 Improve Update-Frequency Analysis

A complete app-history dataset would be preferable for calculating:

-   Average days between updates
-   Median days between updates
-   Update frequency by category
-   Update frequency vs rating
-   Update frequency vs installs

------------------------------------------------------------------------

## 10.7 Add Review Sentiment Analysis

The original case study proposes sentiment analysis if review text is
available.

The current notebook does not perform this because the analyzed dataset
does not include the review-text information required for that analysis.

A separate Google Play Store review dataset could be integrated for:

-   Positive/negative sentiment
-   Common complaints
-   Feature requests
-   Frequent praise
-   Sentiment vs rating

------------------------------------------------------------------------

# 11. Business Recommendations

## Recommendation 1 --- Do Not Optimize Only for Downloads

The weak installs-rating correlation suggests that acquiring more users
does not automatically result in higher ratings.

Product teams should track both:

-   Acquisition metrics
-   Satisfaction metrics

------------------------------------------------------------------------

## Recommendation 2 --- Monitor Reviews Along With Ratings

Ratings should be evaluated together with review volume.

A more reliable success framework could include:

``` text
App Success Score =
Rating + Review Volume + Install Volume + Retention/Engagement
```

The exact weighting should be determined using business objectives and
additional data.

------------------------------------------------------------------------

## Recommendation 3 --- Optimize App Size

App size should be monitored because large applications can create
storage and download barriers.

Teams should investigate whether unnecessary assets, large media files,
or inefficient packaging can be reduced.

------------------------------------------------------------------------

## Recommendation 4 --- Study High-Install Categories

Game, Communication, Social, Productivity, and Tools show the highest
total install volumes in this dataset.

These categories can be studied for:

-   Feature patterns
-   Monetization models
-   User engagement
-   Update behavior
-   Common user expectations

This should be treated as market evidence rather than proof that a new
application should automatically enter one of these categories.

------------------------------------------------------------------------

## Recommendation 5 --- Use Review Text for Product Improvement

When review text is available, sentiment and topic analysis can
identify:

-   Common complaints
-   Bugs
-   Feature requests
-   Positive experiences
-   Usability issues

This would provide much deeper product insight than star ratings alone.

------------------------------------------------------------------------

## Recommendation 6 --- Use More Robust Success Metrics

Future analysis should combine:

-   Rating
-   Number of reviews
-   Installs
-   Install growth
-   Update frequency
-   App size
-   Price
-   User sentiment

rather than treating one metric as the definition of success.

------------------------------------------------------------------------

# 12. Suggested Future Analysis

The project can be extended into a stronger portfolio-level analytics
project by adding:

### Product Analytics

-   Rating vs review volume
-   Installs vs review volume
-   App size vs retention, if retention data becomes available
-   Update frequency vs ratings
-   Update frequency vs installs

### Pricing Analytics

-   Free vs paid performance
-   Price bands
-   Price vs reviews
-   Price vs installs
-   Price vs rating

### NLP

If review text is added:

-   Sentiment analysis
-   Word frequency
-   Topic modeling
-   Complaint classification
-   Positive-feature extraction

### Statistical Analysis

-   Confidence intervals
-   Hypothesis testing
-   Statistical significance of category differences
-   Non-parametric tests where appropriate

### Predictive Analytics

A future model could attempt to predict:

-   Expected rating
-   High-install probability
-   Review volume

However, the target variable and modeling strategy should be defined
carefully to avoid data leakage.

------------------------------------------------------------------------

# 13. Portfolio Value

This project demonstrates practical experience with:

-   Python
-   Pandas
-   NumPy
-   Data cleaning
-   Missing-value treatment
-   Duplicate handling
-   Data-type conversion
-   Feature transformation
-   Exploratory Data Analysis
-   GroupBy operations
-   Correlation analysis
-   Data visualization
-   Business-question-driven analysis
-   Translating analytical findings into recommendations

It is particularly useful as a **Data Analyst portfolio project**
because it connects technical analysis with business questions rather
than focusing only on coding.

------------------------------------------------------------------------

# 14. Project Structure

A recommended GitHub structure is:

``` text
App-Insights-Analysis/
│
├── README.md
├── EDA1.ipynb
├── googleplaystore.csv

------------------------------------------------------------------------

# 15. Conclusion

The **App Insights Unlocked** project demonstrates how exploratory data
analysis can be used to understand mobile-app performance and user
behavior.

The analysis shows that app success cannot be explained by a single
variable. High install volume, high ratings, review engagement,
category, app size, pricing, content rating, and update activity all
provide different pieces of information.

One of the strongest observations from the analysis is the weak linear
correlation between installs and ratings. This indicates that
**popularity and user satisfaction should be treated as separate
dimensions of app performance**.

The project can be significantly strengthened by retaining decimal
ratings, properly converting price and size into consistent numerical
formats, applying minimum-review thresholds for rating comparisons, and
adding review-text sentiment analysis.

------------------------------------------------------------------------

## 16. Data Source

Google Play Store Apps dataset:

**Kaggle:**
`https://www.kaggle.com/datasets/lava18/google-play-store-apps`

------------------------------------------------------------------------

## 17. Author

**Abhinav**

Data Analytics / Data Science Portfolio Project
