## Filtering data

### WHERE
  SELECT column_name 
  FROM table_name 
  WHERE column_name operator values;
 
  WHERE <> 'Alice Mutton'; --not equal to(or maybe in other SQL is !=
  
  WHERE UnitsInStock BETWEEN 15 AND 80;
  
  WHERE ProductName IS NULL
  
### IN
  WHERE SupplierID IN (9,10,11);
  
  Benefits of IN: 
  --you can make a long list of options 
  --faster than OR 
  --don't need to think about order 
  --can contain another SELECT 
  
### OR
  WHERE ProductName = 'Tofu' OR 'Konbu';
  
### OR with AND
  WHERE SupplierID =9 OR SupplierID =11  
  AND UnitPrice>15
  
  WHERE (SupplierID =9 OR SupplierID =11)  
  AND UnitPrice>15
  
  --the order of operations, use()
  
  
### NOT
  WHERE NOT City='London' AND NOT City='Seattle';
  
### Wildcards (use LIKE)
can only be used with strings 

  %Pizza --anything ending with the word pizza 
  Pizza% --anything after pizza 
  %Pizza% --anything before and after the word pizza 
  S%E --anything that starts with S and ends with E
  
% wildcard will not match NULLs

  WHERE size LIKE '%pizza' 
  WHERE size LIKE '_pizza'
   
    
## Sorting

### ORDER BY 

* must always be the last clause in a select statement 

  ORDER BY 2,3 
  --2nd column and 3rd column 
  
  DESC descending order 
  ASC ascending order 
  
  
  
## Match Operations

  SELECT ProductID 
  ,UnitsOnOrder * UnitPrice AS Total_Order_Cost 
  FROM Products 

## Aggragate functions 
### avg() 
  --rows containing NULL values are ignored by the avg() function 
### count()
  SELECT COUNT(*) AS total_customers --counts all the rows containing values and NULL  
  SELECT COUNT(customerid) AS total_customers --counts all the rows in a specific column ignoring NULL 
### min() --NULL are ignored 
### max() --NULL are ignored
### sum() 
  SELECT SUM(unitprice * unitsinstock) AS total_price 
  FROM Products 
  WHERE supplierid=23; 
  
### DISTINCT on aggregate functions: 
  SELECT COUNT(DISTINCT customerid) 
  FROM customers 
  --this can prevent getting duplicates
  --cannot use on count(*)
  
  
## Grouping 

### GROUP BY
SELECT region 
,COUNT (customerid) AS total_customers 
FORM customers 
GROUP BY region; 

--every column in your SELECT statement must be present in a GROUP BY clause, except for aggregated calculations 
--NULLs will be grouped together 

### HAVING 
  SELECT customerid 
  ,COUNT (*) AS orders 
  FROM orders 
  GROUP BY customerid 
  HAVING COUNT (*) >=2;  
  
--WHERE vs. HAVING 
 --WHERE filters before data is grouped 
 --HAVING filters after data is grouped 
 --rows eliminated by the WHERE clause will not be included in the group 
