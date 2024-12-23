# activite-sql


here is the script :
create table Customer(
CustomerID INT Not null primary key,
CustomerFirstName Varchar(50) not null,
CustomerLastName Varchar(50) not null,
CustomerAddress Varchar(50) not null,
CustomerCIty Varchar(50)  not null,
CustomerPostCode Char(4) null,
CustomerPhoneNumber char(12) null
);

create table inventory(
InventoryID tinyINT not null primary key,
InventoryName Varchar(50) not null,
InventoryDescription varchar(255) null
);
insert into inventory(InventoryID,InventoryName,InventoryDescription) values 
(1,'noidea','whatisthat'),
(2,'noidvfea','whatvffvisthat'),
(3,'noi5444dea','what545isthat');


create table employee(
EmployeeID tinyint not null primary key,
EmployeeFirstName varchar(50) not null,
EmployeeLastName varchar(50) not null,
EmployeeExtension char(4) not null
);


create table sale(
SaleID tinyint not null primary key,
CustomerID int not null,
InventoryID  tinyint not null,
EmployeeID tinyint not null,
SaleDate date not null,
SaleUnityPrice DECIMAL(10, 4) not null,
foreign key (CustomerID) references Customer(CustomerID),
foreign key (InventoryID) references inventory(InventoryID),
foreign key (EmployeeID) references employee(EmployeeID)
);


drop table inventaire;


insert into Customer(CustomerID,CustomerFirstName,CustomerLastName,CustomerAddress,CustomerCIty,CustomerPostCode,CustomerPhoneNumber) values 
(1,'REDA','JENHAJI','reda@gmail.com','SALE',100,0664146942),
(2,'ahmed','Jenan','ahmed@gmail.com','rabat',250,0652147896),
(3,'yassir','zbidaz','yasser@gmail.com','fes',102,0678451236);
INSERT INTO employee (EmployeeID, EmployeeFirstName, EmployeeLastName, EmployeeExtension) VALUES 
(1, 'John', 'Doe', '1234'),
(2, 'Jane', 'Smith', '5678'),
(3, 'Alice', 'Johnson', '9101');
INSERT INTO sale (SaleID, CustomerID, InventoryID, EmployeeID, SaleDate, SaleUnityPrice,SaleQuantity) VALUES 
(1, 1, 1, 1, '2024-12-20', 15.99 , 40),
(2, 2, 2, 2, '2024-12-21', 25.50 , 50 ),
(3, 3, 3, 3, '2024-12-22', 30.75 , 60);

DELETE FROM sale;
select * from Customer;

alter table sale 
add column SaleQuantity int not null;
select *,(SaleQuantity * SaleUnityPrice) as total from sale
ORDER BY  total DESC;

SELECT employee.EmployeeID, employee.EmployeeFirstName, employee.EmployeeLastName, 
       SUM(sale.SaleQuantity * sale.SaleUnityPrice) AS TotalSales
FROM sale
JOIN employee ON sale.EmployeeID = employee.EmployeeID
GROUP BY employee.EmployeeID, employee.EmployeeFirstName, employee.EmployeeLastName
HAVING TotalSales > 0;

ALTER TABLE Customer 
ADD CustomerEmail VARCHAR(100);


UPDATE Customer
SET CustomerEmail = 'newemail@example.com'
WHERE CustomerID = 1;

DELETE FROM Customer
WHERE CustomerCity = 'New York';

SELECT *
FROM sale
WHERE SaleDate >= CURDATE() - INTERVAL 30 DAY;


SELECT CustomerID, SaleID, SaleQuantity
FROM sale
WHERE SaleQuantity > 5;




