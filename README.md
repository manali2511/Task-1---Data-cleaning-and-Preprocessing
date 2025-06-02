import pandas as pd

# 1. Load the dataset
df = pd.read_csv('netflix_titles.csv')

# 2. Drop duplicate rows
df.drop_duplicates(inplace=True)

# 3. Handle missing values
df['director'].fillna('Not Specified', inplace=True)
df['cast'].fillna('Not Specified', inplace=True)
df['country'].fillna('Unknown', inplace=True)
df['rating'].fillna('Not Rated', inplace=True)
df['duration'].fillna('Unknown', inplace=True)

# Convert 'date_added' to datetime
df['date_added'] = pd.to_datetime(df['date_added'], errors='coerce')

# 4. Standardize text values
df['type'] = df['type'].str.strip().str.lower()  # e.g., "Movie", "TV Show"
df['country'] = df['country'].str.strip().str.title()  # e.g., "united states" -> "United States"

# 5. Rename columns to lowercase with underscores
df.columns = df.columns.str.strip().str.lower().str.replace(' ', '_')

# 6. Fix data types
df['release_year'] = df['release_year'].astype(int)

# 7. Save the cleaned dataset
df.to_csv('cleaned_netflix_titles.csv', index=False)
