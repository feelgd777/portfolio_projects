# Walmart Sales Data Analysis
This project is designed to explore the Walmart Sales data to understand top performing branches and products, sales trends for different produxt lines, and customer behaviour. 

## Purpose:
To gain insight into the sales data of Walmart to understand the different factors that affect sales of the different branches.

## Data:
This dataset contains sales transactions from a three different branches of Walmart located in Mandalay, Yangon and Naypyitaw. The data contains 17 columns and 1000 rows:

| Column                  | Description                             | Data Type      |
| :---------------------- | :-------------------------------------- | :------------- |
| invoice_id              | Invoice of the sales made               | VARCHAR(30)    |
| branch                  | Branch at which sales were made         | VARCHAR(5)     |
| city                    | The location of the branch              | VARCHAR(30)    |
| customer_type           | The type of the customer                | VARCHAR(30)    |
| gender                  | Gender of the customer making purchase  | VARCHAR(10)    |
| product_line            | Product line of the product solf        | VARCHAR(100)   |
| unit_price              | The price of each product               | DECIMAL(10, 2) |
| quantity                | The amount of the product sold          | INT            |
| VAT                     | The amount of tax on the purchase       | FLOAT(6, 4)    |
| total                   | The total cost of the purchase          | DECIMAL(10, 2) |
| date                    | The date on which the purchase was made | DATE           |
| time                    | The time at which the purchase was made | TIMESTAMP      |
| payment                 | The total amount paid                   | DECIMAL(10, 2) |
| cogs                    | Cost Of Goods sold                      | DECIMAL(10, 2) |
| gross_margin_percentage | Gross margin percentage                 | FLOAT(11, 9)   |
| gross_income            | Gross Income                            | DECIMAL(10, 2) |
| rating                  | Rating                                  | FLOAT(3, 1)    |


    CREATE TABLE IF NOT EXISTS sales (
    	invoice_id VARCHAR(30) NOT NULL PRIMARY KEY,
    	branch VARCHAR(5) NOT NULL,
    	city VARCHAR(30) NOT NULL,
    	customer_type VARCHAR(30) NOT NULL,
    	gender VARCHAR(10) NOT NULL,
    	product_line VARCHAR(100) NOT NULL,
    	unit_price DECIMAL(10 , 2 ) NOT NULL,
    	quantity INT NOT NULL,
    	VAT FLOAT(6 , 4 ) NOT NULL,
    	total DECIMAL(12 , 4 ) NOT NULL,
    	date DATETIME NOT NULL,
    	time TIME NOT NULL,
    	payment VARCHAR(15) NOT NULL,
    	cogs DECIMAL(10 , 2 ) NOT NULL,
    	gross_margin_pct FLOAT(11 , 9 ),
    	gross_income DECIMAL(12 , 4 ) NOT NULL,
    	rating FLOAT(2 , 1 ) NOT NULL
	);


	ALTER TABLE sales  
	DROP COLUMN payment_method;  

	ALTER TABLE sales  
	MODIFY COLUMN payment VARCHAR(20);  

	ALTER TABLE sales  
	MODIFY COLUMN rating FLOAT(3, 1);  


------------------------------------------------------------------------------
### Feature Engineering

#### time_of_day

	ALTER TABLE sales     
	ADD COLUMN time_of_day VARCHAR(20);  

	UPDATE sales   
	SET 
 		time_of_day = (CASE  
 			WHEN `time` BETWEEN "00:00:00" AND "12:00:00" THEN "Morning"  
			WHEN `time` BETWEEN "12:01:00" AND "16:00:00" THEN "Afternoon"  
  			ELSE "Evening"  
  		END);  
  
#### day_name

	ALTER TABLE sales     
	ADD COLUMN day_name VARCHAR(10);    

	UPDATE sales     
	SET 
 		day_name = DAYNAME(date);    

#### month_name

	ALTER TABLE sales   
	ADD COLUMN month_name VARCHAR(10);  

	UPDATE sales   
	SET 
  		month_name = MONTHNAME(date);  


------------------------------------------------------------------------------
### Generic 

#### How many unique cities does the data have?

	SELECT DISTINCT 
 		city  
	FROM 
 		sales;  
 
#### In which city is each branch?

	SELECT DISTINCT 
 		city, branch  
	FROM 
 		sales;  


------------------------------------------------------------------------------
### Product

#### How many unique product lines does the data have?

	SELECT COUNT(DISTINCT product_line)  
	FROM sales;  
    
#### What is the most comon payment method?

	SELECT   
		payment,   
		COUNT(payment) c  
	FROM 
 		sales  
	GROUP BY payment  
	ORDER BY c DESC;  
  
#### What is the top selling product line?

	SELECT   
		product_line,   
		COUNT(product_line) cnt  
	FROM 
 		sales  
	GROUP BY product_line  
	ORDER BY cnt DESC;   


#### What is the total revenue by month?

	SELECT   
		month_name month,   
		SUM(total) Total_revenue  
	FROM 
 		sales  
	GROUP BY month  
	ORDER BY Total_revenue DESC;  

#### What month had the largest cost of goods sold?

	SELECT   
		month_name month,  
		SUM(cogs) cogs  
	FROM 
		sales  
	GROUP BY month  
	ORDER BY cogs DESC;  

#### What product line had the largest revenue?

	SELECT  
		product_line,  
		SUM(total) Total_revenue  
	FROM 
 		sales  
	GROUP BY product_line  
	ORDER BY Total_revenue DESC;  

#### What is the city with the largest revenue?

	SELECT    
		branch,  
		city,  
		SUM(total) Total_revenue  
	FROM 
 		sales  
	GROUP BY city, branch  
	ORDER BY Total_revenue DESC;  

#### What product linke had the largest VAT(tax)?ALTER

	SELECT   
		product_line,  
		AVG(VAT) avg_tax  
	FROM 
		sales  
	GROUP BY product_line  
	ORDER BY avg_tax DESC;  

#### Which branch sold more products than average product sold?

	SELECT   
		branch,   
		SUM(quantity) qty  
	FROM 
		sales  
	GROUP BY branch  
	HAVING SUM(quantity) > (SELECT AVG(quantity) FROM sales);  

#### What is the most common product line by gender?

	SELECT   
		gender,   
		product_line,  
		COUNT(gender) total_cnt  
	FROM 
		sales  
	GROUP BY gender, product_line  
	ORDER BY total_cnt DESC;  

#### What is the average rating of each product line?

	SELECT  
		product_line,   
		ROUND(AVG(rating), 2) avg_rating  
	FROM 
		sales  
	GROUP BY product_line   
	ORDER BY avg_rating DESC;  


------------------------------------------------------------------------------
### Sales

#### What day and time are customers more likely to buy?

	SELECT  
		day_name,   
		time_of_day,   
		COUNT(*) total_sales   
	FROM 
		sales  
	GROUP BY day_name, time_of_day    
	ORDER BY total_sales DESC;  
  
#### Which city has the largest Value Added Tax?

	SELECT   
		city,  
		AVG(VAT) avg_tax  
	FROM 
		sales  
	GROUP BY city  
	ORDER BY avg_tax DESC;  


------------------------------------------------------------------------------
### Customer

#### How many unique payment methods does the data have?

	SELECT DISTINCT payment   
	FROM sales;  

#### Which customer type buys the most?

	SELECT   
		customer_type,   
		COUNT(*) cstm_count  
	FROM 
		sales  
	GROUP BY customer_type  
	ORDER BY cstm_count DESC;  

#### What gender buys the most?

	SELECT   
		gender,   
		COUNT(*) cnt  
	FROM 
		sales  
	GROUP BY gender    
	ORDER BY cnt DESC;  
  
#### Which time of the day do customers give hightest rating?

	SELECT   
		time_of_day,   
		AVG(rating) avg_rating  
	FROM 
		sales  
	GROUP BY time_of_day  
	ORDER BY avg_rating DESC;  

#### Whcih day of the week has the hightest ratings?

	SELECT   
		day_name,   
		AVG(rating) avg_rating  
	FROM 
 		sales  
	GROUP BY day_name  
	ORDER BY avg_rating DESC;  



