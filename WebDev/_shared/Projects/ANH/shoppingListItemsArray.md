>[!info]- Learning Outcome
>This page covers the complex nature of the multidimensional array produced by the `join` command used in Flask


# Arrays Overview

> [!info] This section provides a general overview and examples of arrays in Python and Flask. Used as background knowledge.


## Arrays and Multidimensional Arrays in Python and Flask

### Single-Dimensional Arrays

**Python**

Single-dimensional arrays in Python are simply lists. You can create a single-dimensional array using square brackets `[]`.

```python
fruits = ["apple", "banana", "cherry"]
```

You can access elements in the array using their index.

```python
print(fruits[0])  # Output: apple
```

You can also iterate over the array using a `for` loop.

```python
for fruit in fruits:
    print(fruit)
```

**Flask**

Flask provides a way to handle single-dimensional arrays as part of HTTP requests and responses. To receive a single-dimensional array from a client, you can use the `request.json` object.

```python
from flask import Flask, request

app = Flask(__name__)

@app.route('/array', methods=['POST'])
def receive_array():
    # Get the array from the request body
    array = request.json.get('array')

    # Process the array
    # ...

    return 'Success'
```

To send a single-dimensional array to a client, you can use the `jsonify()` function.

```python
from flask import Flask, jsonify

app = Flask(__name__)

@app.route('/array', methods=['GET'])
def send_array():
    # Create a single-dimensional array
    array = ["apple", "banana", "cherry"]

    # Send the array to the client
    return jsonify(array)
```

### Multidimensional Arrays

**Python**

Multidimensional arrays in Python are represented using nested lists. You can create a multidimensional array using square brackets `[]` and nested square brackets `[][]`.

```python
board = [['X', '.', '.'],
         ['.', 'O', '.'],
         ['.', '.', 'X']]
```

You can access elements in the array using their indices.

```python
print(board[0][0])  # Output: X
```

You can also iterate over the array using nested `for` loops.

```python
for row in board:
    for cell in row:
        print(cell)
```

**Flask**

Flask provides a way to handle multidimensional arrays as part of HTTP requests and responses. To receive a multidimensional array from a client, you can use the `request.json` object.

```python
from flask import Flask, request

app = Flask(__name__)

@app.route('/multi_array', methods=['POST'])
def receive_multi_array():
    # Get the multidimensional array from the request body
    array = request.json.get('array')

    # Process the array
    # ...

    return 'Success'
```

To send a multidimensional array to a client, you can use the `jsonify()` function.

```python
from flask import Flask, jsonify

app = Flask(__name__)

@app.route('/multi_array', methods=['GET'])
def send_multi_array():
    # Create a multidimensional array
    array = [['X', '.', '.'],
             ['.', 'O', '.'],
             ['.', '.', 'X']]

    # Send the array to the client
    return jsonify(array)
```

# SQL & Join Operations
> [!info] This section provides a general overview and examples of JOIN operations with SQL and Flask. Used as background knowledge.

**What is a JOIN Operation in SQL?**

JOIN is a powerful operation in SQL (Structured Query Language) that allows you to combine rows from two or more tables based on a common column or columns. It is used to retrieve data from multiple tables simultaneously and create more complex queries.

**How JOIN Works**

JOIN operations work by comparing the values in one or more columns of two tables. The rows that have matching values in the specified columns are then combined into a single result set.

**Types of JOIN Operations**

There are four main types of JOIN operations in SQL:

- **INNER JOIN:** Returns only the rows that match in both tables.
- **OUTER JOIN:** Returns all rows from one table and matching rows from another table.
- **LEFT OUTER JOIN:** Returns all rows from the left table and matching rows from the right table.
- **RIGHT OUTER JOIN:** Returns all rows from the right table and matching rows from the left table.

**Syntax**

The general syntax of a JOIN operation is:

```sql
SELECT *
FROM table1
JOIN table2
ON table1.column_name = table2.column_name;
```

In this syntax:

- `table1` and `table2` are the tables you want to join.
- `column_name` is the common column or columns used to join the tables.


## Join Example 

Consider the following two tables:

**Customers Table**

|customer_id|customer_name|
|---|---|
|1|John Smith|
|2|Jane Doe|
|3|Mark Johnson|

**Orders Table**

|order_id|customer_id|product_name|quantity|
|---|---|---|---|
|101|1|Laptop|1|
|102|2|Smartphone|2|
|103|3|Tablet|1|

**Example Join Operations**

**INNER JOIN**

```sql
SELECT *
FROM Customers
INNER JOIN Orders
ON Customers.customer_id = Orders.customer_id;
```

**Result:**

|customer_id|customer_name|order_id|product_name|quantity|
|---|---|---|---|---|
|1|John Smith|101|Laptop|1|
|2|Jane Doe|102|Smartphone|2|
|3|Mark Johnson|103|Tablet|1|

This query returns only the rows that match in both the Customers and Orders tables.

**OUTER JOIN**

```sql
SELECT *
FROM Customers
FULL OUTER JOIN Orders
ON Customers.customer_id = Orders.customer_id;
```

**Result:**

| customer_id | customer_name | order_id | product_name | quantity |
| ----------- | ------------- | -------- | ------------ | -------- |
| 1           | John Smith    | 101      | Laptop       | 1        |
| 2           | Jane Doe      | 102      | Smartphone   | 2        |
| 3           | Mark Johnson  | 103      | Tablet       | 1        |
| NULL        | NULL          | NULL     | NULL         | NULL     |

This query returns all rows from both the Customers and Orders tables, even if there are no matching rows. The NULL values represent rows that do not have a match in the other table.

**LEFT OUTER JOIN**

```sql
SELECT *
FROM Customers
LEFT OUTER JOIN Orders
ON Customers.customer_id = Orders.customer_id;
```

**Result:**

|customer_id|customer_name|order_id|product_name|quantity|
|---|---|---|---|---|
|1|John Smith|101|Laptop|1|
|2|Jane Doe|102|Smartphone|2|
|3|Mark Johnson|103|Tablet|1|
|NULL|NULL|NULL|NULL|NULL|

This query returns all rows from the Customers table, and matching rows from the Orders table. However, if there are no matching rows in the Orders table, the query returns a NULL value for the order information.

**RIGHT OUTER JOIN**

```sql
SELECT *
FROM Customers
RIGHT OUTER JOIN Orders
ON Customers.customer_id = Orders.customer_id;
```

**Result:**

|customer_id|customer_name|order_id|product_name|quantity|
|---|---|---|---|---|
|1|John Smith|101|Laptop|1|
|2|Jane Doe|102|Smartphone|2|
|3|Mark Johnson|103|Tablet|1|
|NULL|NULL|NULL|NULL|NULL|

This query returns all rows from the Orders table, and matching rows from the Customers table. However, if there are no matching rows in the Customers table, the query returns a NULL value for the customer information.


## Using JOIN Operations in Flask

To perform a JOIN operation in Flask, you can use the `join()` method of the `Query` object.

```python
from flask_sqlalchemy import SQLAlchemy

db = SQLAlchemy()

class Customer(db.Model):
    customer_id = db.Column(db.Integer, primary_key=True)
    name = db.Column(db.String(80))
    email = db.Column(db.String(120))

class Order(db.Model):
    order_id = db.Column(db.Integer, primary_key=True)
    customer_id = db.Column(db.Integer, db.ForeignKey('customer.customer_id'))
    product_id = db.Column(db.Integer)
    quantity = db.Column(db.Integer)

@app.route('/join')
def join():
    # Perform an INNER JOIN
    results = db.session.query(Customer, Order).join(Order, Customer.customer_id == Order.customer_id).all()

    # Process the results
    # ...

    return 'Success'
```

The `join()` method takes two arguments:

- The first argument is the table to join with.
- The second argument is the condition for joining the tables.

You can also use the `outerjoin()` method to perform LEFT, RIGHT, or FULL OUTER JOINs.

```python
# Perform a LEFT JOIN
results = db.session.query(Customer, Order) .outerjoin(Order, Customer.customer_id == Order.customer_id).all()
```



# Project Specific Information

In the Shopping List stage of the project, to display a shopping list to the user, including the items in the list and the item names, data needs to be retrieved from two different tables at the same time

## Database

The database, focusing on the shopping list sub-system, is visualised in the Entity Relationship Diagram (ERD) as:

![erdShoppingLists](/WebDev/_shared/Projects/ANH/images/erdShoppingLists.png)

This diagram describes:
- `shopping_lists` is linked to the `User` table through the `userID`->`id` fields connection.
- `shopping_list_items` link individual `shopping_item` entries to individual `shopping_lists`. 

**In summary:** To display an individual shopping list to the user, the list of items needs to be retrieved from `shopping_list_items` and each item's name needs to be retrieved from `shopping_item`. This requires a `join` operation on the database.

## Sample Database Data

Using the information above, and the sample data below, you can see that in the shopping_list_items table, the record with an ID of 4 matches the `shoppingListID` of 2 with the item with an ID of 5, named "Self Raising Flour" from the `shopping_item` table.

### `shopping_item`

| id  | name               |
| --- | ------------------ |
| 1   | Taco               |
| 2   | Cheese             |
| 3   | Bread              |
| 4   | Flour              |
| 5   | Self Raising Flour |
| 6   | Salsa              |
| 7   | Paprika            |
| 8   | Milk               |

### `shopping_list_items`

| id  | shoppingListID | shoppingItemID | quantity | completed |
| --- | -------------- | -------------- | -------- | --------- |
| 4   | 2              | 5              | 10       | 0         |
| 5   | 1              | 6              | 3        | 1         |

> [!important] **Goal:** The goal of JOIN operations is to load data from two different tables. In this case, load the item name (from `shopping_item`) and the list of items in a shopping list (from `shopping_list_items`)
> This means that when the list is shown, it would appear like this:
> ![joinExampleList](/WebDev/_shared/Projects/ANH/images/joinExampleList.png)
> So, showing "Self Raising Flour" Instead of showing the number 5

## Code explanation

The code that achieves this in the shopping list mini Web App can be found in the `shoppingList(list_id)` function.

```python
list_items = db.session.query(ShoppingListItems, ShoppingItem).join(ShoppingItem, ShoppingListItems.shoppingItemID == ShoppingItem.id).filter(ShoppingListItems.shoppingListID == list_id).all()
```

![joinCode](WebDev/_shared/Projects/ANH/images/joinCode.png)

This code is similar to the previous `db.session.query()` commands coded in the remainder of the project. 

The code identifies the two tables (via the models - `ShoppingListItems` and `ShoppingItem`) and runs the `join` command, linking the two tables through `ShoppingListItems.shoppingItemID` and `ShoppingItem.id`. 

The results from the join command is then `filter`ed by the shoppingListID so it only loads the data for the shopping list that is to be displayed (identified by `list_id`). 
