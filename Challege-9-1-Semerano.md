# Challenge Set 9
## Part I: W3Schools SQL Lab 

*Introductory level SQL*

--

This challenge uses the [W3Schools SQL playground](http://www.w3schools.com/sql/trysql.asp?filename=trysql_select_all). Please add solutions to this markdown file and submit.

1. Which customers are from the UK?  
   
   SELECT * FROM Customers WHERE Country="UK"
   
### There are 7 customers from the UK.  They have customer IDs of 4, 11, 16, 19, 38, 53, 72.

2. What is the name of the customer who has the most orders?   

SELECT customers.CustomerID, Customers.CustomerName, COUNT(Orders.OrderID) as OrdersCount FROM Customers INNER JOIN Orders ON Customers.CustomerID = Orders.CustomerID GROUP BY Customers.CustomerID, Customers.CustomerName ORDER BY OrderCount DESC LIMIT 5

### The customer with the most orders is Ernst Handel.
  
3. Which supplier has the highest average product price? 

SELECT Suppliers.SupplierID, Products.SupplierID, Suppliers.SupplierName, AVG(Products.Price) FROM Suppliers INNER JOIN Products ON Suppliers.SupplierID = Products.SupplierID GROUP BY Suppliers.SupplierID, Suppliers.SupplierName, Price ORDER BY AVG(Price) DESC;

### Aux joyeux ecclésiastiques has the highest average product price.
  
4. How many different countries are all the customers from?

SELECT COUNT(DISTINCT(Country)) FROM Customers;

### The customers are from 21 different countries.
  
5. What category appears in the most orders?  
OrderDetailID	OrderID	ProductID	Quantity
OrderID	CustomerID	EmployeeID	OrderDate	ShipperID
CategoryID	CategoryName	Description
ProductID	ProductName	SupplierID	CategoryID	Unit	Price
EmployeeID	LastName	FirstName	BirthDate	Photo	Notes
SupplierID	SupplierName	ContactName	Address etc

SELECT OrderDetailID, Count(OrderID), od.ProductID, CategoryName, cat.CategoryID  FROM Products as pr INNER JOIN OrderDetails as od ON pr.ProductID = od.ProductID INNER JOIN Categories as cat ON pr.CategoryID = cat.CategoryID GROUP BY cat.CategoryID, CategoryName ORDER BY Count(OrderID)  DESC Limit 10;

### Dairy Products appear in the most orders.  
6. What was the total cost for each order?  

SELECT  OrderID, od.ProductID, SUM(Price)  FROM Products as pr INNER JOIN OrderDetails as od ON pr.ProductID = od.ProductID GROUP BY OrderID Order BY SUM(price) ASC Limit 10;

###Total order costs range from 460.34 to 2.50. 
   
7. Which employee made the most sales (by total price)? 

SELECT ord.EmployeeID, LastName, FirstName, ord.OrderID, od.ProductID, Quantity, SUM(Price)  FROM Orders as ord INNER JOIN Employees as emp on ord.EmployeeID = emp.EmployeeID INNER JOIN OrderDetails as od ON od.OrderID = ord.OrderID INNER JOIN Products as pr ON od.ProductID = pr.ProductID GROUP BY ord.OrderID, ord.EmployeeID ORDER BY SUM(Price) DESC Limit 5;

###Margaret Peacock had the most sales by price.
     
8. Which employees have BS degrees? 

SELECT LastName, FirstName, Notes FROM Employees;

###Janet Leverling and Steve Buchanan have BS degrees.
  
9. Which supplier of three or more products has the highest average product price? 

SELECT COUNT(ProductID), ProductName, pr.SupplierID, SupplierName, AVG(Price) FROM Suppliers as sup INNER JOIN Products as pr ON sup.SupplierID = pr.SupplierID GROUP BY SupplierName ORDER BY COUNT(ProductID) DESC LIMIT 18;

###Tokyo Traders had the highest average product price of 46.
