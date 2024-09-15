# Fast Food Marketing Campaign Analysis With SQL

In this case study, three different promotions for a new item at a fast food restaurant are tested over the course of four weeks to see which has the greatest effect on sales. This dataset includes MarketID, MarketSize, LocationID, AgeOfStore, Promotion, Week, and SalesInThousands.

Source: https://www.kaggle.com/datasets/chebotinaa/fast-food-marketing-campaign-ab-test

### 1. How many total locations were used in this study? 

````sql
SELECT
  COUNT(DISTINCT LocationID) AS Number_of_Locations
FROM `data-analytics-sql-424800.marketing_campaign.marketing-campaign`
````

<img width="242" alt="Screenshot 2024-09-15 at 5 04 52 PM 2" src="https://github.com/user-attachments/assets/9819f177-29fc-4adc-a503-7b0721899058">

137 total locations were used in this case study.

````sql
SELECT 
  Promotion, COUNT(DISTINCT LocationID) AS Number_of_Locations
FROM `data-analytics-sql-424800.marketing_campaign.marketing-campaign` 
GROUP BY(Promotion)
````

<img width="360" alt="Screenshot 2024-09-15 at 6 00 03 PM" src="https://github.com/user-attachments/assets/b8bb1c3d-1bc0-47c2-aa5d-4309de013cc2">

43 locations are testing Promo 1, 47 locations are testing Promo 2, and 47 locations are testing Promo 3. 

### 2. What is the total amount of sales for each promotion? 

````sql
SELECT Promotion, SUM(SalesInThousands) AS TotalSales
FROM `data-analytics-sql-424800.marketing_campaign.marketing-campaign` 
GROUP BY (Promotion)
````

<img width="300" alt="Screenshot 2024-09-15 at 6 01 38 PM" src="https://github.com/user-attachments/assets/1491437d-3abb-4058-836d-65c8f697130e">

Results show that Promo 3 had the highest total sales overall, followed by Promo 1. However, Promo 1 was tested at a slightly less amount of locations. Let's see if Promo 3 really is the best choice to use for this new campaign. 

### 3. How did MarketID affect promotion performance? 

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

<img width="685" alt="Screenshot 2024-09-15 at 6 07 23 PM" src="https://github.com/user-attachments/assets/16fafef8-9fb9-4eb6-a0d4-b8131d06cfcb">

This query shows the average sales per location of each promotion within each MarketID. The image shows the first three MarketID's. Of the ten MarektID's, Promo 1 performed the best in every one. 

### 4. How did Market Size affect promotion performance? 

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

<img width="762" alt="Screenshot 2024-09-15 at 6 10 28 PM" src="https://github.com/user-attachments/assets/add251fb-cc44-4ce7-8671-3cce471d8832">

This shows that Promo 3 performed slightly better than Promo 1 within the large market size. Promo 1 performed the best within both the medium and small market sizes. The majority of locations in this study are medium sized. 

### 5. How did Age of Store affect promotion performance? 

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

<img width="682" alt="Screenshot 2024-09-15 at 6 13 32 PM" src="https://github.com/user-attachments/assets/5a5e6b24-9126-4644-b7e2-ec49cabd7c15">

The image shows stores that are 1-4 years old. The oldest store is 23 years. This query shows that 1 year old stores have the highest amount of locations, and Promo 1 performed the best. Promo 1 also performed the best for mostly every other age of store. 

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

<img width="686" alt="Screenshot 2024-09-15 at 6 18 00 PM" src="https://github.com/user-attachments/assets/f4fe00cd-dd1f-45f5-bf98-643628b972f8">

Total sales were consistent week by week for each promotion. 

### 7. Which of the three promotions should be used to market this new fast food item? 

When looking at overall total sales, Promo 3 has the highest. However, when analyzing the data a little deeper, results show that Promo 1 performs the best across MarketID, Market Size, and Age of Store. Therefore, Promo 1 is the correct choice for this new marketing campaign. 





