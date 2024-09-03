# MySQL Stored Procedures Examples

These examples demonstrate various aspects of working with stored procedures in MySQL, including data retrieval, insertion, updates, exception handling, and more. Stored procedures offer powerful tools for encapsulating business logic within the database.

## 1. Creating Stored Procedures to Display Data from a Table

### Example: Procedure to Display All Customers

```sql
DELIMITER $$

CREATE PROCEDURE ShowAllCustomers()
BEGIN
    SELECT * FROM customers;
END $$

DELIMITER ;
```

This procedure displays all records from the `customers` table.

## 2. Using Parameters to Filter Data

### Example: Procedure to Display Customers by City

```sql
DELIMITER $$

CREATE PROCEDURE ShowCustomersByCity(IN city_param VARCHAR(50))
BEGIN
    SELECT * FROM customers WHERE city = city_param;
END $$

DELIMITER ;
```

This procedure displays customers from a specific city passed as a parameter.

## 3. Creating Stored Procedures to Insert Data into a Table

### Example: Procedure to Insert a New Customer

```sql
DELIMITER $$

CREATE PROCEDURE InsertCustomer(
    IN first_name_param VARCHAR(50),
    IN last_name_param VARCHAR(50),
    IN email_param VARCHAR(100),
    IN phone_param VARCHAR(15),
    IN address_param VARCHAR(255),
    IN city_param VARCHAR(50),
    IN state_param VARCHAR(50),
    IN zip_code_param VARCHAR(10)
)
BEGIN
    INSERT INTO customers (first_name, last_name, email, phone_number, address, city, state, zip_code)
    VALUES (first_name_param, last_name_param, email_param, phone_param, address_param, city_param, state_param, zip_code_param);
END $$

DELIMITER ;
```

This procedure inserts a new customer record into the `customers` table.

## 4. Using Conditionals to Insert Data

### Example: Procedure to Insert a Customer if Not Exists

```sql
DELIMITER $$

CREATE PROCEDURE InsertCustomerIfNotExists(
    IN email_param VARCHAR(100),
    IN first_name_param VARCHAR(50),
    IN last_name_param VARCHAR(50)
)
BEGIN
    IF NOT EXISTS (SELECT 1 FROM customers WHERE email = email_param) THEN
        INSERT INTO customers (first_name, last_name, email)
        VALUES (first_name_param, last_name_param, email_param);
    END IF;
END $$

DELIMITER ;
```

This procedure inserts a customer only if they do not already exist in the table based on their email.

## 5. Creating Stored Procedures to Update Data in a Table

### Example: Procedure to Update Customer Email

```sql
DELIMITER $$

CREATE PROCEDURE UpdateCustomerEmail(
    IN customer_id_param INT,
    IN new_email_param VARCHAR(100)
)
BEGIN
    UPDATE customers SET email = new_email_param WHERE customer_id = customer_id_param;
END $$

DELIMITER ;
```

This procedure updates the email address of a customer based on their ID.

## 6. Using Loops to Update Data

### Example: Procedure to Update Customer State in Bulk

```sql
DELIMITER $$

CREATE PROCEDURE UpdateCustomerState(
    IN old_state_param VARCHAR(50),
    IN new_state_param VARCHAR(50)
)
BEGIN
    DECLARE done INT DEFAULT FALSE;
    DECLARE cust_id INT;

    DECLARE cur CURSOR FOR SELECT customer_id FROM customers WHERE state = old_state_param;
    DECLARE CONTINUE HANDLER FOR NOT FOUND SET done = TRUE;

    OPEN cur;

    read_loop: LOOP
        FETCH cur INTO cust_id;
        IF done THEN
            LEAVE read_loop;
        END IF;
        UPDATE customers SET state = new_state_param WHERE customer_id = cust_id;
    END LOOP;

    CLOSE cur;
END $$

DELIMITER ;
```

This procedure updates the state for all customers from a specific old state to a new state using a loop.

## 7. Exception Handling in Stored Procedures

### Example: Procedure with Exception Handling

```sql
DELIMITER $$

CREATE PROCEDURE SafeInsertCustomer(
    IN first_name_param VARCHAR(50),
    IN last_name_param VARCHAR(50),
    IN email_param VARCHAR(100)
)
BEGIN
    DECLARE CONTINUE HANDLER FOR SQLEXCEPTION
    BEGIN
        -- Error handling code
        ROLLBACK;
    END;

    START TRANSACTION;

    INSERT INTO customers (first_name, last_name, email)
    VALUES (first_name_param, last_name_param, email_param);

    COMMIT;
END $$

DELIMITER ;
```

This procedure demonstrates how to handle exceptions by rolling back the transaction if an error occurs.

## 8. Data Migration Between Tables and Views Using Stored Procedures

### Example: Procedure to Migrate Data to an Archive Table

```sql
DELIMITER $$

CREATE PROCEDURE MigrateOldCustomers()
BEGIN
    INSERT INTO customers_archive
    SELECT * FROM customers WHERE created_at < NOW() - INTERVAL 1 YEAR;

    DELETE FROM customers WHERE created_at < NOW() - INTERVAL 1 YEAR;
END $$

DELIMITER ;
```

This procedure migrates customers older than one year to an archive table and then deletes them from the main table.

## 9. Stored Procedures vs. Functions

### Stored Procedures:

- Can perform multiple operations (e.g., insert, update, delete).
- Do not need to return a value but can do so if required.
- Can include transaction control (COMMIT, ROLLBACK).
- Example: Inserting a new customer into a table.

### Functions:

- Must return a value.
- Cannot perform transaction control.
- Typically used for calculations or to return a single value.
- Example: A function to calculate the total order amount for a customer.

---
