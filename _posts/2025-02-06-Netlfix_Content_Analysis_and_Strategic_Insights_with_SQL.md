---
layout: post
title: Netlfix Content Analysis with SQL
image: "/posts/Netflix.jpg"
tags: [SQL]
---

In this project I will use SQL to analyse Netflix's extensive catalog of movies and TV shows!

# Table of contents

- [00. Project Overview](#project-overview)
- [01.Goals and Objectives](#goals-and-objectives)
- [02. Data Overview](#data-overview)
- [03. SQL Queries](#sql-queries)
- [04. Questions and Findings](#questions-and-findings)
- [05. Key Takeways](#key-takeways)
- [06. Who this Project Helps](#who-this-project-helps)
- [07. Growth & Next Steps](#growth-next-steps)

## Project Overview

This project analyses Netflix’s extensive catalog of movies and TV shows using SQL. By examining key attributes such as content types, production countries, release years, and genres, it uncovers patterns and trends that highlight Netflix's evolving content strategy. The insights gained provide a deeper understanding of how Netflix’s catalogue has grown and diversified over time, as well as how global production and genre preferences have shaped the platform’s offerings.

## 🎯 Goals and Objectives
- Determine the most popular content type each year.

- Identify the most common genres by year and country.

- Track the growth of Netflix content over time.

- Discover country-level production and genre patterns.

## 📊 Data Overview
- **Source:** [Kaggle - Netflix Movies and TV Shows](https://www.kaggle.com/shivamb/netflix-shows)
- **Size:** ~8,800 titles
- **Key Columns:** `show_id`, `title`, `type`, `director`, `cast`, `country`, `release_year`, `duration`, `listed_in`, `rating`
- **Timeframe:** Up to 2021
- **Limitations:** Does not include watch/view count data or user-level metrics

## SQL Queries
Here are the key SQL queries I used to derive insights from the dataset:

### Number of Movies vs TV Shows

```sql 
SELECT 
    category,
    COUNT(show_id) as frequency 
FROM 
    netflix_cleaned
GROUP BY category;
```

### Most Common Content Ratings

```sql
SELECT
    rating,
    COUNT(show_id) as frequency
FROM 
    netflix_cleaned
GROUP BY rating
ORDER BY COUNT(show_id) desc;
```

## Top 10 Countries with Most Content

```sql
SELECT
    country,
    COUNT(show_id) as frequency
FROM 
    netflix_cleaned
WHERE 
    country is not null
GROUP BY 
    country
ORDER BY frequency DESC
LIMIT 10;
```

## Top 10 Countries for TV Shows only

```sql
SELECT 
    country,
    COUNT(show_id) as frequency
FROM 
    netflix_cleaned
WHERE 
    category='TV Show'
GROUP BY 
    country
ORDER BY frequency DESC
LIMIT 10;
```
## Number of Releases per Year

```sql
SELECT 
    EXTRACT(YEAR FROM clean_release_date) AS release_year,
    COUNT(*) as title_count
FROM netflix_cleaned
WHERE 
   EXTRACT(YEAR FROM clean_release_date)>2000
GROUP BY 
    EXTRACT(YEAR FROM clean_release_date)
ORDER BY 
    EXTRACT(YEAR FROM clean_release_date)
```
## How has Netflix's intenational content grown over time

```sql
SELECT 
    EXTRACT(YEAR FROM clean_release_date) AS year,
    COUNT(DISTINCT(country)) AS unique_countries,
    COUNT(*) FILTER (WHERE country != 'United States') as international_countries,
    COUNT(*) AS total_titles,
    ROUND(COUNT(*) FILTER (WHERE country != 'United States')*1.0/COUNT(*),2) AS international_ratio
FROM netflix_cleaned
WHERE EXTRACT(YEAR FROM clean_release_date) >2000
GROUP BY EXTRACT(YEAR FROM clean_release_date)
ORDER BY year;
```

## Which directors have the most content on Netflix

```sql
SELECT
    director,
    COUNT(*) AS title_count
FROM netflix_cleaned
WHERE director is not null
GROUP BY director
ORDER BY title_count DESC;
```

 ## What genres are trending over time

```sql
WITH genre_counts as(
SELECT
    EXTRACT(YEAR FROM clean_release_date) as year,
    "Type" as genre,
    COUNT(*) as total_titles
FROM netflix_cleaned
WHERE EXTRACT(YEAR FROM clean_release_date)>2000
GROUP BY 
    EXTRACT(YEAR FROM clean_release_date),
    "Type"),
ranked_genres as(
SELECT
    year,
    genre,
    total_titles,
    rank() over (partition by year order by total_titles DESC) as genre_rank
FROM genre_counts
)
SELECT
    year,
    genre,
    total_titles
FROM ranked_genres
WHERE genre_rank=1
ORDER BY year,total_titles desc;
```

## Which genres have the highest content volume by country
```sql
WITH unnested_data AS (
    SELECT
        UNNEST(STRING_TO_ARRAY(country, ',')) AS country,
        "Type"
    FROM netflix_cleaned
),
genre_counts AS (
    SELECT
        country,
        "Type" as genre,
        COUNT(*) AS count
    FROM unnested_data 
    GROUP BY country, genre
),
ranked_genres AS (
    SELECT
        country,
        genre,
        count,
        RANK() OVER (PARTITION BY country ORDER BY count DESC) AS rank
    FROM genre_counts
)
SELECT
    country,
    genre
FROM ranked_genres
WHERE rank = 1
ORDER BY count DESC
LIMIT 324
OFFSET 4;
```

## Which TV Shows have the longest run

```sql
SELECT
    title,
    rank() over (order by duration_value desc) as season_rank 
FROM netflix_cleaned
WHERE category='TV Show' 
LIMIT 10;
```
## Running total of titles released per year

```sql
WITH release_year AS (
SELECT 
    EXTRACT(YEAR FROM clean_release_date) AS year,
    COUNT(*) as titles_per_year
FROM netflix_cleaned
WHERE EXTRACT(YEAR FROM clean_release_date)>2000
GROUP BY EXTRACT(YEAR FROM clean_release_date))

SELECT
    year,
    SUM(titles_per_year) over (ORDER BY year) as total_titles
FROM release_year
```
## 🔍 Questions & Findings

Based on the SQL queries, here are some of the insights derived from the data:

### 1.📺 Number of Movies and Tv Shows

- **Movies:** 5377 
- **TV Shows:** 2410 
> **Insight:** Movies make up the majority of Netflix’s catalog.

---

### 2. 🔢 Most Common Content Ratings

| Rating | Count |
|--------|-------|
| TV-MA  | 2,863 |
| TV-14  | 1,931 |
| R      | 806   |

> **Insight:** Netflix content skews toward mature audiences.

---
### 3. 🌍 Top 10 Countries for TV Shows and Total Content

| Country       | Total Content | 
|---------------|---------------|
| United States | 2,555        | 
| India         | 923          | 
| UK            | 397          |

| Country       | TV Shows      | 
|---------------|---------------|
| United States | 705           | 
| UK            | 204           | 
| Japan         | 157           | 

> **Insight:** The US dominates for both Movies and TV Shows, along with the UK. However, for Total Content India is in second place, whereas for TV Shows alone Japan is more popular

--- 

### 4. 🕒 Average Movie Duration 

- **Average Duration:** ~99 minutes
  > **Insight:** Most Netflix movies fall in the 90–110 min range, while most TV Shows on Netflix are only 1 season long

---

### 5. 📊 Distribution of Seasons in TV Shows

| Seasons | Count |
|---------|-------|
| 1       | 1608 |
| 2       | 382  |
| 3+      | 420  |

> **Insight:** Limited series with one season are most common.

---

### 6. 📅 Releases Per Year

![image](https://github.com/user-attachments/assets/547d9d79-7fbf-416d-aae8-3833266de254)


> **Insight:** Releases increased over time with a peak in **2019–2020**, with a dip around 2021. This peak is probably in line with covid where people were stuck at home and more likely to watch Netflix.

---

### 7. 🎬 Top Directors on Netflix

| Director        | Number of Titles |
|-----------------|------------------|
| Raul Campos,    | 18
  Jan Suter       | 18               |
| Marcus Raboy    | 16               |
| Jay Karas       | 14               |

> **Insight:** Some directors appear frequently, especially in animated/kids content.

---
### 8. 🌐 International Outreach Over Time

![image](https://github.com/user-attachments/assets/7129447a-151f-4f58-a0e3-192027f2ccc4)

> **Insight:** Netflix expanded rapidly into non-U.S. markets starting ~2016.

---

### 9. 📈 Trending Genres Over the Years

> **Insight:** Dramas and Documentaries are consistently trending across years.

---

### 10. 🌎 Highest Content per Genre per Country


| Country |  Genre                 | Count |
|---------|------------------------|-------|
| UK      | Documentaries          | 41    |
| Taiwan  | International TV Shows | 31    |
| Egypt   | Comedies               | 29    |

> **Insight:** Countries have genre specialties—Taiwan excels in Internation TV Shows, UK in Documentaries.

---

### 11. 🧮 Longest Running Shows

| Title             | Duration Rank |
|-------------------|---------------|
| Grey’s Anatomy    | 1             |
| NCIS              | 12            |

> **Insight:** Some long-running shows are also syndicated globally.

---

### 12. 🧱 Total Content Over Time

![image](https://github.com/user-attachments/assets/ceb24d62-48ff-4d26-beaa-ea11e1dee531)


> **Insight:** Consistent growth until 2020, slight plateau afterward.

---

## 📈 Key Takeways

- Drama remains Netflix’s most consistently produced and globally distributed genre, making it a cornerstone for international audience appeal and long-term viewer engagement strategies.

- Movies make up nearly 70% of Netflix’s catalog, showing a strong focus on standalone content. However, among TV shows, over 65% have only one season, highlighting a possible gap in long-form, binge-worthy series that drive viewer retention.

- The U.S., India, and the U.K. are leading content producers, highlighting Netflix’s strategic focus on both Western and high-growth Asian markets. India's strong presence reflects increasing localization efforts and demand in emerging regions.

- Netflix has significantly diversified its genre offerings since 2016, likely in response to global expansion and varied user preferences. This breadth supports personalized recommendation algorithms and broadens market reach.

## 👨‍💼 Who This Project Helps

- **Netflix Content Strategists:** To identify under-served genres or countries.
- **Marketing Teams:** To understand regional audience preferences.
- **Executives:** To track global expansion and content growth strategy.
- **Aspiring Data Analysts:** To apply SQL in real-world business contexts.

## 🚀 Growth and Next Steps

- Integrate User Data: Analyse viewing habits and ratings for deeper insights.

- Predict Trends: Use machine learning to forecast future content trends.

- Sentiment Analysis: Assess reviews to understand audience reactions.

- Geospatial Analysis: Visualise content distribution by region.

- Factor in External Events: Study how global events impact content trends.

