# HPCC DataPatterns Library Extension
### Detection of Semantic Types in huge datasets and their validation.
Semantic type detection is critical for analyzing large textual datasets. NLP techniques like cosine similarity, range-based classification, and regex matching can help identify the type of information present in the text. This enables efficient categorization of the dataset, making it easier to extract insights and draw conclusions.
### Table of Contents
Installation</br>
Basic Methodology - Detailed Explanation of All Functions </br>
Examples</br>
Links for some datasets</br>

### Installation
Download the zip file for this Github Repository or clone it using </br>
`git clone https://github.com/akanksha0209/HPCC-DataPatterns-Library-Extension.git `</br>
After cloning it make sure all dependencies are installed.

### Basic Methodology - Detailed Explanation of All Functions
#### Overview of the different functions </br>
#### classify_column_datatype:</br>
This is a function that takes a pandas dataframe as input and iterates through each column to predict its data type. It checks the data type of the column and then uses regular expressions and pandas datetime functions to predict whether the column is numerical, categorical, datetime, time, bool, or unknown. The predicted data types are returned as a dictionary. Finally, the function prints the predicted data types for each column.</br>
#### predict_matching_values: </br>
This function takes in four parameters: the column number, a key, a type map, and a list of column names. The purpose of the function is to predict matching values for a given key in a type map based on the similarity between the column name and the key.
First, the function retrieves the name of the column for the given column number and gets the embeddings for the column name and the key using spaCy's pre-trained language model. It then computes the cosine similarity between the two embeddings to determine their similarity.Next, it retrieves the values from the type map for the given key and finds the most similar value to the key based on cosine similarity. This most similar value is used as a reference point for determining which other values in the key's value list closely match the column name.Finally, the function creates a list of values that have a similarity score above the reference point's similarity score and returns this list as the predicted matching values.</br>

#### detect1_semantic_type: </br>
This function detects the semantic type of a list of numeric values and performs a range based classification. 
The parameters chosen are latitude, longitude, temperature, humidity, measurement, and salary. The range as well as the differences in the consequent values is calculated.
- Latitude and longitude, all the values of the column are -90<=latitude<=90, and -180<=longitude<=180. 
- Temperature, all values are in the range (-10, 50), all absolute difference should be less than 10
- Humidity, all values are in the range(0, 100), 
- Altitude, all values are in the range(-413.6, 8848) 
- Salary and cost, all values are greater than 0
Based on the ranges, the output is obtained. </br>

#### classify_string_column_three: </br>
This function performs regex based classification. The regex patterns for different entities like email, phone number, pincode, and url is defined. 
- email_pattern = r'\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Z|a-z]{2,}\b'
- phone_pattern = r'\b\d{3}[-.]?\d{3}[-.]?\d{4}\b'
- pincode_pattern = r'\b\d{6}\b'
- url_pattern = r'http[s]?://(?:[a-zA-Z]|[0-9]|[$-_@.&+]|[!*\(\),]|(?:%[0-9a-fA-F][0-9a-fA-F]))+'

The pattern searching is performed and the semantic type is returned</br>

#### get_entities: </br>
This function assigns named entity recognition value to an input </br>

#### assign_column_ner_classification: </br>
The whole dataframe is broken into chunks of size 25. This function assigns named entity recognition value to new copy of dataframe and returns the new dataframe. It extracts majority of each column and stores it in an array </br>

#### major_col_pred_array: </br>
The function 'major_col_pred_array' takes a dataframe as input and predicts the major column type using NER classification. It assigns a classification to a subset of the data (num_samples) using another function called 'assign_column_ner_classification'. It then calculates the most common classification for each column and stores it in an array called 'majority_arr'. Finally, it prints the most common classification for each column and returns the 'majority_arr'. This function can be useful for quickly identifying the dominant column types in a large dataset. </br>

#### match_column_type: </br>
This function takes a dataset and a column name as input parameters and returns the best matching column type based on the similarity of the values in the column with predefined type maps. Here are the main steps of the function:
- It creates a TfidfVectorizer object to transform the text data into vectors and fit it on the column data.
- It iterates over the predefined type maps and transforms the values into vectors to compute the cosine similarity between the values vector and the text vectors of the column data.
- It computes the average similarity score for each type map and stores it in a dictionary.
- It returns the type map with the highest average similarity score as the best matching column type. </br>

#### classify_columms: </br>
Classifies columns in a CSV dataset using NER and regex-based entity classification.
- Classify object type columns using NLP and regex
- If no named entity is found, regex is used to classify the column
- Classify numerical columns using range-based hierarchical classification
- If no semantic type is found, the column range is calculated and categorization is done as constant, binary, ordinal, interval, and ratio
A Pandas DataFrame with column names and their predicted entity types is returned. </br>


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

