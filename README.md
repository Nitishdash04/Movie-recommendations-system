<t1>Movie-recommendations-system</t1>

# Movie Recommendation System

This repository contains a simple **Movie Recommendation System** built using **Python** and **Pandas**. The system provides recommendations based on user ratings using various collaborative filtering methods.

## Table of Contents

- [Project Overview](#project-overview)
- [Features](#features)
- [Dataset](#dataset)
- [Installation](#installation)
- [Usage](#usage)
- [Recommendation Techniques](#recommendation-techniques)
- [Contributing](#contributing)

## Project Overview

This project demonstrates a **movie recommendation system** that suggests movies to users based on user ratings. It uses the **MovieLens** dataset, which contains movie ratings provided by users. The system implements basic recommendation algorithms using collaborative filtering.

## Features

- User-based collaborative filtering
- Item-based collaborative filtering
- Simple statistical methods for recommendations
- Built using Python and Pandas
- Ability to handle large datasets

## Dataset

We use the [MovieLens dataset](https://grouplens.org/datasets/movielens/) in this project. The dataset contains millions of user ratings on a variety of movies. The dataset has the following format:

- `movies.csv`: Contains information about movies (movie ID, title, genres)
- `ratings.csv`: Contains user ratings (user ID, movie ID, rating, timestamp)

You can download the dataset from [here](https://grouplens.org/datasets/movielens/).

## Installation

1. Clone the repository:

```bash
git clone https://github.com/your-username/movie-recommendation-system.git
cd movie-recommendation-system
```

2. Install the required dependencies:

```bash
pip install -r requirements.txt
```

3. Download the MovieLens dataset from the above link and place the files (`movies.csv`, `ratings.csv`) in the `data/` directory.

## Usage

To generate movie recommendations based on user preferences, run the `recommend.py` script:

```bash
python recommend.py
```

You can also specify different filtering methods (user-based or item-based):

```bash
python recommend.py --method user_based
```

### Sample Code (Python and Pandas)

Here's an overview of the Python code used to generate recommendations:

```python
import pandas as pd

# Load datasets
movies = pd.read_csv('data/movies.csv')
ratings = pd.read_csv('data/ratings.csv')

# Merge datasets
data = pd.merge(ratings, movies, on='movieId')

# Create a pivot table with users and movie ratings
user_movie_matrix = data.pivot_table(index='userId', columns='title', values='rating')

# Calculate the correlation between movies
movie_similarity = user_movie_matrix.corr(method='pearson', min_periods=50)

def get_movie_recommendations(movie_name, num_recommendations=5):
    similar_movies = movie_similarity[movie_name].dropna()
    similar_movies = similar_movies.sort_values(ascending=False)[1:num_recommendations+1]
    return similar_movies

# Example usage
recommended_movies = get_movie_recommendations('Toy Story (1995)')
print(recommended_movies)
```

## Recommendation Techniques

- **User-based collaborative filtering**: Recommends movies based on similarity between users.
- **Item-based collaborative filtering**: Recommends movies based on similarity between movies.
- **Pearson Correlation Coefficient**: Used for finding similar users/movies.

## Contributing

Feel free to fork this repository and submit pull requests. Contributions are welcome!
