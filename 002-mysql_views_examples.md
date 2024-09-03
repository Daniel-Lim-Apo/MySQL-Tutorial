# MySQL Views Examples

## Criação de Views Usando Diferentes Tipos de Comandos

Esses exemplos demonstram como criar, modificar, atualizar e excluir views em MySQL.

### Exemplo 1: View Simples com SELECT

```sql
CREATE VIEW customer_emails AS
SELECT first_name, last_name, email
FROM customers;
```

Esta view, chamada `customer_emails`, mostra os nomes e e-mails dos clientes.

### Exemplo 2: View com Filtragem

```sql
CREATE VIEW texas_customers AS
SELECT first_name, last_name, city, state
FROM customers
WHERE state = 'TX';
```

A view `texas_customers` exibe apenas os clientes que estão no estado do Texas.

### Exemplo 3: View com Join

```sql

CREATE SCHEMA IF NOT EXISTS myschema;

CREATE TABLE myschema.orders (
    order_id INT AUTO_INCREMENT PRIMARY KEY,
    customer_id INT,
    order_date DATE,
    product_name VARCHAR(100),
    quantity INT,
    total_amount DECIMAL(10, 2),
    FOREIGN KEY (customer_id) REFERENCES myschema.customers(customer_id)
);

INSERT INTO myschema.orders (customer_id, order_date, product_name, quantity, total_amount)
VALUES
(1, '2024-09-01', 'Laptop', 1, 1200.00),
(2, '2024-09-02', 'Smartphone', 2, 1600.00),
(3, '2024-09-03', 'Tablet', 1, 300.00),
(4, '2024-09-04', 'Monitor', 2, 400.00),
(5, '2024-09-05', 'Keyboard', 1, 50.00),
(6, '2024-09-06', 'Mouse', 2, 40.00),
(7, '2024-09-07', 'Printer', 1, 150.00),
(8, '2024-09-08', 'External Hard Drive', 1, 100.00),
(9, '2024-09-09', 'Webcam', 1, 75.00),
(10, '2024-09-10', 'Headset', 1, 85.00),
(1, '2024-09-11', 'Laptop Bag', 1, 50.00),
(1, '2024-09-12', 'Wireless Mouse', 1, 25.00),
(2, '2024-09-13', 'Smartphone Case', 2, 40.00),
(2, '2024-09-14', 'Wireless Charger', 1, 30.00),
(3, '2024-09-15', 'Tablet Cover', 1, 20.00),
(3, '2024-09-16', 'Bluetooth Keyboard', 1, 70.00),
(4, '2024-09-17', 'Monitor Stand', 1, 60.00),
(4, '2024-09-18', 'HDMI Cable', 2, 30.00),
(5, '2024-09-19', 'Mechanical Keyboard', 1, 100.00),
(5, '2024-09-20', 'Gaming Mouse', 1, 45.00),
(6, '2024-09-21', 'Mouse Pad', 2, 20.00),
(6, '2024-09-22', 'USB Hub', 1, 25.00),
(7, '2024-09-23', 'Printer Ink', 3, 90.00),
(7, '2024-09-24', 'Photo Paper', 1, 15.00),
(8, '2024-09-25', 'Portable SSD', 1, 120.00),
(8, '2024-09-26', 'USB Flash Drive', 2, 40.00),
(9, '2024-09-27', 'Webcam Stand', 1, 25.00),
(9, '2024-09-28', 'Microphone', 1, 60.00),
(10, '2024-09-29', 'Noise-Canceling Headphones', 1, 200.00),
(10, '2024-09-30', 'Laptop Cooling Pad', 1, 30.00);


CREATE VIEW customer_orders AS
SELECT customers.first_name, customers.last_name, orders.order_id, orders.order_date
FROM customers
JOIN orders ON customers.customer_id = orders.customer_id;
```

A view `customer_orders` combina dados das tabelas `customers` e `orders` para mostrar os pedidos de cada cliente.

## Criação de Views Indexadas

```sql
CREATE VIEW indexed_customer_view AS
SELECT customer_id, first_name, last_name
FROM customers
WITH CHECK OPTION;
```

A view `indexed_customer_view` garante que qualquer modificação de dados respeite a condição definida na view, e é potencialmente indexável para melhorar a performance de consultas.

## Modificação de Views

```sql
ALTER VIEW texas_customers AS
SELECT first_name, last_name, city, state, zip_code
FROM customers
WHERE state = 'TX';
```

O comando acima altera a view `texas_customers` para incluir o código postal (`zip_code`) na exibição.

## Atualização de Tabelas Usando Views

```sql
UPDATE customer_emails
SET email = 'new.email@example.com'
WHERE first_name = 'Alice' AND last_name = 'Johnson';
```

Este comando atualiza o e-mail de um cliente através da view `customer_emails`.

## Exclusão de Views

```sql
DROP VIEW IF EXISTS customer_emails;
```

O comando acima exclui a view `customer_emails` se ela existir.

---
