# MovieLens Recommendation System using SVD 🎬🍿

A collaborative filtering movie recommendation system built with Singular Value Decomposition (SVD) on the MovieLens 1M dataset. This project analyzes user preferences and predicts ratings to recommend personalized movies.

## 📋 Project Overview

This recommendation system processes over 1 million movie ratings to understand user preferences and provide accurate movie recommendations. Using matrix factorization techniques (SVD), the system identifies latent features in user-movie interactions to predict how users would rate unwatched movies.

## 🎯 Features

- **Collaborative Filtering**: Predicts ratings based on user-movie interaction patterns
- **SVD Matrix Factorization**: Decomposes the user-item matrix into latent factors
- **Gender-Based Analysis**: Analyzes rating differences between male and female users
- **Data Exploration**: Comprehensive analysis of rating distributions and movie popularity
- **Top Movie Identification**: Finds highest-rated and most-reviewed movies
- **Personalized Recommendations**: Generates movie suggestions for individual users

## 📊 Dataset

### MovieLens 1M Dataset

The project uses three main data files:

#### 1. **ratings.dat** (1 million ratings)
- **UserID**: Unique user identifier
- **MovieID**: Unique movie identifier  
- **Rating**: 1-5 star rating
- **Timestamp**: Rating timestamp

#### 2. **movies.dat** (3,706 movies)
- **MovieID**: Unique movie identifier
- **Title**: Movie title with release year
- **Genres**: Pipe-separated genre list

#### 3. **users.dat** (6,040 users)
- **UserID**: Unique user identifier
- **Gender**: M (Male) or F (Female)
- **Age**: Categorical age groups
- **Occupation**: Job category code
- **Zip-code**: Postal code

**Dataset Source**: [GroupLens MovieLens 1M](https://grouplens.org/datasets/movielens/1m/)

## 🏗️ Project Architecture

### Data Pipeline
```
Raw Data (ratings.dat, movies.dat, users.dat)
    ↓
Data Loading & Parsing
    ↓
Data Merging (Pandas merge operations)
    ↓
Exploratory Data Analysis
    ↓
Pivot Table Creation (User-Movie Matrix)
    ↓
SVD Matrix Factorization
    ↓
Rating Prediction & Recommendations
```

### Key Analyses Performed

1. **Overall Movie Ratings**: Average ratings across all users
2. **Gender-Based Preferences**: Rating differences between male and female users
3. **Movie Popularity**: Most reviewed and highest-rated movies
4. **Rating Distribution**: Analysis of rating patterns across demographics
5. **Collaborative Filtering**: User-based and item-based recommendations

## 🛠️ Technologies Used

- **Python 3.x**
- **Pandas** - Data manipulation and pivot tables
- **NumPy** - Numerical operations and matrix computations
- **Matplotlib** - Data visualization
- **Jupyter Notebook** - Interactive development

## 🚀 Getting Started

### Prerequisites

```bash
pip install pandas numpy matplotlib jupyter
```

### Dataset Download

Download the MovieLens 1M dataset from:
https://grouplens.org/datasets/movielens/1m/

Extract the following files to your project directory:
- `ratings.dat`
- `movies.dat`
- `users.dat`

### Running the Project

1. Clone the repository:
```bash
git clone https://github.com/mann-127/movie-lens.git
cd movie-lens
```

2. Ensure data files are in the project directory:
```
movie-lens/
├── Movie_RecSys_SVD.ipynb
├── ratings.dat
├── movies.dat
├── users.dat
└── README for data
```

3. Launch Jupyter Notebook:
```bash
jupyter notebook Movie_RecSys_SVD.ipynb
```

4. Run all cells to:
   - Load and merge the datasets
   - Perform exploratory data analysis
   - Create user-movie rating matrices
   - Apply SVD for recommendations
   - Generate personalized movie suggestions

## 📁 Project Structure

```
movie-lens/
├── Movie_RecSys_SVD.ipynb    # Main recommendation system notebook
├── ratings.dat               # User ratings data (24.6 MB)
├── movies.dat                # Movie metadata (171 KB)
├── users.dat                 # User demographics (134 KB)
├── README for data           # Dataset documentation
├── LICENSE                   # MIT License
└── README.md                 # Project documentation
```

## 🔍 Key Implementation Details

### Data Loading
```python
# Load ratings data
column_list_ratings = ["UserID", "MovieID", "Ratings", "Timestamp"]
ratings_data = pd.read_csv('ratings.dat', sep='::', 
                           names=column_list_ratings, 
                           engine='python')

# Load movies data
column_list_movies = ["MovieID", "Title", "Genres"]
movies_data = pd.read_csv('movies.dat', sep='::', 
                          names=column_list_movies, 
                          engine='python', 
                          encoding='latin-1')

# Load user data
column_list_users = ["UserID", "Gender", "Age", "Occupation", "Zip-code"]
user_data = pd.read_csv("users.dat", sep="::", 
                        names=column_list_users, 
                        engine='python')
```

### Data Merging
```python
# Merge all datasets into comprehensive dataframe
data = pd.merge(pd.merge(ratings_data, user_data), movies_data)
```

### Pivot Table Creation
```python
# Create user-movie rating matrix
mean_ratings = data.pivot_table('Ratings', 
                                index=["Title"], 
                                columns=["Gender"], 
                                aggfunc='mean')
```

## 📈 Analysis Results

### Top Rated Movies (Overall)
- Seven Samurai (1954): 4.56/5
- I Am Cuba (1964): 4.80/5
- Gate of Heavenly Peace, The (1995): 5.00/5

### Most Reviewed Movies
1. American Beauty (1999) - 3,428 ratings
2. Star Wars: Episode IV (1977) - 2,991 ratings
3. Star Wars: Episode V (1980) - 2,990 ratings

### Gender Preference Differences
- **Female-preferred**: Romance, Drama, Comedy
- **Male-preferred**: Action, Sci-Fi, Thriller
- Significant rating differences found in certain genres

## 🎓 SVD Methodology

**Singular Value Decomposition** factorizes the user-movie rating matrix:

```
R ≈ U × Σ × V^T
```

Where:
- **R**: Original user-movie rating matrix (m × n)
- **U**: User-feature matrix (m × k)
- **Σ**: Diagonal matrix of singular values (k × k)
- **V^T**: Movie-feature matrix (k × n)
- **k**: Number of latent features (reduced dimensionality)

This decomposition reveals hidden patterns in user preferences and movie characteristics.

## 📊 Exploratory Data Analysis

The notebook includes:
- Rating distribution analysis
- Gender-based preference comparisons
- Movie popularity metrics
- Rating count statistics
- Genre preference analysis
- Top movies by different criteria

## 🤝 Contributing

Contributions are welcome! Feel free to:
- Improve the recommendation algorithm
- Add more analysis visualizations
- Implement additional filtering methods
- Optimize SVD parameters
- Submit pull requests

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 👤 Author

**mann-127**
- GitHub: [@mann-127](https://github.com/mann-127)

## 🙏 Acknowledgments

- **GroupLens Research** - For providing the MovieLens 1M dataset
- **University of Minnesota** - MovieLens project creators
- **F. Maxwell Harper and Joseph A. Konstan** - 2015. The MovieLens Datasets: History and Context. ACM Transactions on Interactive Intelligent Systems (TiiS)

## 📚 Dataset Citation

```
F. Maxwell Harper and Joseph A. Konstan. 2015. 
The MovieLens Datasets: History and Context. 
ACM Transactions on Interactive Intelligent Systems (TiiS) 5, 4: 19:1–19:19.
```

---

⭐ Star this repository if you find it helpful!

🎬 **Built with passion for movies and machine learning!**
