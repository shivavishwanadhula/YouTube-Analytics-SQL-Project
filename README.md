# YouTube-Analytics-SQL-Project
End-to-end YouTube trending data analysis using MySQL — 40 queries covering data cleaning, KPI reporting, window functions, stored procedures and triggers.


**A complete end-to-end SQL project analyzing YouTube trending video data — from data cleaning and KPI reporting to advanced window functions, stored procedures, and triggers.**



## 📌 Project Overview

This project is designed to simulate a real-world **YouTube Analytics Data Warehouse using SQL**. It covers complete analytics workflows from Data Cleaning to Advanced SQL — using a structured Star Schema database with 4 tables.

The project is divided into **4 major phases** with **40 SQL queries** covering both foundational and senior-level SQL skills.

**Business Objectives:**
1. Identify high-performing videos and channels
2. Analyze engagement and audience behavior
3. Detect viral trends and growth patterns
4. Optimize SQL query performance
5. Create scalable analytics architecture



## 🗂️ Database Schema (Star Schema)

**Database:** `yt_analytics_dw`

```
                    ┌──────────────────┐
                    │  dim_categories  │
                    │  category_id     │
                    │  category_name   │
                    └────────┬─────────┘
                             │
┌──────────────────┐  ┌──────▼───────────────┐  ┌────────────────────────┐
│   dim_channels   │  │      dim_videos       │  │   fact_trending_stats  │
│  channel_id      │◄─│  video_id (PK)        │─►│  stat_id (PK) AUTO INC │
│  channel_title   │  │  title                │  │  video_id (FK)         │
└──────────────────┘  │  publish_time         │  │  trending_date         │
                      │  description          │  │  views                 │
                      │  tags                 │  │  likes                 │
                      │  category_id (FK)     │  │  dislikes              │
                      │  channel_id (FK)      │  │  comments              │
                      └───────────────────────┘  └────────────────────────┘
```


## 🔬 Project Phases

### 🔷 Phase 1 — Data Cleaning & SQL Foundation
> Ensuring data quality and integrity before analysis begins.

| Query | What It Does | SQL Concepts Used |
|-------|-------------|-------------------|
| Q1 | Detect NULL values in `title` and `video_id` | `CASE`, `SUM`, `IS NULL` |
| Q2 | Replace NULL comments with 0 | `IFNULL` |
| Q3 | Find duplicate `video_id` records | `GROUP BY`, `HAVING COUNT(*) > 1` |
| Q4 | Isolate duplicate rows for removal | `ROW_NUMBER()`, `CTE`, `PARTITION BY` |
| Q5 | Standardize channel names (TRIM + UPPER) | `TRIM()`, `UPPER()`, `UPDATE` |
| Q6 | Convert `publish_time` string to DATETIME | `STR_TO_DATE()` |
| Q7 | Find rows with negative views/likes/comments | Constraint / Data Validation |
| Q8 | Build a clean unified analytics VIEW | Multi-table `JOIN`, `CREATE VIEW` |
| Q9 | Detect orphan records in fact table | `LEFT JOIN`, NULL filtering |
| Q10 | Classify videos as Viral / Trending / Normal | `CASE WHEN` with view thresholds |

---

### 🔷 Phase 2 — Business Analytics & KPI Reporting
> Answering real business questions with SQL aggregations and reporting.

| Query | What It Does | SQL Concepts Used |
|-------|-------------|-------------------|
| Q11 | Top 10 most viewed videos | `SUM`, `GROUP BY`, `ORDER BY`, `LIMIT` |
| Q12 | Top channels by total views | `SUM`, `GROUP BY`, `ORDER BY` |
| Q13 | Category-wise view market share (%) | `SUM() OVER()` — Window Function |
| Q14 | Overall KPI snapshot (videos, views, likes, comments) | `COUNT DISTINCT`, `SUM` |
| Q15 | Engagement rate per video (`likes + comments / views`) | Arithmetic, `ROUND()` |
| Q16 | Monthly trending video count | `YEAR()`, `MONTH()`, `STR_TO_DATE()`, `GROUP BY` |
| Q17 | Estimated ad revenue per video (`views / 1000 * 3`) | Revenue formula, `ROUND()` |
| Q18 | Categories with above-average views | Subquery in `HAVING` |
| Q19 | Top channels by total engagement | `SUM(likes + comments)`, `ORDER BY` |
| Q20 | Monthly total views trend | `MONTH()`, `SUM`, `GROUP BY` |

---

### 🔷 Phase 3 — Advanced SQL Analytics
> Production-level SQL techniques used in real analytics engineering roles.

| Query | What It Does | SQL Concepts Used |
|-------|-------------|-------------------|
| Q21 | Rank all videos by views | `DENSE_RANK() OVER(ORDER BY views DESC)` |
| Q22 | Running total of views by date | `SUM(SUM()) OVER(ORDER BY trending_date)` |
| Q23 | 7-day moving average of views | `AVG() OVER(ROWS BETWEEN 6 PRECEDING AND CURRENT ROW)` |
| Q24 | Day-over-day views comparison | `LAG(SUM(views)) OVER(ORDER BY trending_date)` |
| Q25 | Predict next day's views | `LEAD(SUM(views)) OVER(ORDER BY trending_date)` |
| Q26 | Segment videos into 4 performance quartiles | `NTILE(4) OVER(ORDER BY views DESC)` |
| Q27 | First and latest views for each video | `FIRST_VALUE()`, `LAST_VALUE()`, `PARTITION BY` |
| Q28 | Generate a date series (Jan 1–10, 2025) | `Recursive CTE`, `DATE_ADD()`, `UNION ALL` |
| Q29 | Create index on `video_id` for faster queries | `CREATE INDEX`, `SHOW INDEX` |
| Q30 | Analyze query execution plan | `EXPLAIN` |

---

### 🔷 Phase 4 — Senior-Level SQL Reporting
> Complex queries and database automation for production environments.

| Query | What It Does | SQL Concepts Used |
|-------|-------------|-------------------|
| Q31 | Detect viral videos (views > 5M AND likes > 200K) | Multi-condition `WHERE` filter |
| Q32 | Videos above their own category's average views | Correlated Subquery |
| Q33 | Detect view drops between consecutive trending days | `LAG()`, `CTE`, `WHERE views < previous_views` |
| Q34 | Month-over-month view growth rate (%) | `LAG()`, `CTE`, growth rate formula |
| Q35 | Category summary VIEW for reporting | `CREATE VIEW`, `COUNT DISTINCT`, `AVG` |
| Q36 | Engagement funnel (views → likes → comments) | `SUM` aggregation |
| Q37 | Category-wise pivot report by month (Jan, Feb) | `CASE WHEN MONTH()`, Pivot pattern |
| Q38 | Create CTAS summary table for top channels | `CREATE TABLE AS SELECT` |
| Q39 | Stored Procedure to fetch top 10 videos | `DELIMITER`, `CREATE PROCEDURE`, `CALL` |
| Q40 | Trigger to log every new video insert | `CREATE TRIGGER`, `AFTER INSERT`, `audit_log` table |

---

## 🛠️ SQL Skills Covered

| Category | Skills |
|----------|--------|
| **Data Cleaning** | NULL handling, IFNULL, COALESCE, duplicate detection, data validation |
| **Joins & Views** | INNER JOIN, LEFT JOIN, CREATE VIEW, orphan detection |
| **Aggregations** | GROUP BY, HAVING, SUM, COUNT, AVG, ROUND |
| **Subqueries** | Scalar subquery, correlated subquery, subquery in HAVING |
| **Window Functions** | DENSE_RANK, ROW_NUMBER, NTILE, LAG, LEAD, FIRST_VALUE, LAST_VALUE, SUM OVER, AVG OVER |
| **CTEs** | Standard CTE, Recursive CTE |
| **Date Functions** | STR_TO_DATE, YEAR, MONTH, DATE_ADD |
| **Optimization** | CREATE INDEX, SHOW INDEX, EXPLAIN |
| **Automation** | Stored Procedures, Triggers, CTAS Tables, Audit Logging |

---

## 💡 Key SQL Insights from the Project

1. Viral videos (views > 5M) show significantly higher engagement rates — likes and comments amplify visibility.
2. Entertainment and Music categories lead overall view market share.
3. Channels with consistent trending appearances show stronger long-term performance.
4. Monthly analysis reveals seasonal spikes that can guide content publishing strategy.
5. Likes-to-view ratio is a stronger quality signal than raw view count alone.
6. Running totals and moving averages give better trend visibility than point-in-time snapshots.
7. Trend drop detection via `LAG()` helps flag declining content quickly.
8. `EXPLAIN` + Indexing on `video_id` dramatically improves query performance on large datasets.
9. Stored Procedures and Triggers bring automation and governance to the analytics pipeline.
10. CTAS tables pre-aggregate heavy queries for faster downstream reporting.

---

## 📁 Project Structure

```
📦 youtube-analytics-sql/
├── 📄 README.md
├── 📄 youtube_analytics_project.sql     ← Full project (all 40 queries)
├── 📂 phase_1_data_cleaning/
│   └── cleaning_queries.sql             ← Q1 to Q10
├── 📂 phase_2_business_analytics/
│   └── kpi_queries.sql                  ← Q11 to Q20
├── 📂 phase_3_advanced_sql/
│   └── advanced_queries.sql             ← Q21 to Q30
├── 📂 phase_4_senior_reporting/
│   └── senior_queries.sql               ← Q31 to Q40
└── 📂 schema/
    └── create_tables.sql                ← DDL: All 4 table definitions
```

---

## 🚀 How to Run This Project

```sql
-- Step 1: Create the database
CREATE DATABASE yt_analytics_dw;
USE yt_analytics_dw;

-- Step 2: Create all 4 tables (schema/create_tables.sql)
-- dim_categories, dim_channels, dim_videos, fact_trending_stats

-- Step 3: Load your YouTube trending data into the tables

-- Step 4: Run the analytics view first (required by all phases)
-- This creates: vw_clean_youtube_data

-- Step 5: Run each phase file in order
-- Phase 1 → Phase 2 → Phase 3 → Phase 4

-- Step 6: Call the stored procedure
CALL top_videos();

-- Step 7: Query the views
SELECT * FROM vw_clean_youtube_data;
SELECT * FROM vw_executive_dashboard;
SELECT * FROM audit_log;
```

> 💡 **Dataset:** Download the [YouTube Trending Videos Dataset](https://www.kaggle.com/datasets/datasnaek/youtube-new) from Kaggle to run this project with real data.

## 🧠 Skills Demonstrated

| Skill Area | Level |
|---|---|
| Data Cleaning & Quality | ████████████████████ Advanced |
| Joins & Views | ████████████████████ Advanced |
| Aggregations & KPIs | ████████████████████ Advanced |
| Subqueries | ████████████████████ Advanced |
| Window Functions | ████████████████████ Advanced |
| CTEs & Recursive CTEs | ████████████████████ Advanced |
| Query Optimization | ████████████░░░░░░░░ Intermediate–Advanced |
| Stored Procedures | ████████████████████ Advanced |
| Triggers & Audit Logging | ████████████████████ Advanced |






**[👤 Author]**

**SHIVA VISHWANADHULA**

📧 [charyshiva842@gmail.com](mailto:charyshiva842@gmail.com)
🔗 [LinkedIn](https://www.linkedin.com/in/shiva-vishwanadhula/)



⭐ **If this project helped you, drop a star!** ⭐

*Built to demonstrate real-world SQL skills from data cleaning to advanced analytics.*
