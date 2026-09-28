🧹 Amazon Data Cleaning Practice

A data-cleaning and preprocessing practice project using an Amazon product dataset. The project focuses on inspecting raw data, cleaning inconsistent values and data types, handling missing data, performing basic numerical analysis, and practicing **Pandas** and **NumPy** operations.

 📌 Project Overview

This project uses an Amazon product dataset containing **1,465 records and 16 columns**.

The accompanying Jupyter Notebook works through a series of practical data-cleaning and analysis exercises, including:

* Inspecting DataFrame columns and data types
* Removing unnecessary columns
* Cleaning currency and percentage values
* Converting columns to appropriate numeric data types
* Handling invalid rating values
* Detecting and handling missing values
* Performing basic statistical analysis
* Filtering and sorting products
* Grouping products by category
* Calculating discount amounts
* Practicing NumPy array operations
* Preparing cleaned numerical data for correlation analysis

> **Note:** The primary purpose of this project is data-cleaning practice rather than developing a complete business analytics solution.

---

## 🎯 Objectives

The main objectives of this project are to:

* Understand the structure of a real-world dataset
* Identify and remove unnecessary columns
* Clean numerical values stored as text
* Handle currency symbols, commas, and percentage signs
* Convert columns to suitable numeric data types
* Identify and handle missing values
* Perform exploratory analysis using Pandas
* Practice filtering, sorting, grouping, and aggregation
* Practice NumPy arrays, reshaping, and broadcasting
* Prepare cleaned data for further statistical analysis

---

## 📊 Dataset Description

The original CSV contains **1,465 rows and 16 columns**.

### Dataset Columns

| Column                | Description                  |
| --------------------- | ---------------------------- |
| `product_id`          | Product identifier           |
| `product_name`        | Product name                 |
| `category`            | Product category hierarchy   |
| `discounted_price`    | Product price after discount |
| `actual_price`        | Original product price       |
| `discount_percentage` | Discount percentage          |
| `rating`              | Product rating               |
| `rating_count`        | Number of ratings            |
| `about_product`       | Product description          |
| `user_id`             | User identifier information  |
| `user_name`           | User name information        |
| `review_id`           | Review identifier            |
| `review_title`        | Review title information     |
| `review_content`      | Review content               |
| `img_link`            | Product image link           |
| `product_link`        | Product page link            |

The original dataset contained **2 missing values in `rating_count`**.

---

## 🛠️ Tools & Technologies

* Python
* Jupyter Notebook
* Pandas
* NumPy

### Libraries

```python
import numpy as np
import pandas as pd
```

---

## 🧹 Data Cleaning & Preprocessing

### 1. Removing Unnecessary Columns

The following columns were removed from the working DataFrame:

```python
df.drop(
    columns=[
        "img_link",
        "product_link",
        "review_id",
        "user_name",
        "user_id",
        "about_product",
        "product_id"
    ],
    inplace=True
)
```

This reduced the working dataset from **16 columns to 9 columns**.

### 2. Cleaning Price Columns

Currency symbols and commas were removed before converting the price columns to floating-point values.

```python
df["discounted_price"] = (
    df["discounted_price"]
    .str.replace("₹", "")
    .str.replace(",", "")
    .astype(float)
)

df["actual_price"] = (
    df["actual_price"]
    .str.replace("₹", "")
    .str.replace(",", "")
    .astype(float)
)
```

### 3. Handling Invalid Ratings

Rows containing the invalid rating value `|` were removed:

```python
df = df[df["rating"] != "|"]
```

### 4. Cleaning Discount Percentage

The `%` symbol was removed and the column was converted to numeric values:

```python
df["discount_percentage"] = (
    df["discount_percentage"]
    .str.replace("%", "")
    .astype(float)
)
```

### 5. Converting Ratings

The `rating` column was converted to floating-point values:

```python
df["rating"] = df["rating"].astype(float)
```

### 6. Cleaning Rating Counts

Commas were removed from `rating_count` before converting the column to floating-point values:

```python
df["rating_count"] = df["rating_count"].str.replace(",", "")
df["rating_count"] = df["rating_count"].astype(float)
```

### 7. Handling Missing Values

Missing values were checked and rows containing missing values were removed:

```python
df = df.dropna()
```

After this step, the working DataFrame contained **1,462 rows**.

### 8. Creating a Discount Amount

A new column was created to calculate the difference between the original and discounted prices:

```python
df["discount_amt"] = (
    df["actual_price"] - df["discounted_price"]
)
```

---

## 📈 Analysis Performed

### Descriptive Statistics

| Metric              |      Mean |
| ------------------- | --------: |
| Discount Percentage |    47.67% |
| Rating              |      4.10 |
| Rating Count        | 18,307.38 |

### ⭐ Highest Product Ratings

The maximum rating observed in the cleaned dataset was **5.0**.

Three products were identified with this rating:

* Syncwire LTG to USB Cable for Fast Charging...
* REDTECH USB-C to Lightning Cable 3.3FT...
* Amazon Basics Wireless Mouse | 2.4 GHz Connect...

### 📂 Average Rating by Category

The notebook grouped products by category and calculated the average rating:

```python
high = df.groupby("category")["rating"].mean()
high.sort_values(ascending=False).head(1)
```

The highest average category rating returned by the notebook was:

```text
Computers&Accessories|Tablets — 4.6
```

### 🔎 Product Filtering

Products were filtered using rating and discount conditions:

```python
df[
    (df["rating"] > 4.5) &
    (df["discount_percentage"] > 50.0)
]
```

This returned **16 products** in the notebook output.

### 🔽 Product Sorting

Products were sorted by rating in descending order:

```python
df.sort_values("rating", ascending=False).head(10)
```

---

## 🔢 NumPy Analysis

NumPy was used to calculate statistics for `actual_price`:

```python
arr = df["actual_price"].to_numpy()

print("Min:", arr.min())
print("Max:", arr.max())
print("Mean:", arr.mean())
print("Std:", arr.std())
```

### Results

| Statistic          |       Value |
| ------------------ | ----------: |
| Minimum            |        39.0 |
| Maximum            |   139,900.0 |
| Mean               |  5,447.0029 |
| Standard Deviation | 10,874.5541 |

The notebook also practiced:

* Converting a Pandas column into a NumPy array
* Reshaping arrays
* Broadcasting operations

Example:

```python
arr_2d = arr.reshape(61, 24)
new_price = arr * 2
```

---

## 📊 Correlation Preparation

The cleaned numerical columns were selected for further correlation analysis:

```python
df[
    [
        "discounted_price",
        "actual_price",
        "discount_percentage",
        "rating",
        "rating_count"
    ]
]
```

The exercise asks for the correlation between `rating` and `rating_count`, but the notebook does not contain a completed correlation calculation or reported correlation value.

---

## 🔍 Key Findings

Based strictly on the completed notebook outputs:

* Original dataset: **1,465 rows × 16 columns**
* Working dataset after column removal: **9 columns**
* Invalid rating values were removed during the cleaning process
* `rating_count` contained **2 missing values**
* Final cleaned dataset: **1,462 rows**
* Average discount percentage: **47.67%**
* Average product rating: **4.10**
* Average rating count: **18,307.38**
* Highest product rating: **5.0**
* Highest reported category average rating: **4.6**
* Highest-rated category: **Computers&Accessories|Tablets**
* `actual_price` range: **₹39.00 – ₹139,900.00**

> These findings represent the outputs explicitly produced by the notebook and do not extend beyond the completed analysis.

---

## 📁 Project Structure

```text
Amazon-Data-Cleaning/
│
├── amazon 1.csv
├── Amazon 1.ipynb
└── README.md
```

---

## 💡 Skills Demonstrated

### Python & Pandas

* DataFrame inspection
* Column selection
* Column removal
* Data type conversion
* String manipulation
* Missing-value handling
* Filtering
* Sorting
* Grouping
* Aggregation
* Element-wise calculations

### NumPy

* NumPy array conversion
* Array statistics
* Array reshaping
* Broadcasting

### Data Cleaning

* Removing irrelevant columns
* Cleaning currency-formatted values
* Cleaning percentage-formatted values
* Converting text-based numerical columns
* Handling invalid values
* Handling missing values
* Creating derived columns

### Basic Data Analysis

* Mean calculations
* Minimum and maximum values
* Standard deviation
* Category-level aggregation
* Product filtering
* Product ranking

---

## 🚀 How to Run

### 1. Clone the Repository

```bash
git clone <repository-url>
cd Amazon-Data-Cleaning
```

### 2. Install Required Libraries

```bash
pip install pandas numpy jupyter
```

### 3. Start Jupyter Notebook

```bash
jupyter notebook
```

### 4. Open the Notebook

Open:

```text
Amazon 1.ipynb
```

Make sure the dataset:

```text
amazon 1.csv
```

is located in the same directory as the notebook.

---

## 🎓 Learning Outcomes

This project provided practical experience working with a real-world CSV dataset and strengthened my understanding of the initial stages of a data analytics workflow.

Key learning outcomes include:

* Understanding raw dataset structure
* Identifying data-quality issues
* Cleaning text-based numerical data
* Working with missing values
* Converting columns into appropriate data types
* Using Pandas for data manipulation
* Using NumPy for numerical operations
* Performing basic descriptive analysis
* Creating derived analytical columns
* Preparing cleaned data for further analysis

This project serves as a **data-cleaning practice project** and demonstrates foundational skills required before moving into more advanced exploratory analysis and data visualization.

---

## 👤 Author

**Rohit Chatterjee**

Data Analytics Portfolio Project
