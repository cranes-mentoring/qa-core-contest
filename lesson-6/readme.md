## SQL core

---

**Introduction:**

SQL (Structured Query Language) is a fundamental tool for testers working with databases. Whether you are testing a web application, mobile app, or internal software product, understanding SQL basics is a crucial skill for ensuring effective testing. In this article, we will explore fundamental SQL concepts that are essential for a tester.

---

**1. SQL Basics:**

SQL provides a standardized way to interact with databases. Key concepts that a tester should know include:

- **Tables:** Databases consist of tables, which are structured sets of data. Each row in a table represents a single record, and columns define data types.

  Example:

  ```sql
  CREATE TABLE Users (
    UserID INT PRIMARY KEY,
    UserName VARCHAR(50),
    Email VARCHAR(100)
  );
  ```

- **Queries:** SQL queries are used to extract, update, insert, and delete data. Primary query operators include SELECT, INSERT, UPDATE, and DELETE.

  Example:

  ```sql
  SELECT UserName, Email FROM Users WHERE UserID = 1;
  ```

- **Constraints:** Constraints define rules that data must follow. For instance, PRIMARY KEY ensures the uniqueness of values in a column.

  Example:

  ```sql
  ALTER TABLE Users ADD CONSTRAINT PK_Users_UserID PRIMARY KEY (UserID);
  ```

---

**2. SELECT Queries:**

SELECT queries are the primary tool for retrieving data from a database. Testers should be familiar with:

- **Selecting Specific Columns (SELECT column1, column2):** Determining which columns to retrieve from a table.

  Example:

  ```sql
  SELECT FirstName, LastName FROM Employees;
  ```

- **WHERE Conditions (SELECT * FROM table WHERE condition):** Filtering data using conditions.

  Example:

  ```sql
  SELECT ProductName, Price FROM Products WHERE Price > 50;
  ```

- **Sorting (ORDER BY column):** Ordering query results.

  Example:

  ```sql
  SELECT City, Population FROM Cities ORDER BY Population DESC;
  ```

---

**3. Data Manipulation:**

Testers should also be able to modify data in the database:

- **Inserting Data (INSERT INTO table VALUES):** Adding new records to a table.

  Example:

  ```sql
  INSERT INTO Customers (CustomerName, ContactName, Country) VALUES ('CompanyABC', 'John Doe', 'USA');
  ```

- **Updating Data (UPDATE table SET column=value WHERE condition):** Modifying existing records.

  Example:

  ```sql
  UPDATE Products SET StockQuantity = StockQuantity - 1 WHERE ProductID = 101;
  ```

- **Deleting Data (DELETE FROM table WHERE condition):** Removing records from a table.

  Example:

  ```sql
  DELETE FROM Orders WHERE OrderID = 1001;
  ```

---

**4. Joins:**

An important aspect of testing is the ability to combine data from different tables:

- **INNER JOIN, LEFT JOIN, RIGHT JOIN:** Different types of joins allowing data combination based on specific conditions.

  Example:

  ```sql
  SELECT Customers.CustomerName, Orders.OrderID
  FROM Customers
  INNER JOIN Orders ON Customers.CustomerID = Orders.CustomerID;
  ```

---

**5. Grouping and Aggregation:**

Testers should understand how to work with grouped data and use aggregate functions:

- **GROUP BY, HAVING:** Grouping data and filtering groups.

  Example:

  ```sql
  SELECT Country, COUNT(*) AS NumberOfCustomers FROM Customers GROUP BY Country HAVING COUNT(*) > 1;
  ```

- **COUNT, SUM, AVG, MAX, MIN:** Aggregate functions for analyzing data within groups.

  Example:

  ```sql
  SELECT Category, AVG(Price) AS AveragePrice FROM Products GROUP BY Category;
  ```

---

**Conclusion:**

Understanding SQL basics is a key element in a tester's toolkit. Knowing the structure of a database, forming effective queries, and interacting with data helps testers perform their job efficiently, ensuring the quality and reliability of software products. It is essential to continually deepen your knowledge of SQL, as this enhances professional competence and leads to successful database testing.