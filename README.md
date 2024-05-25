# Customer Happiness Index Analysis using Python

### 📊 Data Analysis and Manipulation Pipeline 🛠️

## Table of Contents

1. [About](#about)
2. [Purpose of Project](#purpose-of-project)
3. [About Data](#about-data)
4. [Functionality](#functionality)
5. [Python Code](#python-code)
6. [Conclusion](#conclusion)

## About
This repository contains a Python script for a data analysis and manipulation pipeline implemented using the Pandas library. 

## Purpose of Project
The script reads data from a text file, performs various data transformations, merges multiple DataFrames, and saves the final processed data to a new text file.

## About Data
The dataset used in this analysis is loaded from a text file. It includes various columns such as 'MDN', 'BILLING_ACCT_ID', 'ZONE_NAME', 'REGION', 'EXCHANGE', 'CRDDTM', and 'HAPPINESS_INDEX'.

## Functionality
### Data Loading
- Reads data from a text file into a Pandas DataFrame. 
- Allows customization of file path, delimiter, encoding, and skiprows parameters.

### Data Preprocessing
- Converts date-time columns to datetime format.
- Extracts month and year from the date-time column.
- Converts specific columns to appropriate data types.

### Data Manipulation
- Creates separate DataFrames for each month's data.
- Performs data aggregation and grouping.
- Merges multiple DataFrames based on a common column ('MDN').

### Data Cleaning
- Renames columns for clarity and consistency.
- Removes redundant or unnecessary columns.

### Data Export
- Saves the final processed data to a new text file.
- Provides options to customize the file path and delimiter for the output file.

## Python Code
```python
import pandas as pd
import warnings

warnings.filterwarnings('ignore')

# Step 1: Define the file path
file_path = r'path_to_your_file.txt'

# Step 2: Read the text file into a DataFrame
df = pd.read_csv(file_path, delimiter='\t', encoding='utf-16', skiprows=0)

# Step 3: Explore or manipulate the DataFrame
print(df.head())  # Display the first few rows of the DataFrame

# Convert 'CRDDTM' to datetime
df['CRDDTM'] = pd.to_datetime(df['CRDDTM'])

# Extract month and year from 'CRDDTM'
df['Month'] = df['CRDDTM'].dt.strftime('%b-%y')

# Convert necessary columns to appropriate types
df['MDN'] = df['MDN'].astype(str)
df['HAPPINESS_INDEX_STR'] = df['HAPPINESS_INDEX'].astype(str)

# Split 'HAPPINESS_INDEX_STR' to get integer part
df['HAPPINESS_INDEX_LEFT'] = df['HAPPINESS_INDEX_STR'].str.split('.').str[0]
df['HAPPINESS_INDEX_INT'] = df['HAPPINESS_INDEX_LEFT'].astype(int)

# Select relevant columns for summary data
summary_data1 = df[['MDN', 'BILLING_ACCT_ID', 'ZONE_NAME', 'REGION', 'EXCHANGE', 'Month', 'HAPPINESS_INDEX_INT']]
print(summary_data1)

# Create separate DataFrames for each month
# (Code for creating separate DataFrames is omitted for brevity)

# Group data by 'MDN' to get unique values for other columns
monthly_summary = df.groupby('MDN').agg({
    'BILLING_ACCT_ID': 'first',
    'ZONE_NAME': 'first',
    'REGION': 'first',
    'EXCHANGE': 'first',
})

# Reset index to make 'MDN' a column again
monthly_summary.reset_index(inplace=True)

# Print the new DataFrame
print(monthly_summary)

# Merge DataFrames based on the 'MDN' column
merged_df = pd.merge(merged_table, monthly_summary, on='MDN', how='left')

# Print the merged DataFrame
print(merged_df)

# Select relevant columns for final DataFrame
chi_data_df = merged_df[['MDN', 'HAPPINESS_INDEX_INT_Oct22', 'HAPPINESS_INDEX_INT_Nov22', 'HAPPINESS_INDEX_INT_Dec22', 
                         'HAPPINESS_INDEX_INT_Jan23', 'HAPPINESS_INDEX_INT_Feb23', 'HAPPINESS_INDEX_INT_Mar23', 
                         'HAPPINESS_INDEX_INT_Apr23', 'HAPPINESS_INDEX_INT_May23', 'HAPPINESS_INDEX_INT_Jun23', 
                         'HAPPINESS_INDEX_INT_Jul23', 'HAPPINESS_INDEX_INT_Aug23', 'HAPPINESS_INDEX_INT_Sep23', 
                         'HAPPINESS_INDEX_INT_Oct23', 'HAPPINESS_INDEX_INT_Nov23', 'HAPPINESS_INDEX_INT', 
                         'BILLING_ACCT_ID', 'ZONE_NAME', 'REGION', 'EXCHANGE']]

# Rename columns for clarity
new_column_names = {
    'HAPPINESS_INDEX_INT_Oct22': 'CHI_Oct22',
    'HAPPINESS_INDEX_INT_Nov22': 'CHI_Nov22',
    'HAPPINESS_INDEX_INT_Dec22': 'CHI_Dec22',
    'HAPPINESS_INDEX_INT_Jan23': 'CHI_Jan23',
    'HAPPINESS_INDEX_INT_Feb23': 'CHI_Feb23',
    'HAPPINESS_INDEX_INT_Mar23': 'CHI_Mar23',
    'HAPPINESS_INDEX_INT_Apr23': 'CHI_Apr23',
    'HAPPINESS_INDEX_INT_May23': 'CHI_May23',
    'HAPPINESS_INDEX_INT_Jun23': 'CHI_Jun23',
    'HAPPINESS_INDEX_INT_Jul23': 'CHI_Jul23',
    'HAPPINESS_INDEX_INT_Aug23': 'CHI_Aug23',
    'HAPPINESS_INDEX_INT_Sep23': 'CHI_Sep23',
    'HAPPINESS_INDEX_INT_Oct23': 'CHI_Oct23',
    'HAPPINESS_INDEX_INT_Nov23': 'CHI_Nov23',
    'HAPPINESS_INDEX_INT': 'CHI_Dec23',
}
chi_data_df = chi_data_df.rename(columns=new_column_names)

# Save DataFrame to a text file
chi_data_df.to_csv(r'path_to_save_file.txt', index=False, sep='\t')
```

## Conclusion
This Python script provides a robust data analysis and manipulation pipeline using the Pandas library. By following a structured approach, it enables users to efficiently process, clean, and analyze their data, leading to valuable insights and informed decision-making. With customizable functionalities for data loading, preprocessing, manipulation, cleaning, and export, the script offers flexibility and scalability for various data analysis tasks.
