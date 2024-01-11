# FIFA_23-data-cleaning

## Introduction

This document provides a comprehensive summary of the data cleaning process for the FIFA23 dataset. The dataset, obtained from Kaggle, contains information about players in the FIFA23 video game, including attributes such as player name, age, nationality, club, overall rating, and more. The cleaning process aimed to address issues such as missing values and inconsistent formatting.

## Dataset Overview

- **Source:** Kaggle.
- **Size:** 18K+ records of player data.
- **Attributes:** Player name, age, nationality, club, overall rating, and more.

## Issues Found

1. **Missing Values:**
   - *Hits Column:* Represents the number of times a player has been searched; some players had never been searched, resulting in blank records.
   - *Loan Date End Column:* Represents the end date of contracts for players on loan; blank records for players with no contract.

2. **Inconsistent Formatting:**
   - *Heights and Weights Columns:* Values stored in different units; resolved using transformations, lambda functions, and normalization techniques.

## Tools Used

1. **Python:** For data cleaning tasks.
2. **Pandas:** Data manipulation, cleaning, and handling missing values.
3. **NumPy:** Mathematical operations and array handling.
4. **Jupyter Notebooks:** Interactive environment for code development, exploration, and documentation.

## Data Cleaning Process

1. **Data Understanding:**
   - Thorough examination of dataset structure and columns.
   - Creation of a data dictionary based on online sources.

2. **Data Exploration:**
   - Exploratory Data Analysis for insights, patterns, and anomalies.

3. **Handling Missing Values:**
   - Understanding the reasons for missing values in Hits and Loan Date End columns.
   - Filling missing values in Hits and Loan Date End based on data context.

4. **Standardizing Formatting:**
   - Resolving inconsistent formatting in Heights and Weights columns using transformations, lambda functions, and normalization.

5. **Validation and Quality Checks:**
   - Rigorous validation to ensure data quality, accuracy, and integrity.

## Code Snippets

```python
# Example code snippets from the cleaning process

# Filling missing values
df['Club'].fillna('Unknown', inplace=True)
df['body_type'].fillna('Unknown', inplace=True)
df['body_measurement'].fillna('Unknown', inplace=True)
df.drop('Body Type', axis=1, inplace=True)

# Standardizing formatting
df['Position'] = df['Position'].str.split('>').str[1]
df['Joined'] = original_column['Joined']
df['Joined(year)'] = df['Joined'].str.strip(',').str[-4:]
# More code snippets...

# Calculate 'Contract_length'
df['Contract_length'] = df['Contract Valid Until(year)'] - df['Joined(year)']

# Convert 'Release Clause' to million
df['Release Clause'] = df['Release Clause'].apply(convert_to_million)
df_sorted['Release Clause(in million)'] = df_sorted['Release Clause']
df_sorted.drop('Release Clause', axis=1, inplace=True)

# Convert 'Height' to integer
df_sorted['Height'].apply(convert_height)
