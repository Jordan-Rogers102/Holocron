>[!info]- Goal
>The aim of this weeks work is to enable ANH to allow for new shopping lists to be created. We have already created the databases, models, and forms for the shopping lists and even shopping list items to be C.R.U.D(ed) now the templates need to be made for the website to function and app.py needs to be updated



# Previous Weeks Solution

If you struggled with the creation of the tables, model and forms, use the code in this section to create.

## Database Tables

The below code should have been added to the `SQL` database

```sql
CREATE TABLE shopping_lists(  
    id INTEGER NOT NULL PRIMARY KEY AUTOINCREMENT,
    name TEXT NOT NULL,
    userID INTEGER NOT NULL
);

CREATE TABLE shopping_item(  
    id INTEGER NOT NULL PRIMARY KEY AUTOINCREMENT,
    name TEXT NOT NULL
);

CREATE TABLE shopping_list_items(  
    id INTEGER NOT NULL PRIMARY KEY AUTOINCREMENT,
    shoppingListID INTEGER NOT NULL,
    shoppingItemID INTEGER NOT NULL,
    quantity INTEGER NOT NULL,
    completed BOOLEAN NOT NULL
);
```

Your database should create the tables shown:

![shoppingListDB](/WebDev/_shared/Projects/ANH/images/shoppingListDB.png)



## `models.py`

These should have been added to `models.py` 

```python
class ShoppingLists(db.Model):
    id = db.Column(db.Integer, primary_key=True, autoincrement=True)
    userID = db.Column(db.Integer)
    name = db.Column(db.String(255))

class ShoppingItem(db.Model):
    id = db.Column(db.Integer, primary_key=True, autoincrement=True)
    name = db.Column(db.String(255))

class ShoppingListItems(db.Model):
    id = db.Column(db.Integer, primary_key=True, autoincrement=True)
    shoppingListID = db.Column(db.Integer)
    shoppingItemID = db.Column(db.Integer)
    quantity = db.Column(db.Integer)
    complete = db.Column(db.Boolean)

```

## forms

These two class forms should have been added into `forms.py` to determine what data fields need can be gathered from user input

```python
class ShoppingListForm(FlaskForm):
    name = StringField("Name", validators=[DataRequired()])
    submit = SubmitField("Submit List")

class ShoppingListItemForm(FlaskForm):
    item_name = StringField("Item Name", validators=[DataRequired()])
    submit = SubmitField("Submit Item")
```

When all of this has been implemented correctly. You should find a table in your database with these parameters. Note: yours won't have any data inside yet

![](WebDev/_shared/Projects/ANH/images/shoppingListDataTable.png)

# This week focus

Now that ANH has the correct databases, models, and forms for the shopping lists we need to create templates and edit the website so that new shopping lists can be made

# Templates

Create a new template called  `shoppingLists.html`

Replace the standard code with the following 

```jinja2
{% extends "base.html" %}

{% block pageCSS %}
{% endblock %}

{% block rowOneContent %}
<h1>SHOPPING List</h1>
{% endblock %}

{% block rowTwoColOneContent %}
{% endblock %}

{% block rowTwoColTwoContent %}
{% endblock %}

{% block rowThreeContent %}
<div class="footerText">Copyright 2024.</div>
{% endblock %}
```

Now implement code into `{% block rowTwoColOneContent %}` and `{% block rowTwoColTwoContent %}` that will allow for new Shopping lists to be made.

>[!info]- Hint 1
>You have done something very similar before when making the TODO list to display the forms and the data. Utilise similar syntax. Syntax will need adjustments for Shopping List (copy pasting the TODO code won't work)
>The only information users should be inputting for the `<form>` is the shopping lists `name` 

>[!info]- Hint 2
>Once implemented your webpage should look something like this (you may not be able to see this until the app.py is changed later on in these instructions but this image should show you how it needs to be coded in html):
![](WebDev/_shared/Projects/ANH/images/shoppingListInputExample.png)
>>`{% block rowTwoColOneContent %}` is in Green
>`{% block rowTwoColTwoContent %}` is in Red

Also make sure you add a link to this new page to `base.html`
![](WebDev/_shared/Projects/ANH/images/shoppingListBaseUpdateExample.png)

``` html
<a class="nav-link" href="/shoppingLists">Shopping Lists</a>
``` 

# app.py

Open `app.py` 
Add `ShoppingListForm, ShoppingListItemForm` under `from forms import`
Add `ShoppingLists, ShoppingListItems, ShoppingItem` under `from models import`

This allows this file to load and use the new class just created.

Create a new `route` in `app.py` for `shoppingLists`

Remember when creating a new route we want to:
- Tell the route what `methods` the page can use (`GET` and `POST`)
- Define the route with a name like `view_shoppingLists`
- Query the database and retrieves the records in the `shopping_lists` table which match the current users `userid`. The route will store these results in a variable you could name `all_shopping_lists`
- We need an if statement that will determine whether the route is GETting or POSTing
	- If it's POSTing the route needs to:
		- Create a new variable (maybe called `new_shopping_list`) based on the text entered in the form
		- `add()` new entry into the database system temporarily
		- `commit()` to the database permanently
		- `return redirect()` to reload the page with the new shopping list added
	- For GETting the route should be using:
		- `return render template()` to constantly to constantly output the `shopping_list` template.

<strong>Please remember if you need any help 

>[!info]- Hint 1
>There are many routes already in `app.py` that do similar but slightly different things. Use those alongside these instructions to figure out the code.

![](WebDev/_shared/Projects/ANH/images/pin.png)