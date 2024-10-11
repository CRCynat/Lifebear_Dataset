# Data Cleaning

# Overview
This python script disects a dataset, removes duplicate rows, splits the dataset into manageable sizes for cleaning, validates the data, removes inconsistencies in the dataset and recontructs it as one file into a readable format.

# Requirements
* [Google Colab](https://colab.research.google.com/)
* Dataset
* Pandas
* Regular expression library
* os library

# Installation
Import the relevant modules and libraries
```python
import pandas as pd
import os
import re
```
* pandas: For data manipulation and analysis
* os: For manipulating paths
* re: Specifies a set of strings that matches it

# Functioning Process

# Read Dataset
```python
dataset = f'filepath'

lifebear = pd.read_csv(dataset, sep=';', low_memory=True)
lifebear.info()
```
* Read dataset to be manipulated and cleaned
* .info(): Prints a concise summary of a DataFrame

# Split Dataset Into Chunks
```python
def split_csv(input_file, output_dir, chunk_size_mb=100):
```
* Splits a CSV file into smaller chunks based on size
*  input_file: Path to the input CSV file
*  output_dir: Directory to save the output chunks
*  chunk_size_mb: Size of each chunk in MB

# Check For Valid Emails
```python
def validate_email(email):
  pattern = r'^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$'
  return bool(re.match(pattern, email))
```
* Validates an email address using a regular expression

# Clean and Garbage Extraction
```python
cleaned_dir = '/content/cleaned_chunks'
garbage_dir = '/content/garbage'

if not os.path.exists(cleaned_dir):
  os.makedirs(cleaned_dir)

if not os.path.exists(garbage_dir):
  os.makedirs(garbage_dir)
```
* Create directories for cleaned and invalid chunks

# Check Chunk Files 
```python
for filename in os.listdir(filepath):
  if filename.startswith(filename) and filename.endswith('.csv'):
    filepath = os.path.join(filepath, filename)
    df = pd.read_csv(filepath)

    print(f"\nProcessing chunk: {filename}")
    print("Info:")
    print(df.info())
```
* Use .info(), .head(), .tail() to confirm the datasets were split correctly

# Combine Chunks
```python
combined_df = pd.DataFrame()
for filename in os.listdir(filepath):
  if filename.startswith(filename) and filename.endswith('.csv'):
    filepath = os.path.join(filepath, filename)
    df = pd.read_csv(filepath)
    combined_df = pd.concat([combined_df, df], ignore_index=True)

os.makedirs(filepath, exist_ok=True)
combined_df.to_csv(filename, index=False)
```
* Combines chunks in the filepath to create one file

# Conclusion
These functions and processes extract, transform and store data into clean, readable datasets.
