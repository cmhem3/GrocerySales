# GrocerySales (2023-11-28)
DataCamp SQL Certification - Practical Exam: Grocery Store Sales
![image](https://github.com/user-attachments/assets/f30cc661-943a-44de-b70b-c0a01adf7eb0)

FoodYum is a grocery store chain that is based in the United States.

Food Yum sells items such as produce, meat, dairy, baked goods, snacks, and other household food staples.

As food costs rise, FoodYum wants to make sure it keeps stocking products in all categories that cover a range of prices to ensure they have stock for a broad range of customers.

### Data
The data is available in the table products.  The dataset contains records of customers for their last full year of the loyalty program.
-  side note: as this is a certification from a DataCamp membership, the actual dataset is not available.  However, I've included the data dictionary, as well as my code and results.  DataCamp offers free trials where one can go straight to the SQL data analyst associtate certification if they wish to see this dataset.

**Column Name	with Criteria:**
-  product_id:	Nominal. The unique identifier of the product.  Missing values are not possible due to the database structure.
-  product_type:	Nominal. The product category type of the product, one of 5 values (Produce, Meat, Dairy, Bakery, Snacks).  Missing values should be replaced with “Unknown”.
-  brand:	Nominal. The brand of the product. One of 7 possible values.  Missing values should be replaced with “Unknown”.
- weight:	Continuous. The weight of the product in grams. This can be any positive value, rounded to 2 decimal places.  Missing values should be replaced with the overall median weight.
- price:	Continuous. The price the product is sold at, in US dollars. This can be any positive value, rounded to 2 decimal places.  Missing values should be replaced with the overall median price.
- average_units_sold:	Discrete. The average number of units sold each month. This can be any positive integer value.  Missing values should be replaced with 0.
- year_added:	Nominal. The year the product was first added to FoodYum stock.  Missing values should be replaced with 2022.
- stock_location:	Nominal. The location that stock originates. This can be one of four warehouse locations, A, B, C or D.  Missing values should be replaced with “Unknown”.

## Task 1
Last year (2022) there was a bug in the product system. For some products that were added in that year, the year_added value was not set in the data. As the year the product was added may have an impact on the price of the product, this is important information to have.
-  Write a query to determine how many products have the year_added value missing. Your output should be a single column, missing_year, with a single row giving the number of missing values.
```SQL
-- Write your query for task 1 in this cell
SELECT COUNT(*) AS missing_year
FROM products
WHERE year_added IS NULL;
```
![image](https://github.com/user-attachments/assets/2d8c80ad-d16c-460f-b8f4-c5f16bb9436b)

## Task 2
Given what you know about the year added data, you need to make sure all of the data is clean before you start your analysis. The table below shows what the data should look like.
- Write a query to ensure the product data matches the description provided. Do not update the original table.
```SQL
SELECT product_id, 
		product_type,
		REPLACE(brand, '-', 'Unknown') AS brand,
		ROUND(REPLACE(weight::TEXT, 'grams', '')::NUMERIC, 2) AS weight,
		ROUND(price::numeric, 2) AS price,
		average_units_sold,
		COALESCE(year_added, '2022') AS year_added,
		UPPER(stock_location) AS stock_location
FROM products;
```
![image](https://github.com/user-attachments/assets/9c043a14-9a9f-4036-b31a-6a619bffcf1c)

