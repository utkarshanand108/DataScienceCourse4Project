# DataScienceCourse4_Project
**Sales Performance Analysis of Walmart Stores Using Advanced SQL Techniques — DS PGC Course 4 Final Project**

---

## 📘 Project Overview
This project uses **advanced MySQL techniques** to analyze Walmart’s transaction data and uncover actionable business insights about **sales performance, customer behavior, product trends, and payment preferences**.

**Goal:** Identify growth opportunities and efficiency improvements by applying complex SQL queries on transactional data covering branches, product lines, payment modes, and customer types.

---

## 🧩 Task Summary
1. **Top Branch by Sales Growth Rate (6 Marks)** — Compare month-wise branch sales and rank by average growth rate.  
2. **Most Profitable Product Line per Branch (6 Marks)** — Compute profit margin = `gross_income – cost_of_goods_sold`.  
3. **Customer Segmentation (6 Marks)** — Classify customers as High / Medium / Low spenders by total purchase.  
4. **Anomaly Detection (6 Marks)** — Flag unusually high / low transactions vs average per product line.  
5. **Popular Payment Method by City (6 Marks)** — Find the top payment type for each city.  
6. **Monthly Sales by Gender (6 Marks)** — Compare male vs female revenue each month.  
7. **Best Product Line by Customer Type (6 Marks)** — Identify preferred categories for Members vs Normals.  
8. **Repeat Customers within 30 Days (6 Marks)** — Detect short-term repeat purchases.  
9. **Top 5 Customers by Sales Volume (6 Marks)** — Reward high-value buyers.  
10. **Sales Trends by Weekday (6 Marks)** — Discover the day with maximum sales.  
11. **Presentation & Video (20 Marks)** — PowerPoint + ≤ 5 min explanation video (link included).

---

## 🧰 SQL Techniques Used
```sql
-- Monthly branch growth using CTE & LEFT JOIN
WITH BranchSales AS (
  SELECT Branch, DATE_FORMAT(SaleDate,'%Y-%m') AS Month,
         SUM(Total) AS MonthlySales
  FROM walmart_sales
  GROUP BY Branch, Month
)
SELECT b1.Branch,
       ((b1.MonthlySales - COALESCE(b2.MonthlySales,0)) /
         COALESCE(b2.MonthlySales,1))*100 AS GrowthRate
FROM BranchSales b1
LEFT JOIN BranchSales b2
  ON b1.Branch=b2.Branch
 AND PERIOD_ADD(DATE_FORMAT(b2.Month,'%Y%m'),1)=DATE_FORMAT(b1.Month,'%Y%m');

-- Profitability by product line
SELECT Branch, ProductLine,
       SUM(GrossIncome - CostOfGoodsSold) AS Profit
FROM walmart_sales
GROUP BY Branch, ProductLine
ORDER BY Profit DESC;
```
Techniques demonstrated:
- `CTE`, `JOIN`, `RANK()`, `CASE`, `DATE_FORMAT()`, `COALESCE()`  
- Aggregation & window functions for growth and ranking  
- Conditional grouping for spending tiers and payment popularity

---

## 📊 Key Insights
- **Branch A** leads in average monthly sales growth.  
- **E-Wallet** dominates digital payments (2 of 3 cities).  
- **Female customers** slightly outspend males.  
- **Members → Food & Beverages **, **Normal → Electronic Accessories**.  
- **Fridays** yield peak sales; focus marketing then.  
- Detected anomalies in Fashion & Electronic Accessories.  
- No repeat customer IDs → future need for loyalty tracking.

---

## 🧮 Deliverables
- `DataScienceCourse4ProjectProblemStatement.pdf` — project brief  
- `DataScienceCourse4ProjectSolution.pdf` — full SQL analysis report with insights, visuals & recommendations  
- *(PPT + Video Drive link included in report)*

---

## 🧭 How to Review
1. Open `DataScienceCourse4ProjectSolution.pdf`.  
2. Execute SQL snippets sequentially in MySQL Workbench.  
3. Compare outputs and charts with report screenshots.  
4. Review final PowerPoint + video for summary presentation.

---

## 👤 Author
**Utkarsh Anand**  
DS PGC Course 4 — Final Project (Walmart Sales Performance Analysis)
