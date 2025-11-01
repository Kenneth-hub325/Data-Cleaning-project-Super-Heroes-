
````markdown
# 🦸‍♂️ SuperHero Data Cleaning Project

## 📘 Overview
This project explores and cleans a dataset containing information about superheroes from multiple universes — including **Marvel**, **DC**, **Dark Horse**, and others.  

The aim was to transform the raw catalogue into a **structured, analysis-ready dataset** by handling missing values, fixing inconsistent entries, and improving readability for future analysis or visualization.  

The entire process was performed in a **Jupyter Notebook** using **Python** and **Pandas**.

---

## 📂 Dataset Description
Two datasets were used in this project:

1. **`heroes_information.csv`** — Contains details such as:
   - Name  
   - Gender  
   - Eye Color  
   - Race  
   - Hair Color  
   - Height  
   - Publisher  
   - Skin Color  
   - Alignment  
   - Weight  

2. **`super_hero_powers.csv`** — Contains binary indicators (`True`/`False`) for different powers that superheroes possess.

---

## ⚙️ Steps Performed

### 🧭 1. Data Import
- Imported **Pandas** for data manipulation.  
- Loaded the two datasets using `pd.read_csv()`.

```python
import pandas as pd
heroes_df = pd.read_csv(r"C:\Users\DDR3\Desktop\super heroes dataset\heroes_information.csv")
powers_df = pd.read_csv(r"C:\Users\DDR3\Desktop\super heroes dataset\super_hero_powers.csv")
````

---

### 🔍 2. Initial Exploration

* Displayed the first and last few rows using `.head()` and `.tail()`.
* Checked structure and data types with `.info()`.
* Inspected column names and missing values using `.columns` and `.isnull().sum()`.

---

### 🧹 3. Handling Missing Values

* Replaced missing (`NaN`) values with `"Unknown"`:

  ```python
  heroes_df = heroes_df.fillna("Unknown")
  ```
* Verified that no missing values remained with `.isnull().sum()`.

---

### 🧽 4. Cleaning Inconsistent Data

* Replaced `"-"` with `"No color"` in the **Skin color** column.
* Standardized gender by replacing `"-"` with `"Unspecified"`:

  ```python
  heroes_df["Gender"] = heroes_df["Gender"].replace("-", "Unspecified")
  ```

---

### 🗑️ 5. Removing Redundant Columns

* Dropped the unnecessary **`Unnamed: 0`** column (an index artifact):

  ```python
  heroes_df = heroes_df.drop("Unnamed: 0", axis=1)
  ```

---

### ⚖️ 6. Data Type Correction

* Converted **Height** and **Weight** columns to numeric types.
* Removed rows where `Weight` was `"Unknown"`:

  ```python
  condition = heroes_df["Weight"] == "Unknown"
  heroes_df = heroes_df.drop(heroes_df[condition].index)
  ```

---

### 🧮 7. Fixing Negative and Invalid Values

* Some height and weight values were negative; these were corrected using `.abs()`:

  ```python
  heroes_df["Weight"] = heroes_df["Weight"].abs()
  heroes_df["Height"] = heroes_df["Height"].abs()
  ```

---

### 🏷️ 8. Renaming Columns

* Renamed columns for clarity:

  ```python
  heroes_df = heroes_df.rename(columns={
      "Weight": "Weight (kg)",
      "Height": "Height (cm)"
  })
  ```

---

### 📊 9. Exploratory Insights

* Displayed unique gender categories with `.unique()`.
* Calculated average **weight by gender**:

  ```python
  heroes_df.groupby("Gender")["Weight (kg)"].mean()
  ```

---

## ✅ Final Outcome

After cleaning, the dataset:

* Contains **no missing values or redundant columns**
* Has **standardized categorical entries**
* Uses **consistent numeric formats**
* Is **ready for visualization and further analysis**

---

## 🛠️ Tools Used

* 🐍 **Python 3**
* 📘 **Pandas**
* 📓 **Jupyter Notebook**

---

## 🚀 Future Work

* Merge `heroes_df` with `powers_df` for hero-power analysis.
* Create visualizations (e.g., height/weight distributions, gender representation).
* Perform clustering or classification to group heroes by ability patterns.

---

## 📁 Project Structure

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

📧 Email: [mbadughakenneth2021@gmail.com](mailto:mbadughakenneth2021@gmail.com)
🌐 GitHub: [github.com/kennethmbadugha](https://github.com/kennethmbadugha)

---

```

---
