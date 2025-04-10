---
title: "[Project2] Walmart Analysis"
excerpt: "SQL+Tableau project"

categories:
  - 📊 Project
tags:
  - [Python,SQL,Tableau]

permalink: /📊 Project/SQL project2/

toc: true
toc_sticky: true

date: 2025-04-06
last_modified_at: 2025-04-06
---

## 🦥 Walmart business Analysis 

### Prime Process
1. Data Cleaning - Python
2. Data EDA - SQL 
3. Visualization -  Click [Tableau Dashboard]([https://example.com/](https://public.tableau.com/views/Project1WalmartAnalysis_Jiyun/1_SalesbyPeriod?:language=en-US&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link))


```

SELECT * 
FROM walmart.data
```
```

SELECT COUNT(*)
FROM walmart.data;

```


### how many different payment type we have ? 
```
SELECT payment_method, COUNT(*)
FROM walmart.data
GROUP BY payment_method
```


```
SELECT COUNT(DISTINCT branch) 
FROM walmart.data
```

```
SELECT MAX(quantity) 
FROM walmart.data
```

```
SELECT MIN(quantity) 
FROM walmart.data
```

# Walmart Business Problem
## 1. Analyze payment Methods and Sales 
### Q1. What are the differnet payment methods, and how many transactions 
 and items were sold with each method? 

```
SELECT payment_method, COUNT(*) AS number_of_Payments,SUM(quantity) AS number_of_Quantity_sold
FROM walmart.data
GROUP BY payment_method;
```

## Q2: Identify the highest-rated category in each branch
### Display the branch, category, and avg rating

```
WITH ranked AS (
    SELECT 
        branch,
        category,
        AVG(rating) AS avg_rating,
        ROW_NUMBER() OVER (PARTITION BY branch ORDER BY AVG(rating) DESC) AS rn
    FROM walmart.data
    GROUP BY branch, category
)
SELECT branch, category, avg_rating
FROM ranked
WHERE rn = 1;
```
```
SELECT branch, category, avg_rating
FROM (
    SELECT branch, category, AVG(rating) AS avg_rating
    FROM walmart.data
    GROUP BY branch, category
) t
WHERE avg_rating = (
    SELECT MAX(avg_rating)
    FROM (
         SELECT branch, category, AVG(rating) AS avg_rating
         FROM walmart.data
         GROUP BY branch, category
    ) s
    WHERE s.branch = t.branch
)
ORDER BY branch ASC;
```
### Q3: Identify the busiest day for each branch based on the number of transactions

```
SELECT t.branch, t.day_name, t.no_transactions
FROM (
    SELECT branch, DAYNAME(STR_TO_DATE(date, '%d/%m/%Y')) AS day_name, COUNT(*) AS no_transactions
    FROM walmart.data
    GROUP BY branch, day_name
) t
JOIN (
    SELECT branch, MAX(no_transactions) AS max_no_transactions
    FROM (
        SELECT branch, DAYNAME(STR_TO_DATE(date, '%d/%m/%Y')) AS day_name, COUNT(*) AS no_transactions
        FROM walmart.data
        GROUP BY branch, day_name
    ) s
    GROUP BY branch
) m ON t.branch = m.branch AND t.no_transactions = m.max_no_transactions
ORDER BY t.branch ;
```
### Q4: Calculate the total quantity of items sold per payment method
```
SELECT payment_method, SUM(quantity) AS Total_Quantity_of_Items
FROM walmart.data
GROUP BY payment_method
```
### Q5: Determine the average, minimum, and maximum rating of categories for each city

```
SELECT category, city, AVG(rating) as avg_rate , MAX(rating) as max_rate, MIN(rating) as min_rate
FROM walmart.data
GROUP BY city, category 
```

### Q6: Calculate the total profit for each category

```
SELECT category, FLOOR(SUM(total)) as total_profit
FROM walmart.data 
GROUP BY category
ORDER BY total_profit DESC;
```

### Q7: Determine the most common payment method for each branch

```
SELECT branch, payment_method, method_count
FROM (
    SELECT branch, payment_method, 
           COUNT(*) AS method_count,
           ROW_NUMBER() OVER (PARTITION BY branch ORDER BY COUNT(*) DESC) AS rn
    FROM walmart.data
    GROUP BY branch, payment_method
) ranked
WHERE rn = 1
ORDER BY branch;
```

### Q8: Categorize sales into Morning, Afternoon, and Evening shifts

```
SELECT branch, COUNT(*) AS num_invoices,
       CASE 
           WHEN TIME(time) BETWEEN '06:00:00' AND '11:59:59' THEN 'Morning'
           WHEN TIME(time) BETWEEN '12:00:00' AND '17:59:59' THEN 'Afternoon'
           WHEN TIME(time) BETWEEN '18:00:00' AND '21:59:59' THEN 'Evening'
           ELSE 'Other'
       END AS shift
FROM walmart. data
GROUP BY branch, shift
ORDER BY branch, num_invoices DESC;
```

```
SELECT
    branch,
    CASE 
        WHEN HOUR(TIME(time)) < 12 THEN 'Morning'
        WHEN HOUR(TIME(time)) BETWEEN 12 AND 17 THEN 'Afternoon'
        ELSE 'Evening'
    END AS shift,
    COUNT(*) AS num_invoices
FROM walmart. data
GROUP BY branch, shift
ORDER BY branch, num_invoices DESC;
```

-- advanced : find which shift has more total profit? 
 
### Q9: Identify the 5 branches with the highest revenue decrease ratio from last year to current year (e.g., 2022 to 2023)

```
SELECT branch, YEAR(date) as Year, SUM(total) as Yearly_revenue 
FROM walmart. data
GROUP BY branch, YEAR(date);
SELECT 
    branch,
    SUM(CASE WHEN YEAR(date) = 2022 THEN total ELSE 0 END) AS revenue_2022,
    SUM(CASE WHEN YEAR(date) = 2023 THEN total ELSE 0 END) AS revenue_2023
FROM walmart.data
GROUP BY branch;
```

```

WITH revenue_2022 AS (
    SELECT 
        branch,
        SUM(total) AS revenue
    FROM walmart. data
    WHERE YEAR(STR_TO_DATE(date, '%d/%m/%Y')) = 2022
    GROUP BY branch
),
revenue_2023 AS (
    SELECT 
        branch,
        SUM(total) AS revenue
    FROM walmart. data
    WHERE YEAR(STR_TO_DATE(date, '%d/%m/%Y')) = 2023
    GROUP BY branch
)
SELECT 
    r2022.branch,
    r2022.revenue AS last_year_revenue,
    r2023.revenue AS current_year_revenue,
    ROUND(((r2022.revenue - r2023.revenue) / r2022.revenue) * 100, 2) AS revenue_decrease_ratio
FROM revenue_2022 AS r2022
JOIN revenue_2023 AS r2023 ON r2022.branch = r2023.branch
WHERE r2022.revenue > r2023.revenue
ORDER BY revenue_decrease_ratio DESC
LIMIT 5;
```

```
WITH revenue_2022 AS (
    SELECT 
        branch,
        SUM(total) AS revenue
    FROM walmart.data
    WHERE YEAR(STR_TO_DATE(date, '%d/%m/%Y')) = 2022
    GROUP BY branch
),
revenue_2023 AS (
    SELECT 
        branch,
        SUM(total) AS revenue
    FROM walmart.data
    WHERE YEAR(STR_TO_DATE(date, '%d/%m/%Y')) = 2023
    GROUP BY branch
)
SELECT 
    r2022.branch,
    r2022.revenue AS last_year_revenue,
    COALESCE(r2023.revenue, 0) AS current_year_revenue,
    ROUND(((r2022.revenue - COALESCE(r2023.revenue, 0)) / r2022.revenue) * 100, 2) AS revenue_decrease_ratio
FROM revenue_2022 AS r2022
LEFT JOIN revenue_2023 AS r2023 ON r2022.branch = r2023.branch
ORDER BY revenue_decrease_ratio DESC
LIMIT 5;

```

```

SELECT 
    branch,
    SUM(CASE WHEN YEAR(STR_TO_DATE(date, '%d/%m/%Y')) = 2022 THEN total ELSE 0 END) AS last_year_revenue,
    SUM(CASE WHEN YEAR(STR_TO_DATE(date, '%d/%m/%Y')) = 2023 THEN total ELSE 0 END) AS current_year_revenue,
    ROUND(
        (
            SUM(CASE WHEN YEAR(STR_TO_DATE(date, '%d/%m/%Y')) = 2022 THEN total ELSE 0 END)
            - 
            SUM(CASE WHEN YEAR(STR_TO_DATE(date, '%d/%m/%Y')) = 2023 THEN total ELSE 0 END)
        ) 
        / 
        NULLIF(SUM(CASE WHEN YEAR(STR_TO_DATE(date, '%d/%m/%Y')) = 2022 THEN total ELSE 0 END), 0)
        * 100, 
    2) AS revenue_decrease_ratio
FROM walmart.data
GROUP BY branch
ORDER BY revenue_decrease_ratio DESC
LIMIT 5;
```
