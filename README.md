# 🦸‍♂️ SuperHero Data Cleaning Project

## 📘 Overview

This project explores and cleans a dataset containing information about superheroes from multiple universes (Marvel, DC, Dark Horse, and more).
The aim was to transform the raw catalogue into a **structured, analysis-ready dataset** by handling missing values, fixing inconsistent entries, and improving readability for future analysis or visualization.

The process was carried out in a **Jupyter Notebook** using **Python** and **Pandas**.

---

## 📂 Dataset Description

Two datasets were used in this project:

1. **`heroes_information.csv`** — Contains attributes such as name, gender, eye color, race, hair color, height, publisher, skin color, alignment, and weight.
2. **`super_hero_powers.csv`** — Contains binary (True/False) indicators for different powers that superheroes possess.

---

## ⚙️ Steps Performed

### 1. **Data Import**

* Imported `pandas` for data handling.
* Loaded the two datasets (`heroes_information.csv` and `super_hero_powers.csv`) using `pd.read_csv()`.

```python
import pandas as pd
heroes_df = pd.read_csv(r"C:\Users\DDR3\Desktop\super heroes dataset\heroes_information.csv")
powers_df = pd.read_csv(r"C:\Users\DDR3\Desktop\super heroes dataset\super_hero_powers.csv")
```

---

### 2. **Initial Exploration**

* Displayed the first and last few rows using `.head()` and `.tail()`.
* Checked the structure and data types using `.info()`.
* Inspected column names and null values using `.columns` and `.isnull().sum()`.

---

### 3. **Handling Missing Values**

* Identified and replaced missing (`NaN`) values with `"Unknown"` using:

  ```python
  heroes_df = heroes_df.fillna("Unknown")
  ```
* Verified that all missing values were successfully replaced.

---

### 4. **Cleaning Inconsistent Data**

* Replaced invalid symbols (`"-"`) in the **Skin color** column with `"No color"`.
* Standardized gender entries by replacing `"-"` with `"Unspecified"`.

  ```python
  heroes_df["Gender"] = heroes_df["Gender"].replace("-", "Unspecified")
  ```

---

### 5. **Removing Redundant Columns**

* Dropped the unnecessary **`Unnamed: 0`** column, which was an index artifact from CSV export:

  ```python
  heroes_df = heroes_df.drop("Unnamed: 0", axis=1)
  ```

---

### 6. **Data Type Correction**

* Converted `Height` and `Weight` columns to numeric formats (`int` and `float` where possible).
* Removed rows where `Weight` had the value `"Unknown"`.

  ```python
  condition = heroes_df["Weight"] == "Unknown"
  heroes_df = heroes_df.drop(heroes_df[condition].index)
  ```

---

### 7. **Fixing Negative and Invalid Values**

* Some numeric fields contained negative values. These were corrected using `.abs()`:

  ```python
  heroes_df["Weight"] = heroes_df["Weight"].abs()
  heroes_df["Height"] = heroes_df["Height"].abs()
  ```

---

### 8. **Renaming Columns**

* Renamed `Weight` and `Height` columns to make their units clear:

  ```python
  heroes_df = heroes_df.rename(columns={
      "Weight": "Weight (kg)",
      "Height": "Height (cm)"
  })
  ```

---

### 9. **Exploratory Insights**

* Identified unique gender categories with `.unique()`.
* Calculated the **average weight by gender** using:

  ```python
  heroes_df.groupby("Gender")["Weight (kg)"].mean()
  ```

---

## 🧹 Final Outcome

After cleaning, the dataset:

* Contains **no missing values or redundant columns**
* Has **standardized categorical entries**
* Uses **consistent numeric formats**
* Is **ready for visualization and statistical analysis**

---

## 🛠️ Tools Used

* **Python 3**
* **Pandas**
* **Jupyter Notebook**

---

## 📊 Future Work

* Merge `heroes_df` with `powers_df` for power-based analysis.
* Visualize data (e.g., height/weight distribution, gender representation).
* Perform clustering or classification to categorize heroes by abilities.

---

## 📁 File Structure

```
SuperHeroProject/
│
├── SuperHeroProject.ipynb        # Main notebook with data cleaning steps
├── heroes_information.csv        # Raw heroes dataset
├── super_hero_powers.csv         # Raw powers dataset
└── README.md                     # Project documentation (this file)
```

---

## ✨ Author

**Kenneth Chizaram Mbadugha**
Data Engineer

---

Would you like me to format this README with Markdown styling (headings, emojis, code blocks, and section links) ready for direct upload to GitHub?
