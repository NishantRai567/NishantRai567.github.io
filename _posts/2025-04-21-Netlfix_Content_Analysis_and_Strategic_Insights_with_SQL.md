---
layout: post
title: Netlfix Content Analysis with SQL
image: "/posts/Netflix.jpeg"
---
## Project Overview

This project explores and analyzes Netflix's movie and TV show data using SQL. It uncovers trends in content types, production countries, release years, and more to gain insights into Netflix's evolving catalog.

## 📊 Dataset
- **Source:** [Kaggle - Netflix Movies and TV Shows](https://www.kaggle.com/shivamb/netflix-shows)
- **Size:** ~8,800 titles
- **Key Columns:** `show_id`, `title`, `type`, `director`, `cast`, `country`, `release_year`, `duration`, `listed_in`, `rating`
- **Timeframe:** Up to 2021
- **Limitations:** Does not include watch/view count data or user-level metrics

## 🎯 Goals / Objectives
Determine the most popular content type each year.

Identify the most common genres by year and country.

Track the growth of Netflix content over time.

Discover country-level production and genre patterns.

## 🔍 Questions & Findings

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
  Jan Suter       |                  |
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
|---------|----------------------  |       |
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

- 70% of Netflix content is movies, indicating an opportunity to expand TV show offerings, especially multi-season series, to boost retention.

- Strong international presence, especially in India and Japan, suggests potential for more localized productions.

- Dramas and Documentaries dominate, highlighting areas for further investment and marketing focus.

- With 66% of shows having only 1 season, Netflix risks losing users seeking long-form series.



## 📈 Key Findings

- Drama remains Netflix’s most consistently produced and globally distributed genre, making it a cornerstone for international audience appeal and long-term viewer engagement strategies.

- Movies make up nearly 70% of Netflix’s catalog, showing a strong focus on standalone content. However, among TV shows, over 65% have only one season, highlighting a possible gap in long-form, binge-worthy series that drive viewer retention.

- The U.S., India, and the U.K. are leading content producers, highlighting Netflix’s strategic focus on both Western and high-growth Asian markets. India's strong presence reflects increasing localization efforts and demand in emerging regions.

- Netflix has significantly diversified its genre offerings since 2016, likely in response to global expansion and varied user preferences. This breadth supports personalized recommendation algorithms and broadens market reach.

## 👨‍💼 Who This Project Helps

- **Netflix Content Strategists:** To identify under-served genres or countries.
- **Marketing Teams:** To understand regional audience preferences.
- **Executives:** To track global expansion and content growth strategy.
- **Aspiring Data Analysts:** To apply SQL in real-world business contexts.


