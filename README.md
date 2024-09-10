# restaurant-order-system.
BASIC PROJECT
-- Customers tablosu
CREATE TABLE Customers (
    CustomerID INT PRIMARY KEY,
    CustomerName VARCHAR(100),
    ContactNumber VARCHAR(15),
    Email VARCHAR(100),
    Address VARCHAR(200)
);

-- Employees tablosu
CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    EmployeeName VARCHAR(100),
    Position VARCHAR(50),
    HireDate DATE
);

-- Menu_Items tablosu
CREATE TABLE Menu_Items (
    MenuItemID INT PRIMARY KEY,
    ItemName VARCHAR(100),
    Price DECIMAL(5, 2),
    Category VARCHAR(50)
);

-- Orders tablosu
CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    OrderDate DATE,
    CustomerID INT,
    EmployeeID INT,
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID),
    FOREIGN KEY (EmployeeID) REFERENCES Employees(EmployeeID)
);

-- Order_Details tablosu
CREATE TABLE Order_Details (
    OrderDetailID INT PRIMARY KEY,
    OrderID INT,
    MenuItemID INT,
    Quantity INT,
    FOREIGN KEY (OrderID) REFERENCES Orders(OrderID),
    FOREIGN KEY (MenuItemID) REFERENCES Menu_Items(MenuItemID)
);

-- Müşteri verileri
INSERT INTO Customers (CustomerID, CustomerName, ContactNumber, Email, Address)
VALUES
(1, 'John Doe', '1234567890', 'john@example.com', '123 Elm St'),
(2, 'Jane Smith', '0987654321', 'jane@example.com', '456 Oak St');

-- Çalışan verileri
INSERT INTO Employees (EmployeeID, EmployeeName, Position, HireDate)
VALUES
(1, 'Alice Johnson', 'Waitress', '2020-05-10'),
(2, 'Bob Williams', 'Chef', '2018-03-22');

-- Menü öğeleri
INSERT INTO Menu_Items (MenuItemID, ItemName, Price, Category)
VALUES
(1, 'Margherita Pizza', 12.99, 'Pizza'),
(2, 'Spaghetti Carbonara', 9.99, 'Pasta'),
(3, 'Caesar Salad', 6.99, 'Salad');

-- Siparişler ve sipariş detayları
INSERT INTO Orders (OrderID, OrderDate, CustomerID, EmployeeID)
VALUES
(1, '2024-09-09', 1, 1);

INSERT INTO Order_Details (OrderDetailID, OrderID, MenuItemID, Quantity)
VALUES
(1, 1, 1, 2),
(2, 1, 3, 1);

SELECT o.OrderID, o.OrderDate, e.EmployeeName, od.Quantity, m.ItemName
FROM Orders o
JOIN Order_Details od ON o.OrderID = od.OrderID
JOIN Menu_Items m ON od.MenuItemID = m.MenuItemID
JOIN Employees e ON o.EmployeeID = e.EmployeeID
WHERE o.CustomerID = 1;

SELECT m.ItemName, SUM(od.Quantity) AS TotalQuantity
FROM Order_Details od
JOIN Menu_Items m ON od.MenuItemID = m.MenuItemID
GROUP BY m.ItemName
ORDER BY TotalQuantity DESC
LIMIT 1;
SELECT o.OrderID, o.OrderDate, c.CustomerName
FROM Orders o
JOIN Customers c ON o.CustomerID = c.CustomerID
WHERE o.EmployeeID = 1;

