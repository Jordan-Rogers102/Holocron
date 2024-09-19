>[!info]- Goal
>This week we will be enabling A New Hope to be able to add items to the shopping lists and also to be able to tick items off of the shopping lists so they read as completed.

# Previous Week Section

If you struggled last week here is a very simple breakdown of the completed code.

## Templates

We added a new template to our template folder that scaffolded a new webpage where users could create their shopping lists. We needed to add in a form to the left column so that names of shopping lists could be inputted and then we needed to add a display for the shopping lists in the database:

![shoppingListTemplate1](/WebDev/_shared/Projects/ANH/images/shoppingListTemplate1.png)

![shoppingListTemplate2](/WebDev/_shared/Projects/ANH/images/shoppingListTemplate2.png)

## app.py

app.py needed to be updated to include a new `route` with the right  methods that could `GET` the data contained in the `shoppingLists` table so it can be displayed as well as `POST` the inputted named to the table to create new shopping lists.

![shoppingListRoute](/WebDev/_shared/Projects/ANH/images/shoppingListRoute.png)


# Week 9 Tasks

In this week we are trying to allow for the user to be able to go into their shopping lists and add items to the lists.
We have already created the tables for these shopping lists to include the creation and addition of items back in week 7  ([[/WebDev/_shared/Projects/ANH/shoppingListPart1|shoppingListPart1]])
In the same way when we added in the `shoppingList.html` template we need to create a new template and then add functionality to `app.py` so that that page can add items to our shopping lists.

## Template

Same as before we are adding a new webpage so we need to add a new template. 

Make a new template called `shoppingList.html`

Replace the standard with the following

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

Now edit `{% block rowTwoColOneContent %}` to add a form that will allow a new item to be added to the current shopping list.

>[!info]- Hint
>The user needs to be able to input both the items name and the quantity of that item for this list

Also edit `{% block rowTwoColTwoContent %}` to display the items in the shopping list that is currently open.

>[!info]- Hint
>Once implemented the webpage should look something like (remember you still need to add functionality to `app.y` before it will be able to add items to the lists and show those items in `{% block rowTwoColTwoContent %}`):
>![list example](/WebDev/_shared/Projects/ANH/images/shoppingListItemExample1.png)


## app.py

Open `app.py` 

Add a new `route` that will have `GET` and `POST` methods.
- You will need to define the route with a name like `shoppingList`
- You will need to query the database. We will need to retrieve the name of the item that needs to be displayed as well as the quantity of that item. Store this data in a variable you could name `list_items`. REMEMBER:
	- This needs to match the current `userid`
	- This query will need to `join` and `filter` syntax as we are querying from two different tables in our database
	- ![shoppingListDataSLexample](/WebDev/_shared/Projects/ANH/images/shoppingListDataSLexample.png)
	- You will also need a `query` for the list name as well
- You will need an if statement to determine if you are using `GET` or `POST`
	- `POST` needs to take the new data input in the forms from `{% block rowTwoColOneContent %}` and then:
		- `add()` the data
		- `committ()` the data
		- <strong><em>This will need to be done for the name AND the quantity</em></strong>
	- `GET` needs to use `return render template()` to constantly to constantly output the `shopping_list` template.

for Route the the list_items = db.session. (advise students that explaining this line in their reports is a high order thinking prompt, this will get you good marks. The join part is )

## Ticking off items

The last capability we want to add is to allow A New Hope to be able to tick whether or not certain items have been purchased from the shopping list and to also be able to remove items from the shopping list entirely.

### Template changes

First things first we need to adjust our web page template `shoppingList.html` in order to add clickable symbols that trigger `routes` in app.py. This will go in `{% block rowTwoColTwoContent %}`.

There should be three total symbols but only 2 should display at a time. 
The first will either be a Tick of a Cross so that the Cross is displayed if the `Completed` column in the `Shopping List Items` table is set to false indicating that the item has not been completed yet.
	Use an if statement to have this alternate between a Cross and a Tick to show whether or not the item has been completed.
	Clicking the cross of the tick should trigger a `route` that changes the `Completed` column in the `Shopping List Items` table to true if false or false if true.
The last symbol should be a Bin and trigger a `route` upon clicking that deletes the item.

The `routes` that these symbols call will be covered in the next section.

>[!info]- Hint
>The page should look something like this once the next section if completed.
>it won't work fully until the changes to `app.y` have been implemented
>If these red crosses are clicked the Boolean value `Completed` will change and the red cross will change to a green tick.
>If the bin is clicked the item will be removed from the shopping list all together
>![shoppingListItemExample2](/WebDev/_shared/Projects/ANH/images/shoppingListItemExample2.png)


### app.py

We need 2 new `routes` in `app.py`:

The first will change the `complete` boolean from the `Shopping List Items` from 1 to 0 or 0 to 1.
	Remember how you created all of your routes in the past
	The route will need to extract the `ID` value from the 1 `Shopping List Items` table by querying the `Shopping List Items` table and assigning a variable to the `ID`
	Then use the variable you've created to change the boolean `Completed` column in that particular `ID`
	`commit()` these changes

The second will remove the shopping list item from the database entirely.
	Same as before we need to extract the `ID` of the particular item in the `Shopping List Items` table so that we know which item we are affecting.
	We will need to `delete()` the item from the table
	`commit()` the changes

Remember that at the end of both of these `routes` we need to `return.redirect(url_for())` to reload the same page again with the updated information.

>[!info]- Hint
>Ensure that these routes have names that are called by the symbols. SPELLING MATTERS A LOT HERE. CAP SENSITIVE
>

For extension. Will need another column in the table that is enabled/disable and determines if the item is displayed
![](/WebDev/_shared/Projects/ANH/images/pin.png)