# 🎬 BingePlay: SQL Data Analysis & User Engagement Tracking

## 📌 Project Overview
BingePlay is a comprehensive SQL and Python-based data analytics project designed to extract actionable insights from a simulated streaming platform's database. The goal of this project is to analyze user engagement, track subscription upgrades, identify top-performing content, and detect early signals of user churn. 

All analyses were executed using **MySQL** for database management and **Jupyter Notebook (Python, Pandas, SQLAlchemy)** for querying and data manipulation.

## 🛠️ Tech Stack
*   **Database:** MySQL
*   **Language:** SQL, Python
*   **Libraries:** Pandas, SQLAlchemy, PyMySQL
*   **Environment:** Jupyter Notebook

## 🔍 Project Steps & Key Analysis (Sneak Peek)
Here is a breakdown of the core business questions solved in this project, demonstrating the step-by-step analytical approach:

**1. Revenue & User Base Analysis**
*   Calculated the total active revenue generated in Q1 2024 by filtering active subscriptions and summing the monthly prices.
*   Analyzed signup momentum to find the month with the highest new user registrations, handling ties using conditional logic.

**2. Content & Device Insights**
*   Determined the most popular viewing device (e.g., Smart TVs vs. Mobile) and the average watch time per session.
*   Compared the performance of "Original" vs. "Acquired" content based on total unique viewers.

**3. Advanced User Behavior & Traps Overcome**
*   **The NULL Trap (Never Watched):** Identified users who signed up in Q1 but never watched any shows. *Solution:* Avoided the `NOT IN` subquery trap (which fails with `NULL` user_ids) by using a `LEFT JOIN` and counting where `session_id IS NULL`.
*   **Over-paying Users:** Found users on 'Premium' or 'Family' plans who exclusively watched 'Basic' tier shows using `CTE`s and `NOT EXISTS` to verify their complete watch history.
*   **Cliffhanger Comebacks:** Detected users who left a show incomplete (`completed = 0`) but returned to watch it within 1-7 days. *Solution:* Implemented a **Self-Join** on the `watch_sessions` table filtering with `DATE_ADD`.

**4. The "Killer" Queries (Complex Logic)**
*   **Consecutive-Week Engagement (Gaps-and-Islands):** Identified highly engaged users who maintained a streak of watching content for 4+ consecutive weeks. *Solution:* Extracted `WEEKOFYEAR()`, used the `ROW_NUMBER()` window function, and grouped by the difference to dynamically calculate streak lengths.
*   **Churn Signal Detection:** Flagged users whose watch time dropped by 50% or more between May and June. *Solution:* Avoided using the `LAG()` window function directly in the `WHERE` clause (which misses zero-minute months). Instead, used **Conditional Aggregation within a CTE** to accurately calculate the month-over-month drop percentage.

## ⚙️ How to Run This Project Locally

If you want to test the queries or see the dynamic dataframes, follow these steps:

1. **Download the Data:** Get the SQL database dump and the Jupyter Notebook from this link: 🔗 **https://drive.google.com/drive/folders/1iYoD0KDZ0qLjlqLzUtrTO9jpIrf-VjwJ?usp=sharing**
2. **Database Setup:** 
   * Open MySQL Workbench.
   * Run `CREATE DATABASE bingeplay; USE bingeplay;`
   * Import the `bingeplay.sql` file.
3. **Environment Setup:** Install required libraries via terminal: `pip install pandas sqlalchemy pymysql jupyter`
4. **Execution:** Open the `.ipynb` file, update the MySQL password in the `create_engine` connection string, and hit **"Restart Kernel and Run All Cells"** to view the outputs dynamically.

---
BingePlay Streaming Analytics Project

## 👨‍💻 About the Author
**Tanmay Purushottam Bokade**  
*Computer Engineering Student | Tech & Data Enthusiast*
Let's connect and talk about data, tech, and building cool things!
* 💼 **LinkedIn:** https://www.linkedin.com/in/tanmay-bokade-210280345/
* 🐙 **GitHub:** https://github.com/TanmayB22122006

*Developed as part of a rigorous SQL analytics evaluation emphasizing data accuracy and optimal query structuring.*
