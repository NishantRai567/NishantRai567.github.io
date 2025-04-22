---
layout: post
title: Netlfix Content Analysis with SQL
image: "/posts/Netflix.jpeg"
---
## Description

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


## 🛠 Technologies Used

SQL (PostgreSQL/PG Admin) — for querying and cleaning data

VS Code / SQ Tools — for local SQL work

Excel — for visualisation


## 💼 Business Impact & Skills Demonstrated

- 📈 **Strategic Insights:** Identified content type trends (e.g., 69% of content are movies), helping suggest platform investment focus.
- 🌍 **Market Expansion Analysis:** Analysed country-wise and language trends to infer Netflix's global strategy post-2016.
- 🎯 **Content Planning Support:** Highlighted gaps in long-form TV series and regional genre distribution.
- 🧠 **Analytical Skills:** Applied SQL techniques including CTEs, window functions, and case logic to answer real business questions.
- 📊 **Visualization & Reporting:** Converted raw SQL results into Excel dashboards; T

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

## 🚀 How to Run

1. Clone the repository:
   ```bash
   git clone https://github.com/NishantRai567/Netflix_Project.git
   ```

2. Open the database using your SQL tool.

3. Run queries from the /02_sql/ folder to explore insights
