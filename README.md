# HPCC DataPatterns Library Extension
### Detection of Semantic Types in huge datasets and their validation.
Semantic type detection is critical for analyzing large textual datasets. NLP techniques like cosine similarity, range-based classification, and regex matching can help identify the type of information present in the text. This enables efficient categorization of the dataset, making it easier to extract insights and draw conclusions.
### Table of Contents
Installation</br>
Basic Methodology - Detailed Explanation of All Functions </br>
Examples</br>
Links for some datasets</br>

### Dependencies  
The code is written in Python 3 and requires the following libraries to be installed:</br>

* Python 3.x
* scikit-learn
* spaCy
* pandas
* numpy
* re

### Installation
Download the zip file for this Github Repository or clone it using </br>
`git clone https://github.com/akanksha0209/HPCC-DataPatterns-Library-Extension.git `</br>
After cloning it make sure all dependencies are installed.
Aliter the **detect_semantic_type_demo_file.ipynb** is a tutorial file that can be directly run on google colab. 🔗 https://colab.research.google.com/drive/1rCl-Kst9OBXDjLKvlVukGE0d71dAIm7e?usp=sharing </br>

### Basic Methodology - Detailed Explanation of All Functions
#### Overview of the different functions </br>

### Column Data Type Prediction using NLP </br>
This code contains a function classify_column_datatype(df) that predicts the data types of columns in a pandas DataFrame using natural language processing techniques. The function takes in a pandas DataFrame as input, and returns a dictionary of predicted data types for each column.

**Global Variables**</br>
The code includes the following global variables:

* **path** : the path to the input dataset.
* **predicted_data_types**: an empty dictionary that will store the predicted data types for each column.
* **type_map**: a dictionary that maps named entity types identified by the spaCy natural language processing library to data types.


#### classify_column_datatype:</br>
The **classify_column_datatype(df)** function takes in a pandas DataFrame as input, and returns a dictionary of predicted data types for each column. The function works by iterating through each column in the input DataFrame, and using regular expressions and named entity recognition to predict the data type of each column.

The function first checks the data type of the column using df[column].dtype. If the data type is object, it then checks the column contents using regular expressions to identify patterns such as integers, floats, and datetimes. If the column contents match a particular pattern, the function predicts the corresponding data type.

If the column contents do not match any of the regular expressions, the function uses the spaCy natural language processing library to identify named entities in the column contents. The function then maps the identified named entities to data types using the type_map global variable.

The function returns a dictionary predicted_data_types that maps each column name to its predicted data type.</br>

### NER Classification of CSV file</br>

This code applies Named Entity Recognition (NER) on every value in a column of a CSV file and returns the column with the NER values. The get_entities() function takes a string input and returns a list of entity labels using the en_core_web_sm model from the spaCy library.</br>

The **assign_column_ner_classification()** function assigns the NER values to a new copy of the input dataframe, and returns the new dataframe with the NER values. It samples num_samples number of rows from the input dataframe and converts each column into a string before applying the get_entities() function to each value in the column.</br>

The **major_col_pred_array()** function extracts the majority of each column from the new dataframe with NER values and stores it in an array. It calls the assign_column_ner_classification() function to create the new dataframe and then iterates over each column to count the occurrences of each unique value. It then selects the value with the highest count and stores it in the majority_arr array. The function returns the majority_arr array with the majority NER value for each column.</br>

To use this code, simply pass a dataframe with columns containing string values to the **assign_column_ner_classification()** function. It is also possible to adjust the num_samples parameter to sample a smaller or larger number of rows from the dataframe. 
</br>

#### Function 1: match_column_type</br>
The match_column_type function takes in a dataset and a column name as inputs and returns the semantic type of the column. It does this by computing the cosine similarity between the text in the column and a set of predefined values for each semantic type. The semantic type with the highest similarity score is returned. The function uses the TfidfVectorizer and cosine_similarity functions from the sklearn package to perform these calculations.</br>


#### Function 2: predict_matching_values: </br>
This function takes in four parameters: the column number, a key, a type map, and a list of column names. The purpose of the function is to predict matching values for a given key in a type map based on the similarity between the column name and the key.
First, the function retrieves the name of the column for the given column number and gets the embeddings for the column name and the key using spaCy's pre-trained language model. It then computes the cosine similarity between the two embeddings to determine their similarity.Next, it retrieves the values from the type map for the given key and finds the most similar value to the key based on cosine similarity. This most similar value is used as a reference point for determining which other values in the key's value list closely match the column name.Finally, the function creates a list of values that have a similarity score above the reference point's similarity score and returns this list as the predicted matching values.</br>

#### Function 3: detect1_semantic_type: </br>
This function detects the semantic type of a list of numeric values and performs a range based classification. 
The parameters chosen are latitude, longitude, temperature, humidity, measurement, and salary. The range as well as the differences in the consequent values is calculated.
- Latitude and longitude, all the values of the column are -90<=latitude<=90, and -180<=longitude<=180. 
- Temperature, all values are in the range (-10, 50), all absolute difference should be less than 10
- Humidity, all values are in the range(0, 100), 
- Altitude, all values are in the range(-413.6, 8848) 
- Numerical Indicators like Salary and cost, all values are greater than 0
Based on the ranges, the output is obtained. </br>

#### Function 4: classify_string_column_three: </br>
This function performs regex based classification. The regex patterns for different entities like email, phone number, pincode, and url is defined. 
- email_pattern = r'\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Z|a-z]{2,}\b'
- phone_pattern = r'\b\d{3}[-.]?\d{3}[-.]?\d{4}\b'
- pincode_pattern = r'\b\d{6}\b'
- url_pattern = r'http[s]?://(?:[a-zA-Z]|[0-9]|[$-_@.&+]|[!*\(\),]|(?:%[0-9a-fA-F][0-9a-fA-F]))+'

The pattern searching is performed and the semantic type is returned</br>

#### Function 5: get_entities: </br>
This function assigns named entity recognition value to an input </br>

#### Function 6: assign_column_ner_classification: </br>
The whole dataframe is broken into chunks of size 25. This function assigns named entity recognition value to new copy of dataframe and returns the new dataframe. It extracts majority of each column and stores it in an array </br>

#### Function 7: major_col_pred_array: </br>
The function 'major_col_pred_array' takes a dataframe as input and predicts the major column type using NER classification. It assigns a classification to a subset of the data (num_samples) using another function called 'assign_column_ner_classification'. It then calculates the most common classification for each column and stores it in an array called 'majority_arr'. Finally, it prints the most common classification for each column and returns the 'majority_arr'. This function can be useful for quickly identifying the dominant column types in a large dataset. </br>

#### Function 8: match_column_type: </br>
This function takes a dataset and a column name as input parameters and returns the best matching column type based on the similarity of the values in the column with predefined type maps. Here are the main steps of the function:
- It creates a TfidfVectorizer object to transform the text data into vectors and fit it on the column data.
- It iterates over the predefined type maps and transforms the values into vectors to compute the cosine similarity between the values vector and the text vectors of the column data.
- It computes the average similarity score for each type map and stores it in a dictionary.
- It returns the type map with the highest average similarity score as the best matching column type. </br>

#### Function 9: classify_columms: </br>
Classifies columns in a CSV dataset using NER and regex-based entity classification.
- Classify object type columns using NLP and regex
- If no named entity is found, regex is used to classify the column
- Classify numerical columns using range-based hierarchical classification
- If no semantic type is found, the column range is calculated and categorization is done as constant, binary, ordinal, interval, and ratio
A Pandas DataFrame with column names and their predicted entity types is returned. </br>
The classify_columns function takes two parameters:
* data: A Pandas DataFrame containing the CSV dataset.
* batch_size: The size of the batches to use for processing the dataset (default is 1000).
The output is a Pandas DataFrame with two columns:
* colname: The name of the column.
* prediction: The predicted entity type for the column.
</br>
### How it works
The classify_columns function first separates the columns into two categories: string columns and numeric columns.</br>

#### String columns
For string columns, the function uses spaCy's named entity recognition (NER) to identify named entities in the column. If a named entity is found, the function returns the entity type. If no named entity is found, the function uses regex patterns to classify the column as one of the following entity types:</br>

* Email
* Phone number
* Pincode
* URL
If the column still cannot be classified, the function uses additional regex patterns and heuristics to predict the entity type.</br>

#### Numeric columns
For numeric columns, the function uses a range-based hierarchical classification approach to predict the entity type. The function first calculates the range of values in the column (i.e., the difference between the maximum and minimum values). Depending on the range, the function predicts one of the following entity types:</br>

* Constant (range = 0)
* Binary (range = 1)
* Ordinal (range <= 10)
* Interval (range <= 100)
* Ratio (range > 100)

If the column still cannot be classified, the function uses additional regex patterns and heuristics to predict the entity type.
</br>


### Example 
The dataset used here is books.csv </br>
The dataset is loaded and once the datatypes are detected, we get the following as the ouput.
</br>
</br>
![image](https://user-images.githubusercontent.com/97330850/234066399-8242605a-25d2-4190-b32a-a6875a23a886.png)
</br>
</br>
The ner_classification function returns the dataset in the following manner. </br> 
</br>
![image](https://user-images.githubusercontent.com/97330850/234066796-f3dfe388-8379-437a-9f45-1d870e21e18b.png)
</br>
</br>
The final output after applying all the classification functions and regex is as follows: </br>
</br>
![image](https://user-images.githubusercontent.com/97330850/234067046-fc25c727-a48f-4822-9e3d-a8390861275f.png)
</br>
</br>


### Links for Some Datasets

1) [https://drive.google.com/file/d/1RHoS14zMEKozfDhV6Brtmhiec-qepSWK/view?usp=share_link](https://drive.google.com/file/d/1RHoS14zMEKozfDhV6Brtmhiec-qepSWK/view?usp=share_link) </br>

