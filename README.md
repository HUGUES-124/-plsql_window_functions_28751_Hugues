# ID : 28751
# Names : MUGISHA NKURAYIJA HUGUES
# KMEI SHOP LTD

BUSINESS PROBLEM : The business sells different products like milk products,water and processed juice. It has to make database to keep different tables that it will need like the stock,products the orders made by Customers and the Suppliers to supply their goods each table with its attributes. So this database will help the shop to keep control of the transactions. 

# ERD DIAGRAM FOR Kmei shop ltd
![ERD_DIAGRAM_FOR_KMEI_SHOP](ERD%20Diagram.png)

# Joins

 /*inner join (rows match in all tables) A business wants to know how many customers made the orders and how and the product name of their order. The customers who did not make an order will not be seen*/
 ![innerjoin](https://github.com/HUGUES-124/-plsql_window_functions_28751_Hugues/blob/main/inner%20join.png)
select c.customer_id,c.customer_names,p.product_id,p.product_name from customers c inner join orders o on c.order_id=o.order_id inner join products p on p.product_id= o.product_id;

 /*left_join(rows from the customers table even if they don't match with the ones in the other tables )In left join a business wanted to know all customers including those who didn’t make an order. As you can see Yuhi didn’t make an order yet he is on the list but the product is null*/ 
 
 ![left join](https://github.com/HUGUES-124/-plsql_window_functions_28751_Hugues/blob/main/left%20join.png )

select c.customer_id,c.customer_names,p.product_id,p.product_name from customers c left join orders o on c.order_id=o.order_id left join products p on p.product_id= o.product_id;

/*Right_join( rows from product even if no orders were made)Here a business wanted to show all the products including also those that we not ordered . Here we have all the products that the shop has including those not ordered.*/
![Right_join]( https://github.com/HUGUES-124/-plsql_window_functions_28751_Hugues/blob/main/right%20join.png )

select p.product_id,p.product_name,o.order_id,o.quantity from orders o right join products p on o.product_id=p.product_id;

--full_join
/*  Using full join we can show the data of two tables 
or more even if some rows are not full because there is no relation between all the columns (columns from one table and another*/![Full join](https://github.com/HUGUES-124/-plsql_window_functions_28751_Hugues/blob/main/full%20outer%20join.png)

select c.customer_id,c.customer_names,p.product_id,p.product_name from customers c full outer join orders o on c.order_id=o.order_id full outer join products p on p.product_id= o.product_id;

--self_join
#/*self_join  self join is used to compare may be rows inside a table 
 for example to compare the orders that were made at the same date*/
 ![self join](https://github.com/HUGUES-124/-plsql_window_functions_28751_Hugues/blob/main/self%20join.png)

 select  a.order_id,b.order_id,a.order_date,b.order_date from orders a inner join orders b on a.order_date=b.order_date ;

 # WINDOW FUNCTIONS

 /*1.Ranking functions : (Using Rank() function helps you to rank rows according 
#to certain criteria. For my case I ranked products according to the product price)  */ ![Rank()](https://github.com/HUGUES-124/-plsql_window_functions_28751_Hugues/blob/main/rank.png)

 a.SELECT product_name, prod_price,RANK() OVER (ORDER BY prod_price DESC) AS product_rank FROM products;
-- to not jump a number when there is a tie we use DENSE_RANK
SELECT product_name, prod_price,DENSE_RANK() OVER (ORDER BY prod_price DESC) AS product_rank FROM products;

 /*2.Aggregate functions : The function sum() was used in the above query to show each date and the orders made.
  So here we can see a date and the total orders that took place
. If one wants to avoid duplicates we can use group by and order by .*/
![sum ()](https://github.com/HUGUES-124/-plsql_window_functions_28751_Hugues/blob/main/sum().png)

select order_date ,sum(quantity) OVER (Partition by order_date order by quantity) AS total_orders from orders ;
select product_name,prod_price,avg(prod_price) OVER (partition by product_name order by prod_price) from products;

 /*3.Navigation functions lag( ) accesses data from the previous row while lead( ) accesses data from the following row. 
This can be used to track the performance sequentially */ 
![lag()&lead()](https://github.com/HUGUES-124/-plsql_window_functions_28751_Hugues/blob/main/lead%26lag.png ) 

select order_date,quantity ,lag(quantity) OVER (Order by quantity) from orders;
select order_date,quantity ,lead(quantity) OVER (Order by quantity) from orders;

 /*4.Distibution functions  The function NTILE ( ) is used to distribute the rows into classes. 
For example here we have 4 classes where each has two rows.*/ ![NTILE()]( https://github.com/HUGUES-124/-plsql_window_functions_28751_Hugues/blob/main/Ntile.png)

  select product_name,prod_price ,NTILE(4) OVER (ORDER BY prod_price DESC) from products;
  -- cume_dist() is used to calculate relative rank of a value within values. 
  ![cume_disk()](https://github.com/HUGUES-124/-plsql_window_functions_28751_Hugues/blob/main/cume_disk().png )

   select product_name,prod_price ,CUME_DIST() OVER (ORDER BY prod_price DESC) from products;


# Result Analysis
# what the database is about
The KMEI_Shop database is a database that keeps records and transactions that are done by the shop where it stores the records regarding the products purchased their selling price and the orders made by the customers and the suppliers that will supply the orders from the stock to the customers that made the order.

# why this database was needed ?
 The KMEI_shop was needed as before the shop had the difficulties to keep records using papers where it was not well organized. The database helps to retrieve any records needed easily using joins and to make other different operations.

# What should be done next ?
Next as we have to increase the market this means the database has to increase also it's records may be add tables and attributes to keep records better and retrieve all needed records easily.

# References
* W3schools
* Guidance from Gemini Pro.


 #  "All sources were properly cited. Implementations and analysis represent original work.No AIgenerated content was copied without attribution or adaptation.”

  
 
