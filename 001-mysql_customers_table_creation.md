# MySQL Table Creation and Data Insertion

## Step 1: Create the `customers` Table

```sql
USE mySchema;

CREATE TABLE customers (
    customer_id INT AUTO_INCREMENT PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    email VARCHAR(100),
    phone_number VARCHAR(15),
    address VARCHAR(255),
    city VARCHAR(50),
    state VARCHAR(50),
    zip_code VARCHAR(10)
);
```

## Step 2: Insert Data into the `customers` Table

```sql
USE mySchema;

INSERT INTO customers (first_name, last_name, email, phone_number, address, city, state, zip_code)
VALUES
('Alice', 'Johnson', 'alice.johnson@example.com', '555-1234', '123 Maple Ave', 'Austin', 'TX', '73301'),
('Bob', 'Williams', 'bob.williams@example.com', '555-5678', '456 Oak Ave', 'Austin', 'TX', '73301'),
('Charlie', 'Brown', 'charlie.brown@example.com', '555-8765', '789 Pine Ave', 'Houston', 'TX', '77001'),
('Diana', 'Miller', 'diana.miller@example.com', '555-4321', '101 Birch Ave', 'Houston', 'TX', '77001'),
('Edward', 'Davis', 'edward.davis@example.com', '555-9876', '202 Cedar Ave', 'Dallas', 'TX', '75201'),
('Fiona', 'Wilson', 'fiona.wilson@example.com', '555-6543', '303 Spruce Ave', 'Dallas', 'TX', '75201'),
('George', 'Moore', 'george.moore@example.com', '555-3210', '404 Elm Ave', 'San Antonio', 'TX', '78201'),
('Helen', 'Taylor', 'helen.taylor@example.com', '555-2109', '505 Cherry Ave', 'San Antonio', 'TX', '78201'),
('Ian', 'Anderson', 'ian.anderson@example.com', '555-1098', '606 Ash Ave', 'Fort Worth', 'TX', '76101'),
('Jane', 'Thomas', 'jane.thomas@example.com', '555-0987', '707 Willow Ave', 'Fort Worth', 'TX', '76101');

INSERT INTO customers (first_name, last_name, email, phone_number, address, city, state, zip_code)
VALUES
('John', 'Doe', 'john.doe@example.com', '555-1234', '123 Elm St', 'Springfield', 'IL', '62701'),
('Jane', 'Smith', 'jane.smith@example.com', '555-5678', '456 Oak St', 'Springfield', 'IL', '62701'),
('Michael', 'Johnson', 'michael.johnson@example.com', '555-8765', '789 Pine St', 'Chicago', 'IL', '60601'),
('Emily', 'Davis', 'emily.davis@example.com', '555-4321', '101 Maple St', 'Chicago', 'IL', '60601'),
('James', 'Brown', 'james.brown@example.com', '555-9876', '202 Birch St', 'Peoria', 'IL', '61602'),
('Patricia', 'Wilson', 'patricia.wilson@example.com', '555-6543', '303 Cedar St', 'Peoria', 'IL', '61602'),
('Robert', 'Taylor', 'robert.taylor@example.com', '555-3210', '404 Walnut St', 'Naperville', 'IL', '60540'),
('Linda', 'Anderson', 'linda.anderson@example.com', '555-2109', '505 Cherry St', 'Naperville', 'IL', '60540'),
('David', 'Thomas', 'david.thomas@example.com', '555-1098', '606 Spruce St', 'Aurora', 'IL', '60505'),
('Barbara', 'Jackson', 'barbara.jackson@example.com', '555-0987', '707 Elm St', 'Aurora', 'IL', '60505');

```

## Explanation:

1. **Table Creation (`CREATE TABLE`)**:

   - `customer_id` is the primary key and uses `AUTO_INCREMENT` to automatically assign a unique ID to each customer.
   - Other columns (`first_name`, `last_name`, `email`, etc.) hold specific pieces of information about each customer.

2. **Data Insertion (`INSERT INTO`)**:
   - The `INSERT INTO` statement adds rows of data into the `customers` table.
   - Each `VALUES` clause corresponds to one customer’s data.

This script creates a table to store customer information and inserts data for 10 different customers. You can run this script in your MySQL environment to set up the table and populate it with the data.
