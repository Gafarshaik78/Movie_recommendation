# Movie_recommendation System
The following project represents the development of a movie recommendation system using two important techniques:
1. **Collaborative Filtering**
2. **Content-Based Filtering**

It analyzes movie, rating, and tag data, plots model performance charts, and shows data visualizations to explore trends.


## Dataset Information
The system uses three datasets:
1. `movies.csv`: Contains movie details (ID, title, genres).
2. `ratings.csv`: Contains user ratings for movies.
3. `tags.csv`: Contains user-provided tags for movies.

### Example Dataset Structure:
- **movies.csv**:
  ```
  movieId, title, genres
  1, Toy Story (1995), Adventure|Animation|Children
  ```

- **ratings.csv**:
  ```
  userId, movieId, rating, timestamp
  1, 1, 4.0, 964982703
  ```

- **tags.csv**:
  ```
  userId, movieId, tag, timestamp
  15, 1, Pixar, 1138537770
  ```

---

## Features
### Collaborative Filtering
- Uses **cosine similarity** to find the similarity between users.
- Recommend movies to a user based on ratings from other similar users.

### Content-Based Filtering
- Calculates the similarity between movies by **TF-IDF Vectorization** using both tags and genres.
- Suggests similar movie recommendations based on a movie selected from the dataset.

### Evaluation
- Model performance was measured by the **Root Mean Square Error (RMSE)**.
  
### Visualizations
1. **Rating Distribution**
2. **Number of Ratings per Movie**
3. **Average Ratings per Movie**
4. **User Similarity Heatmap**
5. **Movie Similarity Heatmap**
6. **Word Cloud for Tags**

---

## Installation
1. Clone the repository:
   ```bash
   git clone <repository_url>
   ```
2. Navigate to the project directory:
   ```bash
   cd movie-recommendation-system
   ```
3. Install required Python packages:
   ```bash
   pip install -r requirements.txt
   ```

---

## Usage
1. Load datasets:
   ```python
   movies_df = pd.read_csv('./data/movies.csv')
   ratings_df = pd.read_csv('./data/ratings.csv')
   tags_df = pd.read_csv('./data/tags.csv')
   ```
2. Run the recommendation system:
   ```python
   recommend_movies_user_based(user_id=1, num_recommendations=5)
   recommend_movies_content_based(movie_id=1, num_recommendations=5)
   ```
3. Visualize data:
   ```python
   # Example visualization
   sns.histplot(ratings_df['rating'], bins=10, kde=True)
   plt.show()
   ```
4. Evaluate models:
   ```python
   print('RMSE:', rmse)
   ```

---

## Example Functions
### Recommend Movies (User-Based)
```python
def recommend_movies_user_based(user_id, num_recommendations=5):
    similar_users = user_similarity_df[user_id].sort_values(ascending=False)[1:num_recommendations + 1]
    recommendations = []
    for sim_user in similar_users.index:
        user_movies = user_movie_matrix.loc[sim_user]
        recommendations.extend(user_movies[user_movies > 0].index)
    return list(set(recommendations) - set(user_movie_matrix.loc[user_id][user_movie_matrix.loc[user_id] > 0].index))[:num_recommendations]
```

### Recommend Movies (Content-Based)
```python
def recommend_movies_content_based(movie_id, num_recommendations=5):
    similar_movies = content_similarity_df[movie_id].sort_values(ascending=False)[1:num_recommendations + 1]
    return similar_movies.index.tolist()
```

---

## Requirements
- Python 3.7+
- pandas
- numpy
- scikit-learn
- matplotlib
- seaborn
- wordcloud

Install dependencies using:
```bash
pip install pandas numpy scikit-learn matplotlib seaborn wordcloud
```

---

## Visualizations
Here are some key visualizations included:
1. **Rating Distribution**:
   Displays the frequency of ratings in the dataset.

2. **User Similarity Heatmap**:
   Shows similarity scores between users for collaborative filtering.

3. **Word Cloud**:
   Visualizes the most common movie tags.

---

## Future Enhancements
1. Add hybrid recommendation systems.
2. Include time-based collaborative filtering.
3. Integrate with real-world movie APIs (e.g., TMDb).


