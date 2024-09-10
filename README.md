# Fast Food Marketing Campaign Analysis With SQL

In this case study, three different promotions for a new item at a fast food resturant are tested over the course of four weeks to see which has the greatest effect on sales. This dataset includes MarketID, MarketSize, LocationID, AgeOfStore, Promotion, week, and SalesInThousands.

Source: https://www.kaggle.com/datasets/chebotinaa/fast-food-marketing-campaign-ab-test

### 1. How many total locations were used in this study? 

````sql
SELECT
  COUNT(DISTINCT LocationID) AS Number_of_Locations
FROM `data-analytics-sql-424800.marketing_campaign.marketing-campaign` 
````

137 total locations were used in this case study.

````sql
SELECT 
  Promotion, COUNT(DISTINCT LocationID) AS Number_of_Locations
FROM `data-analytics-sql-424800.marketing_campaign.marketing-campaign` 
GROUP BY(Promotion)
````

43 locations are testing Promo 1, 47 locations are testing Promo 2, and 47 locations are testing Promo 3. 

### 2. What is the total amount of sales for each promotion? 

````sql
SELECT Promotion, SUM(SalesInThousands) AS TotalSales
FROM `data-analytics-sql-424800.marketing_campaign.marketing-campaign` 
GROUP BY (Promotion)
````

Results show that Promo 3 had the highest total sales overall, followed by Promo 1. However, Promo 1 was tested at a slightly less amount of locations. Let's see if Promo 3 really is the best choice to use for this new campaign. 

### 3. How did MarketID effect promotion performance? 

````sql
SELECT
  MarketID, Promotion, NumOfLocations, TotalSales, TotalSales/NumOfLocations AS SalesPerLocation
FROM 
(   SELECT
      MarketID, Promotion, COUNT(LocationID) AS NumOfLocations, SUM(SalesInThousands) AS TotalSales
    FROM `data-analytics-sql-424800.marketing_campaign.marketing-campaign` 
    GROUP BY MarketID, Promotion
    ORDER BY MarketID)
````

This query shows the average sales per location of each promotion within each MarketID. Of the ten different MarektID's, Promo 1 performed the best in every one. 

### 4. How did Market Size effect promotion performance? 

````sql
SELECT
  MarketSize, Promotion, NumOfLocations, TotalSales, TotalSales/NumOfLocations AS SalesPerLocation
FROM 
(   SELECT
      MarketSize, Promotion, COUNT(LocationID) AS NumOfLocations, SUM(SalesInThousands) AS TotalSales
    FROM `data-analytics-sql-424800.marketing_campaign.marketing-campaign` 
    GROUP BY MarketSize, Promotion
    ORDER BY MarketSize)
````

This shows that Promo 3 performed slightly better than Promo 1 within the large market size. Promo 1 performed the best within both the medium and small market sizes. The majority of locations in this study are medium sized. 

### 5. How did Age of Store effect promotion performance? 

````sql
SELECT
  AgeOfStore, Promotion, NumOfLocations, TotalSales, TotalSales/NumOfLocations AS SalesPerLocation
FROM 
(   SELECT
      AgeOfStore, Promotion, COUNT(LocationID) AS NumOfLocations, SUM(SalesInThousands) AS TotalSales
    FROM `data-analytics-sql-424800.marketing_campaign.marketing-campaign` 
    GROUP BY AgeOfStore, Promotion
    ORDER BY AgeOfStore)
````

This shows that many locations used in this study are 1 year old, and Promo 1 performed the best. Promo 1 also performed the best for mostly every other age of store. 

### 6. What is the amount of sales broken down by week for each promotion?

````sql
SELECT
  week, Promotion, NumOfLocations, TotalSales, TotalSales/NumOfLocations AS SalesPerLocation
FROM 
(   SELECT
      week, Promotion, COUNT(LocationID) AS NumOfLocations, SUM(SalesInThousands) AS TotalSales
    FROM `data-analytics-sql-424800.marketing_campaign.marketing-campaign` 
    GROUP BY week, Promotion
    ORDER BY Promotion)
````

Total sales were consistent week by week for each promotion. 

### 7. Which of the three Promotions should be used to market this new fast food item? 

Just by looking at total sales, Promo 3 had the most. But, when analyzing the data a little deeper, results show that Promo 1 performs the best across MarketID, Market Size, and Age of Store. Therefore, Promo 1 is the correct choice for this new marketing campaign. 





