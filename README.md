# Netflix Movies and TV Shows data analysis using SQL
![netflix logo](https://github.com/MUMTAHINA-ARBI/sql-project-netflix-dataset/blob/main/netflix-logo.png)

## Overview
This project uses SQL to analyze Netflix's movie and TV show data comprehensively. The goal is to extract valuable insights and answer various business questions based on the dataset. The following README provides a detailed account of the project's objectives, business problems, solutions, findings, and conclusions.
### Dataset
The data for this project is sourced from the Kaggle dataset:
Dataset Link: (https://www.kaggle.com/datasets/shivamb/netflix-shows)

#### Business Problems & Solutions

-- 1. Count the number of Movies vs TV Shows
SELECT 
	type,
	COUNT(*)
FROM college.netflix
GROUP BY 1;

-- 2. Find the most common rating for movies and TV shows
SELECT
  type, rating
  FROM ( SELECT
  type,rating, COUNT(*),
  RANK() OVER(PARTITION BY type ORDER BY COUNT(*) DESC) as ranking
  FROM college.netflix
  GROUP BY 1, 2) as t1
WHERE ranking = 1;

-- 3. List all movies released in a specific year (e.g., 2020)
SELECT * FROM college.netflix
WHERE release_year = 2020; 

-- 4. Find all content without a director
SELECT * FROM college.netflix
WHERE  director='' ;

-- 5. List all movies that are documentaries
SELECT *
FROM college.netflix;
SELECT * 
FROM college.netflix
WHERE listed_in LIKE '%documentaries%';

-- 6. Count the number of content items in each genre

SELECT listed_in, COUNT(*) AS content_count
FROM college.netflix
GROUP BY listed_in
ORDER BY content_count DESC;

-- 7. List all TV shows with more than 5 seasons
SELECT * 
FROM college.netflix
WHERE type = 'TV Show' 
AND CAST(SUBSTRING_INDEX(duration, ' ', 1) AS UNSIGNED) > 5;

-- 8. Identify the longest movie
SELECT * 
FROM college.netflix
WHERE type= 'Movie'
ORDER BY CAST(SUBSTRING_INDEX(duration, ' ', 1) AS UNSIGNED) DESC
LIMIT 1;
