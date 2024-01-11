# Coursera Social Media Project
- Exploring simulated social media data. For the purposes of the project, we'll refer to the data as tweets following X, formerly known as Twitter.

### Marc Mascaro
### January 2024

# Import required libraries
The following libraries are used:
| Library | Purpose |
|---------|---------|
| Numpy | randomly choose categories and generate randomm number of "likes" |
| Pandas | to leverage dataframe capabillities |
| Matplotlib | to display graphs |
| Plotly | to create graphs |

# Generate social media data
In this step, we will generate random tweets data to analyze. We start by building a python list of categories.
```
categories = ['Food', 'Travel', 'Sports', 'Fitness',
             'Music', 'Health']
```
With the categories in hand, we can create a python dictionary containing **Date**, **Category**, and **Likes**. We use pandas *.date_range()* function to generate 500 dates, starting with January 1, 2022. We use numpy *random.choice()* generate random category entries. Finally, we use numpy *random.randint()* to generate a random integer for number of "likes."
```
tweet_dict = {'Date': pd.date_range('2022-01-01', periods = 500),
              'Category': [np.random.choice(categories) for _ in range(500)],
              'Likes': np.random.randint(0, 10000, size = 500)}
``` 

# Load data into pandas dataframe and explore data
In this step, we load the created dictionary data into a pandas dataframe using the *DataFrame.from_dict()* function and display the first few rows with the *.head()* function.
```
tweets_df = pd.DataFrame.from_dict(tweet_dict)
tweets_df.head()
```

Next, we display information about the *tweets_df* dataframe using the *.info()* function. This function displays information about the dataframe including the names of columns, number of records in each column, and column data type.
```
tweets_df.info()
```
| Column | Data Type |
|--------|-----------|
| Date | datetime |
| Category | object |
| Likes | integer |

Next, we use the *.describe()* function to display summary statistics for the numeric columns. Statistics include record count, mean, standard deviation, min, max, and quartiles.
```
tweets_df.describe(include = ['integer'])
```

Finally, we'll display the count of records for each category by using the *.value_counts()* function. 
```
cat_counts = tweets_df.Category.value_counts().reset_index()
cat_counts
```
| Category | Count |
|----------|-------|
| Sports | 93 |
| Travel | 88 |
| Food | 84 |
| Fitness | 81 |
| Music | 79 |
| Health | 75 | 

# Cleaning the data
The nature of how we generated the data means there is no data cleaning required. For example, the **Date** field is already in the *datetime* format, so no change of data type is needed. Similalry, **Likes** was created using the numpy *random.randint()* function as an integer field.
In addition to ensuring proper data types, the cleaning step would also include an examination and resolution of missing values and duplicate rows. These would be examined using the following code, both of which returned a value of zero (0) indicating no missing values and no duplicate rows.
```
print('Missing values:\n', tweets_df.isnull().sum())
print('Duplicate rows: ', tweets_df.duplicated().sum())
```
