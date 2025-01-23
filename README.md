# Music Store Analysis Project

## Project Overview

The **Music Store Analysis Project** is a comprehensive SQL-based data analysis project. This project involves analyzing a digital music store's database to extract valuable business insights, including customer behaviors, popular genres, and revenue trends. By solving business-related queries, the project demonstrates proficiency in SQL for data exploration and analysis.

---

## Key Features

- **Database Queries**:
  - Complex queries to derive meaningful insights.
  - Usage of common table expressions (CTEs) for structured query development.
  - Aggregations and window functions for advanced analysis.

- **Insights Derived**:
  - Identified the senior-most employee by job title.
  - Determined countries with the most invoices.
  - Analyzed top revenue-generating cities and customers.
  - Found the most popular music genres by country.
  - Explored customer spending patterns on music and artists.

---

## SQL Queries and Outputs

### 1. Senior-most Employee
Query to find the senior-most employee based on job title, ordered by job level.

### 2. Countries with the Most Invoices
Query to rank countries by the number of invoices.

### 3. Top 3 Total Invoices
Query to list the top three highest invoice totals.

### 4. City with the Best Customers
Query to identify the city with the highest sum of invoice totals for a promotional event.

### 5. Best Customer
Query to determine the customer who spent the most money.

### 6. Rock Music Listeners
Query to list the email, first name, last name, and genre of all Rock music listeners, ordered by email.

### 7. Top Rock Artists
Query to invite the top 10 artists with the most Rock tracks in the dataset.

### 8. Longest Songs
Query to list tracks with song lengths exceeding the average, ordered by duration.

### 9. Customer Spending on Artists
Query to find how much each customer spent on specific artists.

### 10. Most Popular Genre by Country
Query to identify the most popular genre for each country based on purchases.

### 11. Top Customer by Country
Query to determine the customer who spent the most in each country, handling ties.

---

## Tools & Technologies Used

- **SQL**:
  - Analytical functions: `ROW_NUMBER()`, `WITH TIES`, and Common Table Expressions (CTEs).
  - Aggregate functions: `SUM()`, `COUNT()`, `AVG()`, and `MAX()`.
  - Joins: Inner joins for data integration.
  - Sorting and filtering with `ORDER BY` and `WHERE`.

---

## Insights & Findings

- **Top Customers**: Identified customers with the highest spending patterns.
- **Popular Genres**: Rock was one of the most purchased genres across multiple countries.
- **Regional Trends**: Certain cities showed higher revenue, indicating potential for promotional events.
- **Artist Performance**: Highlighted top-performing Rock artists by track count.

---

## How to Use

1. Clone this repository to your local machine.
2. Load the provided SQL scripts into your SQL environment (e.g., MySQL Workbench, SQL Server, or PostgreSQL).
3. Execute the queries against the provided music store database.
4. Analyze the outputs for business insights.

---

## Future Enhancements

- Visualize query outputs using Power BI or Tableau.
- Automate data ingestion and query execution.
- Develop dashboards for real-time insights.
- Enhance analysis by integrating additional datasets.

---

## Acknowledgments

This project is based on a simulated music store database and serves as a demonstration of SQL query skills and data analysis expertise.

---
