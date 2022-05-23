# Movies-ETL
### Exctract, Transform, Load

## Overview
An automated pipeline was created for Amazing Prime that takes in new movie data, performs the appropriate transforamtions, and loads the data into tables. I created one function that takes in files from Wikipedia data, Kaggle metadata, and the MovieLens rating data. The ETL process was performed by adding the data to a PostgreSQL database

### Write an ETL Function to Read Three Data Files
A function to read in the three data files was created and named "extract_transform_load." The Kaggle and MovieLens ratings CSV files were read as Pandas DataFrames. The Wikipedia JSON file was opened and converted to JSON raw data then read as a Pandas DataFrame. Then the three DataFrames were returned. A path to the data files was created by naming variables. The DataFrames were set to equal the file names and the variables previously created were reassigned to the variables in the return statement. Then all three files were converted to DataFrames.

#### wiki_movies_df DataFrame
![wiki_movies](https://github.com/jstearns1988/Movies-ETL/blob/main/Resources/wiki_movies_df.png?raw=true)

#### kaggle_metadata DataFrame
![kaggle_metadata](https://github.com/jstearns1988/Movies-ETL/blob/main/Resources/kaggle_metadata.png?raw=true)

#### ratings DataFrame
![ratings](https://github.com/jstearns1988/Movies-ETL/blob/main/Resources/ratings.png?raw=true)

### Extract and Transform Wikipedia Data
The ETL function that reads the three data files was added, the code that creates the wiki_movies_df DataFrame was removed, and a list comprehension was written that filters out TV shows from the wiki_movies_raw file. A new list comprehension was written to iterate through the cleaned wiki movies list. Then the cleaned movies list was read in as a DataFrame. A try-except block was created to catch errors while extracting the IMDB IDs with a regular expression string and dropped any imdb_id duplicates. Another list comprehension was written to keep the columns that have non-null values from the DataFrame followed by the creation of the wiki_movies_df DataFrame from the list. A new variable to hold all the non-null values from the "Box office" column was created. I then converted the box office data to string values using the lambda and join functions. I then wrote another regular expression to match the six elements of form_one of the box office data. To match the three elements of form_two, a regular expression was written. Then the parse_dollars() function was added. Code to clean the box office column in the wiki_movies_df DataFrame using the form_one and form_two lists was added. Following this step; the budget, release date, and running time columns in the wiki_movies_df were cleaned. Three variables for the Wikipedia data, the Kaggle metadata, and the MovieLens rating data files and were set to equal the function created earlier in this analysis. The wiki_movies_df was set to equal the wiki_file variable. The columns from wiki_movies_df DataFrame were added to a list.

#### wiki_movies_df
![wiki_movies_df](https://github.com/jstearns1988/Movies-ETL/blob/main/Resources/wiki_movies2.png?raw=true)

#### wiki_movies_df Colum Names
![wiki_movies_df columns](https://github.com/jstearns1988/Movies-ETL/blob/main/Resources/wiki%20columns.png?raw=true)

### Extract and Transform the Kaggle data
The "extract_transform_and load" function was added to read the kaggle_metadata and ratings DataFrames. Code created in the Extract and Transform Wikipedia steps earlier was reused. The Kaggle metadata was cleaned. I then merged the wiki_movies_df and kaggle_metadata DataFrames and a new movies_df DataFrame was created. Unnecessary columns in movies_df were dropped. The fill_missing_kaggle_data() function was added that fills in the missing Kaggle data on the movies_df Dataframe. I called the fill_missing_kaggle_data() with the movies_df DataFrame and the Kaggle and Wikipedia columns to be cleaned as the arguments. The movies_df DataFrame was filtered to keep the necessary columns. I renamed the columns in the movies_df DataFrame.the ratings DataFrame was merged with the movies_df DataFrame and named movies_with_ratings_df and then cleaned. I created a path to the Wikipedia data, the Kaggle metadata, and the MovieLens rating data files. Then the three variables were set to equal the "extract_transform_load" function.

#### movies_with_ratings_df
![movies_with_ratings](https://github.com/jstearns1988/Movies-ETL/blob/main/Resources/movies%20with%20ratings.png?raw=true)

### Create the Movie Database
Additional code was added to the code above to create a SQL database from the movies_df DataFrame and MovieLens rating data. I ran two queries to confirm the number of rows from the movies table and the ratings table.

#### Movies Table Count Query
![Movies Query](https://github.com/jstearns1988/Movies-ETL/blob/main/movies_query.png?raw=true)

#### Ratings Table Count Query
![ratings]()
