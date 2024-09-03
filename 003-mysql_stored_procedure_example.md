# MySQL Stored Procedure Example

This example demonstrates how to create and use a stored procedure in MySQL to filter and retrieve specific parts of a table based on input parameters.

## Creating a Stored Procedure to Retrieve Part of a Table

### Stored Procedure to Get Customers by State

```sql
DELIMITER $$

CREATE PROCEDURE GetCustomersByState(IN state_param VARCHAR(50))
BEGIN
    SELECT customer_id, first_name, last_name, email, city, state
    FROM customers
    WHERE state = state_param;
END $$

DELIMITER ;
```

### Explanation:

- **DELIMITER**: The `DELIMITER $$` statement changes the delimiter to `$$` to allow the use of `;` within the procedure body without ending the procedure definition.
- **CREATE PROCEDURE**: This command creates a stored procedure named `GetCustomersByState`.
- **IN state_param VARCHAR(50)**: This declares an input parameter `state_param` of type `VARCHAR(50)` to be passed to the procedure.
- **SELECT**: The procedure retrieves `customer_id`, `first_name`, `last_name`, `email`, `city`, and `state` from the `customers` table where the `state` matches the `state_param` passed to the procedure.
- **END $$**: Marks the end of the procedure definition.
- **DELIMITER ;**: Resets the delimiter back to the default `;`.

### How to Call the Stored Procedure:

```sql
CALL GetCustomersByState('TX');

CALL GetCustomersByState('IL');
```

This command calls the `GetCustomersByState` stored procedure, passing 'TX' oa 'IL' as the parameter to retrieve all customers from Texas or Illinois.

---
