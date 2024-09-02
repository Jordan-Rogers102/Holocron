> [!info]- Goal
> The goal of this part of the project is the implementation of a shopping list where users can add and remove items. Users will be able to create and manage different shopping lists for their own purposes (such as "Dinner Party" and "Weekly Items")

This stage of the mini web app is the foundations:
- Database Tables
- Models
- Forms


# Database Tables

Using the skills developed in previous sections, create the following tables in the database:
1. `shopping_lists`
2. `shopping_items`
3. `shopping_list_items`

These tables need to be separated to keep the data stored effectively. `shopping_list_items` links the other two tables together.

**Example**

![shoppingListDatabaseExample](/WebDev/_shared/Projects/ANH/images/shoppingListDatabaseExample.png)

## `shopping_lists`

> [!info] This table will hold the shopping list names and which user they belong to.

Create the table with the following fields. 

| Field  | Data Type                        |
| ------ | -------------------------------- |
| id     | int, auto increment, primary key |
| name   | TEXT                             |
| userID | INTEGER                          |

## `shopping_item`

> [!info] This table will hold the individual shopping list items, such as "Bread", and "Milk"

Create the table with the following fields.

| Field | Data Type                        |
| ----- | -------------------------------- |
| id    | int, auto increment, primary key |
| name  | TEXT                             |

## `shopping_list_items`
> [!info] This table will list the items that are associated with which shopping Lists.

Create the table with the following fields.

| Field          | Data Type                        |
| -------------- | -------------------------------- |
| id             | int, auto increment, primary key |
| shoppingListID | INTEGER                          |
| shoppingItemID | INTEGER<br>                      |
| quantity       | INTEGER                          |
| complete       | BOOLEAN                          |

# Models

Open `models.py` and create the three new classes to match the database tables just created.

![shoppingListModel](/WebDev/_shared/Projects/ANH/images/shoppingListModel.png)

Save the file.

# Forms

Open `forms.py` and create the forms required for to create (and potentially edit) the shopping list, the items and which items belong to which shopping list.

When designing these forms, consider the user experience. Ideally the process would be something similar to:

1. User creates a shopping list (with a form)
2. User clicks on the shopping list.
3. User adds shopping list items to the list.

Step 3 of this process would include adding the individual items to the `shopping_item` table and adding an entry to the `shopping_list_items` table linking the individual item to the shopping list.


Save the file.


Commit and push your changes!

