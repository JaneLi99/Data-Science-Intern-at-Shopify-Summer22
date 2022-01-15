# Data-Science-Intern-at-Shopify-Summer22


## Summer 2022 Data Science Intern Challenge 

Please complete the following questions, and provide your thought process/work. You can attach your work in a text file, link, etc. on the application page. Please ensure answers are easily visible for reviewers!


#### Question 1: Given some sample data, write a program to answer the following: click here to access the required data set

On Shopify, we have exactly 100 sneaker shops, and each of these shops sells only one model of shoe. We want to do some analysis of the average order value (AOV). When we look at orders data over a 30 day window, we naively calculate an AOV of $3145.13. Given that we know these shops are selling sneakers, a relatively affordable item, something seems wrong with our analysis. 

**a. Think about what could be going wrong with our calculation. Think about a better way to evaluate this data.**

The AOV value seems wrong because, in the dataset file, order_amount has many values equal to 70400, which could lead the AOV value to be much greater. I drew the boxplot and found that 70400 is too far from the main box. So I removed 70400 and drew again. 

**b. What metric would you report for this dataset?**

From my guesses, the median value of order_amount would be more convinced. I calculated the median of order_amount with and without 70400 and the results all return 284.

**c. What is its value?**

284


#### Question 2: For this question you’ll need to use SQL. Follow this link to access the data set required for the challenge. Please use queries to answer the following questions. Paste your queries along with your final numerical answers below.

**a. How many orders were shipped by Speedy Express in total?**

54 in total.<br />
SELECT COUNT(o.ShipperID)<br />
FROM Orders AS o<br />
WHERE (SELECT ShipperID <br />
    FROM Shippers AS s<br />
    WHERE s.ShipperName == "Speedy Express") == o.ShipperID;

**b. What is the last name of the employee with the most orders?**

Peacock.<br />
SELECT LastName <br />
FROM Orders o JOIN Employees e ON o.EmployeeID = e.EmployeeID<br />
GROUP BY o.EmployeeID<br />
ORDER BY COUNT(*) DESC<br />
LIMIT 1

**c. What product was ordered the most by customers in Germany?**

Steeleye Stout.<br />
SELECT ProductName<br />
FROM Orders o JOIN Customers c ON o.CustomerID = c.CustomerID <br />
JOIN OrderDetails d ON o.OrderID = d.OrderID <br />
JOIN Products p ON p.ProductID = d.ProductID<br />
WHERE Country='Germany'<br />
ORDER BY Quantity DESC<br />
LIMIT 1

