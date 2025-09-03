# Netflix Movies and TV Shows Data Analysis using SQL

![](https://github.com/tktejas117/-BlinkIt-Grocery-Dataset/blob/main/image.jpg)

## Overview
This project involves a comprehensive analysis of Blinkit’s grocery sales dataset using SQL.The goal is to extract valuable insights and answer various business questions based on sales, items, outlets, and customer ratings.The following README provides the project’s objectives, business problems, SQL solutions, findings, and conclusions.
## Objectives

-- Analyze overall sales performance across items and outlets.
-- Identify top-performing categories, brands, and outlet types.
-- Compare sales contribution by fat content, outlet size, and outlet location.
-- Measure customer satisfaction through ratings and visibility.
-- Categorize items based on product descriptions.

## Dataset

The data for this project is sourced from the Kaggle dataset:

- **Dataset Link:** [Grocery Dataset](https://www.kaggle.com/datasets/arunkumaroraon/blinkit-grocery-dataset)

## Schema

```sql
DROP TABLE IF EXISTS netflix;
CREATE TABLE netflix
(
    DROP TABLE IF EXISTS blinkit_data;
CREATE TABLE blinkit_data
(
    Item_Identifier       VARCHAR(50),
    Item_Weight           DECIMAL(10,2),
    Item_Fat_Content      VARCHAR(50),
    Item_Visibility       DECIMAL(10,4),
    Item_Type             VARCHAR(100),
    Outlet_Identifier     VARCHAR(50),
    Outlet_Establishment_Year INT,
    Outlet_Size           VARCHAR(20),
    Outlet_Location_Type  VARCHAR(50),
    Outlet_Type           VARCHAR(50),
    Total_Sales           DECIMAL(10,2),
    Rating                DECIMAL(3,1),
);

);
```

## Business Problems and Solutions

### 1. Count the Number of Movies vs TV Shows

```sql
SELECT CAST(SUM(Total_Sales) / 1000000.0 AS DECIMAL(10,2)) AS Total_Sales_Million
FROM blinkit_data;
```

**Objective:** Calculate overall revenue generated from all items sold.

### 2. Find the Most Common Rating for Movies and TV Shows

```sql
SELECT CAST(AVG(Total_Sales) AS INT) AS Avg_Sales
FROM blinkit_data;

```

**Objective:** Find the average revenue per sale.

### 3. List All Movies Released in a Specific Year (e.g., 2020)

```sql
SELECT COUNT(*) AS No_of_Items
FROM blinkit_data;

```

**Objective:** Count the total number of items sold.

### 4. Find the Top 5 Countries with the Most Content on Netflix

```sql
SELECT CAST(AVG(Rating) AS DECIMAL(10,1)) AS Avg_Rating
FROM blinkit_data;

```

**Objective:** Find the average customer rating across all items.

### 5. Identify the Longest Movie

```sql
SELECT Item_Fat_Content, CAST(SUM(Total_Sales) AS DECIMAL(10,2)) AS Total_Sales
FROM blinkit_data
GROUP BY Item_Fat_Content;

```

**Objective:** Analyze sales distribution between Low Fat and Regular items.

### 6. Find Content Added in the Last 5 Years

```sql
SELECT Item_Type, CAST(SUM(Total_Sales) AS DECIMAL(10,2)) AS Total_Sales
FROM blinkit_data
GROUP BY Item_Type
ORDER BY Total_Sales DESC;

```

**Objective:** Identify which product categories contribute the most to sales.

### 7. Find All Movies/TV Shows by Director 'Rajiv Chilaka'

```sql
SELECT Outlet_Location_Type, 
       ISNULL([Low Fat], 0) AS Low_Fat, 
       ISNULL([Regular], 0) AS Regular
FROM (
    SELECT Outlet_Location_Type, Item_Fat_Content, 
           CAST(SUM(Total_Sales) AS DECIMAL(10,2)) AS Total_Sales
    FROM blinkit_data
    GROUP BY Outlet_Location_Type, Item_Fat_Content
) AS SourceTable
PIVOT (
    SUM(Total_Sales) 
    FOR Item_Fat_Content IN ([Low Fat], [Regular])
) AS PivotTable
ORDER BY Outlet_Location_Type;


```

**Objective:** Compare fat content sales performance across different outlet locations.

### 8. List All TV Shows with More Than 5 Seasons

```sql
SELECT Outlet_Establishment_Year, CAST(SUM(Total_Sales) AS DECIMAL(10,2)) AS Total_Sales
FROM blinkit_data
GROUP BY Outlet_Establishment_Year
ORDER BY Outlet_Establishment_Year;

```

**Objective:** Evaluate how the age or type of outlet influences sales.

### 9. Count the Number of Content Items in Each Genre

```sql
SELECT Outlet_Size, 
       CAST(SUM(Total_Sales) AS DECIMAL(10,2)) AS Total_Sales,
       CAST((SUM(Total_Sales) * 100.0 / SUM(SUM(Total_Sales)) OVER()) AS DECIMAL(10,2)) AS Sales_Percentage
FROM blinkit_data
GROUP BY Outlet_Size
ORDER BY Total_Sales DESC;

```

**Objective:** Find the contribution of Small, Medium, and Large outlets to overall sales.

### 10.Find each year and the average numbers of content release in India on netflix. 
return top 5 year with highest avg content release!

```sql
SELECT Outlet_Location_Type, CAST(SUM(Total_Sales) AS DECIMAL(10,2)) AS Total_Sales
FROM blinkit_data
GROUP BY Outlet_Location_Type
ORDER BY Total_Sales DESC;

```

**Objective:** Measure sales distribution across different outlet locations.

### 11. List All Movies that are Documentaries

```sql
SELECT Outlet_Type, 
       CAST(SUM(Total_Sales) AS DECIMAL(10,2)) AS Total_Sales,
       CAST(AVG(Total_Sales) AS DECIMAL(10,0)) AS Avg_Sales,
       COUNT(*) AS No_Of_Items,
       CAST(AVG(Rating) AS DECIMAL(10,2)) AS Avg_Rating,
       CAST(AVG(Item_Visibility) AS DECIMAL(10,2)) AS Item_Visibility
FROM blinkit_data
GROUP BY Outlet_Type
ORDER BY Total_Sales DESC;

```

**Objective:** Compare all KPIs (sales, average sales, item counts, ratings, and visibility) by outlet type.



## Findings and Conclusion

- **Sales performace:** Larger outlets contribute the highest percentage of sales.
- **Customer Preferance:** Insights into the most common ratings provide an understanding of the content's target audience.
- **Category Insights:** The top countries and the average content releases by India highlight regional content distribution.
- **Outlet Insights:** Categorizing content based on specific keywords helps in understanding the nature of content available on Netflix.
- **Cutomer Feedback:** Categorizing content based on specific keywords helps in understanding the nature of content available on Netflix.

This analysis provides a comprehensive view of Netflix's content and can help inform content strategy and decision-making.



## Author - Zero Analyst

This project is part of my portfolio, showcasing the SQL skills essential for data analyst roles. If you have any questions, feedback, or would like to collaborate, feel free to get in touch!

### Stay Updated and Join the Community

For more content on SQL, data analysis, and other data-related topics, make sure to follow me on social media and join our community:

- **YouTube**: [Subscribe to my channel for tutorials and insights](https://www.youtube.com/@zero_analyst)
- **Instagram**: [Follow me for daily tips and updates](https://www.instagram.com/zero_analyst/)
- **LinkedIn**: [Connect with me professionally](https://www.linkedin.com/in/najirr)
- **Discord**: [Join our community to learn and grow together](https://discord.gg/36h5f2Z5PK)

Thank you for your support, and I look forward to connecting with you!
