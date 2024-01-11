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
