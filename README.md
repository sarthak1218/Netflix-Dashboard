# Netflix-Dashboard

import pandas as pd
data = pd.read_csv('netflix_data.csv')
print("Data Preview:")
print(data.head())

# remove duplicates and handle missing values
data.drop_duplicates(inplace=True)
data.dropna(subset=['Title', 'Genre', 'Release Year', 'Rating', 'Views'], inplace=True)

# 'Release Year' to datetime 
data['Release Year'] = pd.to_datetime(data['Release Year'], errors='coerce').dt.year

# Group by Genre to get the total views per genre
genre_views = data.groupby('Genre')['Views'].sum().reset_index()

# Sort genres by views
genre_views = genre_views.sort_values(by='Views', ascending=False)

# Save the cleaned data to a new CSV file
data.to_csv('cleaned_netflix_data.csv', index=False)

# Save the genre views data to another CSV file
genre_views.to_csv('genre_views.csv', index=False)

print("Data Cleaning Complete. Cleaned files saved as 'cleaned_netflix_data.csv' and 'genre_views.csv'.")
