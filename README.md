# Customer Happiness Index Analysis using Python

## Data Analysis and Manipulation Pipeline

This repository contains a Python script for data analysis and manipulation pipeline implemented using Pandas library. The script reads data from a text file, performs various data transformations, merges multiple DataFrames, and saves the final processed data to a new text file. Below is the breakdown of the functionality implemented in the script:

Functionality:

Data Loading: Reads data from a text file into a Pandas DataFrame. The file path, delimiter, encoding, and skiprows parameters can be customized as per the data source.

Data Preprocessing: Converts date-time columns to datetime format. Extracts month and year from the date-time column. Converts specific columns to appropriate data types (e.g., converting strings to integers).

Data Manipulation: Creates separate DataFrames for each month's data. Performs data aggregation and grouping to obtain unique values for specific columns. Merges multiple DataFrames based on a common column ('MDN').

Data Cleaning: Renames columns for clarity and consistency. Removes redundant or unnecessary columns.

Data Export: Saves the final processed data to a new text file. Provides options to customize the file path and delimiter for the output file.
