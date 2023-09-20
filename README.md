# SQL_Practice_code
SHOW DATABASES;
CREATE DATABASE southwind;
DROP DATABASE southwind;
CREATE DATABASE IF NOT EXISTS southwind;
DROP DATABASE IF EXISTS southwind;
CREATE DATABASE southwind;
SHOW DATABASES;
USE southwind;
SELECT DATABASE();
SHOW TABLES;
CREATE TABLE IF NOT EXISTS products (
         productID    INT UNSIGNED  NOT NULL AUTO_INCREMENT,
         productCode  CHAR(3)       NOT NULL DEFAULT '',
         name         VARCHAR(30)   NOT NULL DEFAULT '',
         quantity     INT UNSIGNED  NOT NULL DEFAULT 0,
         price        DECIMAL(7,2)  NOT NULL DEFAULT 99999.99,
         PRIMARY KEY  (productID)
       );
SHOW TABLES;
DESCRIBE products;
INSERT INTO products VALUES (1001, 'PEN', 'Pen Red', 5000, 1.23);
INSERT INTO products VALUES
         (NULL, 'PEN', 'Pen Blue',  8000, 1.25),
         (NULL, 'PEN', 'Pen Black', 2000, 1.25);
         
INSERT INTO products (productCode, name, quantity, price) VALUES
         ('PEC', 'Pencil 2B', 10000, 0.48),
         ('PEC', 'Pencil 2H', 8000, 0.49);
INSERT INTO products (productCode, name) VALUES ('PEC', 'Pencil HB');
INSERT INTO products values (NULL, NULL, NULL, NULL, NULL);
SELECT * FROM products;
DELETE FROM products WHERE productID = 1006;
SELECT name, price FROM products;
SELECT * FROM products;
SELECT name, price FROM products WHERE price < 1.0;
SELECT name, quantity FROM products WHERE quantity <= 2000;
SELECT name, price FROM products WHERE productCode = 'PEN';
SELECT * FROM products WHERE name IN ('Pen Red', 'Pen Black');
SELECT * FROM products 
       WHERE (price BETWEEN 1.0 AND 2.0) AND (quantity BETWEEN 1000 AND 2000);
SELECT * FROM products WHERE productCode = NULL;
SELECT * FROM products WHERE productCode IS NULL;
SELECT productID AS ID, productCode AS Code,
              name AS Description, price AS `Unit Price`  -- Define aliases to be used as display names
       FROM products
       ORDER BY ID;
SELECT price FROM products;
SELECT DISTINCT price AS `Distinct Price` FROM products;
SELECT * FROM products ORDER BY productCode, productID;
SELECT * FROM products ORDER BY productCode;
SELECT MAX(price), MIN(price), AVG(price), STD(price), SUM(quantity)
       FROM products;
UPDATE products SET price = price * 1.1;
SET SQL_SAFE_UPDATES = 0;
SET SQL_SAFE_UPDATES = 1;
SELECT * FROM products; 
UPDATE products SET quantity = quantity - 100 WHERE name = 'Pen Red';
SELECT * FROM products WHERE name = 'Pen Red';
UPDATE products SET quantity = quantity + 50, price = 1.23 WHERE name = 'Pen Red';
SELECT * FROM products WHERE name = 'Pen Red';
DELETE FROM products WHERE name LIKE 'Pencil%';
SELECT * FROM products;
DELETE FROM products;
USE southwind;
DROP TABLE IF EXISTS suppliers;
CREATE TABLE suppliers (
         supplierID  INT UNSIGNED  NOT NULL AUTO_INCREMENT, 
         name        VARCHAR(30)   NOT NULL DEFAULT '', 
         phone       CHAR(8)       NOT NULL DEFAULT '',
         PRIMARY KEY (supplierID)
       );
DESCRIBE suppliers;
INSERT INTO suppliers VALUE
          (501, 'ABC Traders', '88881111'), 
          (502, 'XYZ Company', '88882222'), 
          (503, 'QQ Corp', '88883333');
SELECT * FROM suppliers;
ALTER TABLE products
       ADD COLUMN supplierID INT UNSIGNED NOT NULL;
DESCRIBE products;
UPDATE products SET supplierID = 501;
ALTER TABLE products
       ADD FOREIGN KEY (supplierID) REFERENCES suppliers (supplierID);
DESCRIBE products;
UPDATE products SET supplierID = 502 WHERE productID  = 1004;
SELECT * FROM products;
SELECT products.name, price, suppliers.name 
       FROM products 
          JOIN suppliers 
          ON products.supplierID = suppliers.supplierID
       WHERE price < 0.6;
