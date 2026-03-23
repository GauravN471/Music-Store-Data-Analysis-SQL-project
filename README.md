# 🎵 Music Store Data Analysis — SQL Project

![PostgreSQL](https://img.shields.io/badge/PostgreSQL-Advanced-4169E1?style=for-the-badge&logo=postgresql&logoColor=white)
![SQL](https://img.shields.io/badge/SQL-CTEs%20%7C%20Joins%20%7C%20Window%20Functions-orange?style=for-the-badge)
![Domain](https://img.shields.io/badge/Domain-Retail_%26_Entertainment-purple?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge)

> **"Queried a digital music store's relational database across 11 business questions — from employee hierarchy and invoice analysis to genre popularity by country and top customer spend per region."**

---

## 🎯 Executive Summary

A digital music store needed to understand its revenue distribution, customer spending patterns, top-performing genres by market, and which cities represented the highest commercial opportunity. I analysed the full relational database using SQL — progressing from simple aggregations to advanced CTEs and window functions — delivering 11 structured business answers across 3 difficulty levels.

---

## 🛠 Tech Stack

| Tool | Purpose |
|---|---|
| **PostgreSQL** | Primary query engine |
| **CTEs** | Multi-step logic for complex questions |
| **Window Functions** | ROW_NUMBER(), WITH TIES for ranking |
| **Aggregate Functions** | SUM(), COUNT(), AVG(), MAX() |
| **JOINs** | Multi-table joins across invoice, customer, genre, artist tables |
| **Subqueries** | Nested filtering for threshold-based questions |

---

## 🗄 Database Schema
```
employee          → employee_id, last_name, first_name, title, levels
customer          → customer_id, first_name, last_name, email, country, city
invoice           → invoice_id, customer_id, total, billing_country, billing_city
invoice_line      → invoice_line_id, invoice_id, track_id, unit_price, quantity
track             → track_id, name, album_id, media_type_id, genre_id, milliseconds
genre             → genre_id, name
artist            → artist_id, name
album             → album_id, title, artist_id
```

---

## ❓ 11 Business Questions — 3 Levels

**🟢 Easy**
| # | Question | Technique |
|---|---|---|
| 1 | Senior-most employee by job level? | ORDER BY + LIMIT |
| 2 | Countries with most invoices? | GROUP BY + COUNT |
| 3 | Top 3 invoice totals? | ORDER BY + LIMIT |
| 4 | City with highest invoice sum (for promo event)? | GROUP BY + SUM |
| 5 | Best customer by total spend? | JOIN + SUM + ORDER BY |

**🟡 Intermediate**
| # | Question | Technique |
|---|---|---|
| 6 | All Rock music listeners — email, name, genre? | JOIN + WHERE + ORDER BY |
| 7 | Top 10 Rock artists by track count? | JOIN + COUNT + GROUP BY |
| 8 | Tracks longer than average song length? | Subquery + AVG |

**🔴 Advanced**
| # | Question | Technique |
|---|---|---|
| 9 | How much did each customer spend on each artist? | Multi-table JOIN + SUM |
| 10 | Most popular genre per country? | CTE + ROW_NUMBER() |
| 11 | Top spending customer per country (handling ties)? | CTE + WITH TIES |

---

## 💻 Sample SQL — See the Code in Action

**Q10: Most popular genre per country (Advanced — CTE + Window Function)**
```sql
WITH popular_genre AS (
    SELECT
        c.country,
        g.name AS genre,
        COUNT(il.quantity) AS purchases,
        ROW_NUMBER() OVER (
            PARTITION BY c.country
            ORDER BY COUNT(il.quantity) DESC
        ) AS row_num
    FROM invoice_line il
    JOIN invoice i    ON il.invoice_id = i.invoice_id
    JOIN customer c   ON i.customer_id = c.customer_id
    JOIN track t      ON il.track_id = t.track_id
    JOIN genre g      ON t.genre_id = g.genre_id
    GROUP BY c.country, g.name
)
SELECT country, genre, purchases
FROM popular_genre
WHERE row_num = 1
ORDER BY country;
```

**Q4: Best city for a promotional music event**
```sql
SELECT
    billing_city,
    SUM(total) AS invoice_total
FROM invoice
GROUP BY billing_city
ORDER BY invoice_total DESC
LIMIT 1;
```

---

## 💡 Business Insights — The "So What?"

- **Identified Rock as the dominant genre across multiple countries** — with the top 10 Rock artists each contributing 40+ tracks to the catalogue, making Rock-focused promotions the highest-ROI marketing investment across most markets.

- **Found significant spend concentration in a small number of cities** — the top city by invoice total generated disproportionately higher revenue than the average, making it the clear first choice for any live promotional event or partnership investment.

- **Discovered that top-spending customers per country vary significantly in absolute value** — some country-level "top customers" represent major account relationships while others represent thin markets, informing where a VIP customer programme would have the most impact.

---

## 📋 Business Recommendations

1. **Promotional Event Location** — Host the music festival in the highest invoice-sum city — the data clearly identifies this as the market with the deepest customer spend concentration.
2. **Rock Genre Investment** — Prioritise expanding the Rock catalogue and Rock artist partnerships — it is the most purchased genre across the widest range of countries.
3. **VIP Customer Programme** — The top-spending customers per country (Q11) form a ready-made VIP tier — targeted loyalty offers to these accounts would improve retention of the highest-value segment.
4. **Market Expansion Signal** — Countries with high invoice counts but lower per-invoice totals represent volume markets with upsell potential — bundle and upgrade offers could increase average order value.

---

## 🗂 Repository Structure
```
Music-Store-Data-Analysis-SQL-project/
├── README.md
├── SQl query          ← All 11 SQL queries
└── music_database.sql ← Full database schema and seed data
```

---

## 👤 Author

**Gaurav Nikam** — Data Analyst | SQL · Power BI · Excel · Bloomberg Terminal
📧 gauravnikam471@gmail.com
🔗 [LinkedIn](https://www.linkedin.com/in/-471-gaurav-nikam)
