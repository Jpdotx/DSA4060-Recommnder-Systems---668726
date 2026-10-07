# DSA 4060 Personalized Movie Recommender

## Student Details
- **Name:** Sundus Moheddin
- **Student ID:** 668726
- **Assigned User ID:** 27 (last two digits 26: 26 MOD 40 = 26, + 1 = 27)

## Project Objective
This project builds a simple content-based movie recommender for one assigned user (User 27). It profiles the user's taste from their historical ratings and recommends five movies they have not yet rated, using movie genres as the basis for similarity.

## Datasets
- `movies.csv`: catalogue of 36 movies with `movie_id`, `title` and pipe-separated `genres`.
- `ratings.csv`: 440 historical ratings from 40 users with `user_id`, `movie_id` and `rating`. Neither file has missing values.

## Method / Approach
1. Loaded and inspected both files, then filtered the ratings to User 27 (11 rated movies, mean rating 2.82).
2. Profiled the user: top-rated movies and average rating per genre showed a clear preference for Animation/Family (Coco, 4.5).
3. Treated movies rated 4.0 or higher as "liked" (only Coco).
4. Converted genres to numeric vectors with `CountVectorizer` and computed **cosine similarity** between every movie and the liked movie.
5. Removed all movies User 27 has already rated and took the top five. Because only two unrated movies share a genre with Coco, the remaining ties were broken using the user's average rating for each candidate's genres.

## How to Run the Notebook
Requirements: Python 3, `pandas`, `scikit-learn`, `jupyter`.
```
pip install pandas scikit-learn jupyter
jupyter notebook DSA4060_Recommender_668726.ipynb
```
Keep `movies.csv` and `ratings.csv` in the same folder as the notebook, then run all cells from top to bottom (Kernel > Restart & Run All).

## Recommendation Results
| Rank | Movie | Genres |
|------|-------|--------|
| 1 | Finding Nemo | Animation, Adventure |
| 2 | Toy Story | Animation, Comedy |
| 3 | La La Land | Romance, Musical |
| 4 | The Hangover | Comedy |
| 5 | Mad Max: Fury Road | Action, Adventure |

**Interpretation:** The top two share the Animation genre with Coco, the user's only highly rated movie. Ranks 3 to 5 have no genre overlap with Coco, so they were chosen from genres the user rated relatively well (Romance and Comedy at 3.0, Adventure at 3.5). They are weaker recommendations than the first two.

## Limitation and Suggested Improvement
- **Limitation:** The profile rests on a single liked movie (Coco), so only two movies had any genre similarity and the other three needed a fallback rule. Genres are also a coarse description of a film.
- **Improvement:** Add collaborative filtering (use the ratings of similar users) in a hybrid model, and/or use a user-relative "like" threshold so there are more positive examples to learn from.
