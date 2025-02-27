# Pandas

# **1. Introduction to Pandas**

Pandas is a Python library used for **data manipulation, analysis, and cleaning**. It provides two primary data structures:

1. **Series** – A one-dimensional labeled array.
2. **DataFrame** – A two-dimensional labeled table.

### **1.1 Installing and Importing Pandas**

To install pandas:

```bash
pip install pandas
```

To import:

```python
import pandas as pd
import numpy as np  # For numerical operations
```

---

# **2. Pandas Data Structures**

## **2.1 Series (One-Dimensional Data Structure)**

A **Series** is similar to a list or a dictionary, where each value has an index.

### **Creating a Series**

```python
data = [10, 20, 30, 40]
series = pd.Series(data)
print(series)
```

#### **Output:**

```
0    10
1    20
2    30
3    40
dtype: int64
```

Each value is assigned an **index** (0, 1, 2, ...).

### **Custom Indexing in Series**

```python
series = pd.Series(data, index=['A', 'B', 'C', 'D'])
print(series)
```

#### **Output:**

```
A    10
B    20
C    30
D    40
dtype: int64
```

Here, we use **custom labels** instead of default integer indices.

### **Accessing Elements in Series**

```python
print(series['A'])  # Output: 10
print(series[0])    # Output: 10
```

### **Mathematical Operations on Series**

```python
print(series * 2)  # Multiplying all elements by 2
```

#### **Output:**

```
A    20
B    40
C    60
D    80
dtype: int64
```

---

## **2.2 DataFrame (Two-Dimensional Data Structure)**

A **DataFrame** is like an Excel spreadsheet or a SQL table.

### **Creating a DataFrame**

```python
data = {
    'Name': ['Alice', 'Bob', 'Charlie'],
    'Age': [25, 30, 35],
    'City': ['New York', 'Los Angeles', 'Chicago']
}

df = pd.DataFrame(data)
print(df)
```

#### **Output:**

```
     Name  Age         City
0   Alice   25    New York
1     Bob   30  Los Angeles
2  Charlie   35     Chicago
```

### **Accessing Data in DataFrame**

```python
print(df['Name'])  # Select single column
print(df[['Name', 'Age']])  # Select multiple columns
print(df.loc[0])  # Select row by index
print(df.iloc[1])  # Select row by position
```

### **Adding a New Column**

```python
df['Salary'] = [50000, 60000, 70000]
print(df)
```

#### **Output:**

```
     Name  Age         City  Salary
0   Alice   25    New York  50000
1     Bob   30  Los Angeles  60000
2  Charlie   35     Chicago  70000
```

### **Removing a Column**

```python
df.drop(columns=['Salary'], inplace=True)
print(df)
```

---

# **3. Data Inspection & Operations**

## **3.1 Viewing Data**

```python
print(df.head())  # First 5 rows
print(df.tail())  # Last 5 rows
print(df.info())  # Column data types
print(df.describe())  # Summary statistics
```

## **3.2 Sorting Data**

```python
df_sorted = df.sort_values(by='Age', ascending=False)
print(df_sorted)
```

## **3.3 Filtering Data**

```python
df_filtered = df[df['Age'] > 25]  # Select rows where Age > 25
print(df_filtered)
```

---

# **4. Handling Missing Data**

## **4.1 Checking for Missing Data**

```python
print(df.isnull().sum())  # Count missing values in each column
```

## **4.2 Filling Missing Data**

```python
df.fillna(0, inplace=True)  # Replace NaN with 0
df.fillna(df.mean(), inplace=True)  # Replace NaN with column mean
```

## **4.3 Dropping Missing Data**

```python
df.dropna(inplace=True)  # Remove rows with NaN values
```

---

# **5. Data Merging and Concatenation**

## **5.1 Concatenation (Stacking DataFrames)**

```python
df1 = pd.DataFrame({'A': ['A0', 'A1'], 'B': ['B0', 'B1']})
df2 = pd.DataFrame({'A': ['A2', 'A3'], 'B': ['B2', 'B3']})

result = pd.concat([df1, df2])
print(result)
```

## **5.2 Merging DataFrames (Like SQL JOIN)**

```python
df1 = pd.DataFrame({'ID': [1, 2], 'Name': ['Alice', 'Bob']})
df2 = pd.DataFrame({'ID': [1, 2], 'Age': [25, 30]})

merged_df = pd.merge(df1, df2, on='ID')
print(merged_df)
```

---

# **6. Grouping and Aggregation**

## **6.1 Grouping Data**

```python
grouped = df.groupby('City').mean()
print(grouped)
```

## **6.2 Aggregation Functions**

```python
print(df['Age'].sum())   # Sum of all ages
print(df['Age'].mean())  # Average age
print(df['Age'].min())   # Minimum age
print(df['Age'].max())   # Maximum age
```

---

# **7. Working with Files**

## **7.1 Reading CSV Files**

```python
df = pd.read_csv('data.csv')
print(df.head())
```

## **7.2 Writing to CSV**

```python
df.to_csv('output.csv', index=False)
```

## **7.3 Reading/Writing Excel Files**

```python
df = pd.read_excel('data.xlsx')
df.to_excel('output.xlsx', index=False)
```

---

# **8. Advanced Pandas Operations**

## **8.1 Applying Functions**

```python
df['Age'] = df['Age'].apply(lambda x: x + 1)  # Increment age by 1
print(df)
```

## **8.2 Pivot Tables**

```python
pivot = df.pivot_table(index='City', values='Age', aggfunc=np.mean)
print(pivot)
```

## **8.3 Time-Series Handling**

```python
df['Date'] = pd.to_datetime(df['Date'])
df.set_index('Date', inplace=True)
df_resampled = df.resample('M').mean()  # Resample data by month
print(df_resampled)
```

---

# **9. Visualization with Pandas**

## **9.1 Plotting**

```python
import matplotlib.pyplot as plt

df['Age'].plot(kind='bar')
plt.title("Age Distribution")
plt.show()
```

---

