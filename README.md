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

# Visualize and analyze the data
In this section, we prepare and display visualizations to help draw inferences from the data.

We start by examining a histogram of likes. We used the Plotly histogram feature to include a box plot above the histogram that helps us see this is a fairly normal distribution.
```
fig = px.histogram(tweets_df, x = 'Likes',
                  nbins = 20,
                  marginal = 'box',
                  title = 'Distribution of Likes')

fig.show()
```
![image](https://github.com/mac-data-marcm/social_media_proj/assets/148590292/f98fe5db-af24-4fca-a280-a5b65d995cc1)

Next, we look at a count of tweets by category. We see that random seeding of categories placed a similar number of "tweets" in each Category.
```
fig = px.bar(cat_counts, x = 'Category', y = 'count',
             text_auto = '.2f',
             title = 'Count of tweets by Category')

fig.show()
```
![image](https://github.com/mac-data-marcm/social_media_proj/assets/148590292/dcfa3c55-d963-431b-88c6-5c6089a36cec)

Next, we take a look at a box plot showing the relationship between **Likes** and **Category**. We note the following:
- The distributions are similar
- There is slight skewing - Travel, Food, Health, and Sports to the left; and Fitness and Music to the right
- Dispersions are quite similar

```
fig = px.box(tweets_df, y = 'Category', x = 'Likes'
            )

fig.show()
```
![image](https://github.com/mac-data-marcm/social_media_proj/assets/148590292/17e02b7c-7490-4f4e-b965-c08eb5105a76)

Next, we look at some statistics on the data, starting with finding the mean value of **Likes**, using the statement:
```
print('Mean of Likes: ', tweets_df.Likes.mean())
```
The resulting mean of **Likes" is: **5091.8**

We also look at the mean of **Likes** for each category, using the pandas *.grouby()* function and then display the results in a chart. We can see that our generated data is fairly uniform.
```
mean_cat = tweets_df.groupby('Category').Likes.mean().reset_index()
```
```
fig = px.bar(mean_cat, x = 'Category', y = 'Likes',
             text_auto = '.2f',
             title = 'Mean Likes by Category')
fig.show()
```
![image](https://github.com/mac-data-marcm/social_media_proj/assets/148590292/35cc1cda-3fae-447c-bc61-9eb96578538e)

# Conclusions
Throughout the document, we described the process followed and the results found. It would be interesting to run this same scenario with real tweet data. I feel the simulated data is perhaps a bit to clean to draw useful insights.
Regardless, this was fun. I prefer to use Plotly for plots as, in my opinion, it provide cleaner plots for publication or display on a web page.
Thank you.

# Project Link
The link to project repository is https://github.com/mac-data-marcm/social_media_proj/tree/main.
