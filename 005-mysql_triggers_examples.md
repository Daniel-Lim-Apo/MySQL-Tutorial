# MySQL Triggers Examples

These examples demonstrate how to create and use triggers in MySQL to log changes, validate data, and maintain a history of table operations. Triggers are useful for automatically enforcing business rules and auditing changes to your data.

## 1. Creating Triggers

### Example: Trigger After Insert

```sql
DELIMITER $$

CREATE TRIGGER after_customer_insert
AFTER INSERT ON customers
FOR EACH ROW
BEGIN
    INSERT INTO customers_log (action, customer_id, log_time)
    VALUES ('INSERT', NEW.customer_id, NOW());
END $$

DELIMITER ;
```

This trigger runs after a new record is inserted into the `customers` table and logs the action in the `customers_log` table.

## 2. Logging Changes to Tables (INSERT, UPDATE, DELETE)

### Example: Trigger After Update

```sql
DELIMITER $$

CREATE TRIGGER after_customer_update
AFTER UPDATE ON customers
FOR EACH ROW
BEGIN
    INSERT INTO customers_log (action, customer_id, log_time, old_email, new_email)
    VALUES ('UPDATE', NEW.customer_id, NOW(), OLD.email, NEW.email);
END $$

DELIMITER ;
```

This trigger logs any updates made to the `customers` table, recording both the old and new email addresses.

### Example: Trigger After Delete

```sql
DELIMITER $$

CREATE TRIGGER after_customer_delete
AFTER DELETE ON customers
FOR EACH ROW
BEGIN
    INSERT INTO customers_log (action, customer_id, log_time)
    VALUES ('DELETE', OLD.customer_id, NOW());
END $$

DELIMITER ;
```

This trigger logs deletions from the `customers` table, noting the ID of the deleted customer.

## 3. Validating Data Before Allowing Operations

### Example: Trigger Before Insert to Validate Data

```sql
DELIMITER $$

CREATE TRIGGER before_customer_insert
BEFORE INSERT ON customers
FOR EACH ROW
BEGIN
    IF NEW.email NOT LIKE '%@%.%' THEN
        SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'Invalid email address';
    END IF;
END $$

DELIMITER ;
```

This trigger checks if the email format is valid before allowing an insert operation. If not, it raises an error.

## 4. Using Triggers for History Logging

### Example: Trigger to Log Historical Data Before Update

```sql
DELIMITER $$

CREATE TRIGGER before_customer_update
BEFORE UPDATE ON customers
FOR EACH ROW
BEGIN
    INSERT INTO customers_history (customer_id, first_name, last_name, email, modified_time)
    VALUES (OLD.customer_id, OLD.first_name, OLD.last_name, OLD.email, NOW());
END $$

DELIMITER ;
```

This trigger saves the current state of a customer’s record into a history table before the record is updated, allowing you to track changes over time.

---
