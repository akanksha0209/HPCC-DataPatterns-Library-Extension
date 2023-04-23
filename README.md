# HPCC DataPatterns Library Extension
### Detection of Semantic Types in huge datasets and their validation.
Semantic type detection is critical for analyzing large textual datasets. NLP techniques like cosine similarity, range-based classification, and regex matching can help identify the type of information present in the text. This enables efficient categorization of the dataset, making it easier to extract insights and draw conclusions.
### Table of Contents
Installation</br>
Basic Methodology</br>
Examples</br>

### Installation
Download the zip file for this Github Repository or clone it using </br>
`git clone https://github.com/akanksha0209/HPCC-DataPatterns-Library-Extension.git `</br>
After cloning it make sure all dependencies are installed.

### Basic Methodology
##### Overview of the different functions </br>
classify_column_datatype:</br>
This is a function that takes a pandas dataframe as input and iterates through each column to predict its data type. It checks the data type of the column and then uses regular expressions and pandas datetime functions to predict whether the column is numerical, categorical, datetime, time, bool, or unknown. The predicted data types are returned as a dictionary. Finally, the function prints the predicted data types for each column.
