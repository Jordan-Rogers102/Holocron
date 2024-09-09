> [!info]- Goal
> The goal of this tutorial is to:
> - Implement a simple 'mini' app into the flask project
> - Learn & implement CRUD operations
> - Gain evidence for [ICTICT226 - Operate Simple Database Applications](https://training.gov.au/Training/Details/ICTICT226).
> - ![todoDemo](/WebDev/_shared/Projects/ANH/images/todoDemo.gif)
# CRUD


![CRUD](/WebDev/_shared/Projects/ANH/images/todoCRUD.jpeg)

[https://www.atatus.com/glossary/crud/](https://www.atatus.com/glossary/crud/)

**Create**, **Read**, **Update** & **Delete** (CRUD) are the standard operations for use with databases, especially with SQL statements using a relational data system such as SQLite.

You can read more on CRUD by accessing [this page](https://www.humio.com/glossary/crud/).

In this exercise, you’ll demonstrate each of these processes with a simple ToDo application.

# Create the Database Table

In the database extension tab, click the `+` icon next to `Tables` to create a new table.

![todoNewTable](/WebDev/_shared/Projects/ANH/images/todoNewTable.png)

Name the table `todo`.

![todoTableName](/WebDev/_shared/Projects/ANH/images/todoTableName.png)

Update the SQL commands to specify the fields to create in the `todo` table.

![todoTableSQL](/WebDev/_shared/Projects/ANH/images/todoTableSQL.png)

```sql
CREATE TABLE todo(
	id INTEGER NOT NULL PRIMARY KEY AUTOINCREMENT,
	text TEXT,
	done BOOLEAN,
	userID INT
);
```

Press the run link to execute the SQL.

![todoTableExecute](/WebDev/_shared/Projects/ANH/images/todoTableExecute.png)

The table will now be created and will appear in the left-hand view.

![todoTableComplete](/WebDev/_shared/Projects/ANH/images/todoTableComplete.png)

# Create Model

Open `models.py`

At the end of the file, and after any other classes, add the following `todo` class.

 > [!info] Like with any other classes in this case, the names of the class and the variables need to match what the the names are in the database. If you’ve named them different, you will need to make them match.


![todoModelCreate](/WebDev/_shared/Projects/ANH/images/todoModelCreate.png)

```python
class todo (db.Model):
    id = db.Column(db.Integer, primary_key=True, autoincrement=True)
    text = db.Column(db.Text)
    done = db.Column(db.Boolean)
    userID = db.Column(db.Integer)
```

**Save** the file.

# Todo Template

Right click on the Templates folder and create a new HTML file called `todo.html`. 

![todoHTMLNew](/WebDev/_shared/Projects/ANH/images/todoHTMLNew.png)

Replace the contents with this standard code.

```python
{% extends "base.html" %}

{% block pageCSS %}
{% endblock %}

{% block rowOneContent %}
<h1>TODO List</h1>
{% endblock %}

{% block rowTwoColOneContent %}
{% endblock %}

{% block rowTwoColTwoContent %}
{% endblock %}

{% block rowThreeContent %}
<div class="footerText">Copyright 2024.</div>
{% endblock %}

```

Replace the sidebar (`rowTwoColOneContent`) with the code to create a new entry in the todo list.

![todoFormCode](/WebDev/_shared/Projects/ANH/images/todoFormCode.png)

```python
<form method="POST" action="/todo">
    <input type="text" name="text" placeholder="Add a new TODO item">
    <button type="submit" value="update">Create new Todo Entry</button>
</form>
```

Replace the `rowTwoColTwoContent`’s content with the following.

This code **loops** for each entry in the Todo list (how many rows are in the table). For each entry, it creates a checkbox to indicate in the task is done or not, and the text of the todo.

It also adds an Update button for each entry.

> [!example]- An example of what this code will create is:
> ![todoExampleList](/WebDev/_shared/Projects/ANH/images/todoExampleList.png)


![todoList](/WebDev/_shared/Projects/ANH/images/todoListCode.png)

```python
<h2>List</h2>
{% for todo in todos %}
    <p>
    <form method="POST" action="/todoedit/{{ todo.id }}">
        <input type="hidden" name="done" value="off">
        <input type="checkbox" onclick="redirect('/todoedit/{{ todo.id }}')" data-target="/todoedit/{{ todo.id }}" name="done">

        <input type="text" title="{{ todo.dateAdded }}" value="{{ todo.text }}" name="text" class="form-control">

        <button type="submit" value="update">Update</button>
    </form>
<form method="GET" action="/todoedit/{{ todo.id }}">
            <button type="submit" value="delete">Delete</button>
        </form>
{% endfor %}
```

**Save** the file.

# ‘Create Todo’ Route

Open `app.py` .

Update the following import. This allows this file to load and use the new class just created.

![todoImportTodo](/WebDev/_shared/Projects/ANH/images/todoImportTodo.png)

## View Todos

Create a new route by copying this code into `app.py.`

![todoAddRoute](/WebDev/_shared/Projects/ANH/images/todoAddRoute.png)

```python
@app.route('/todo', methods=["POST", "GET"])
def view_todo():
	all_todo = todo.query.filter_by(userID=current_user.id).all()
    if request.method == "POST":
        new_todo = todo(text=request.form['text'], done=False,userID=current_user.id)
        new_todo.done = False
        db.session.add(new_todo)
        db.session.commit()
        db.session.refresh(new_todo)
        return redirect("/todo")
    return render_template("todo.html", todos=all_todo, user=current_user)
```

### An Explanation for each line

| Line                                                                                                            | Explanation                                                                                                                                                                                                                                                                                                                     |
| --------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 47                                                                                                              | Creates the new route, called /todo and also adds the extra functionality of POST and GET methods. This means that this route will send data from the server to the browser (GET) and also accept data being sent back from the browser to the server (POST). POST is the common method to submit form data back to the server. |
| You can read more [https://pythonbasics.org/flask-http-methods/](https://pythonbasics.org/flask-http-methods/). |                                                                                                                                                                                                                                                                                                                                 |
| 48                                                                                                              | Defines the function name                                                                                                                                                                                                                                                                                                       |
| 49                                                                                                              | Queries the database and retrieves the records in the `todo` table which match the current users `userid`. The results are stored into the all_todo variable.                                                                                                                                                                   |
| 51                                                                                                              | Checks if the Create todo form in `rowTwoColOneContent` (or sidebar) is attempting to submit data back to the server (POST).                                                                                                                                                                                                    |
| 51                                                                                                              | Creates a new variable - new_todo by collecting the text entered in the form.                                                                                                                                                                                                                                                   |
| 52                                                                                                              | Sets the done field to False as default.                                                                                                                                                                                                                                                                                        |
| 53-55                                                                                                           | Writes the new entry into the database temporarily, and then commits it to the database permanently. The `refresh()` command updates the entry in memory to match the database.                                                                                                                                                 |
| 56                                                                                                              | After submitting the new ToDo entry to the database, this reloads the current page.                                                                                                                                                                                                                                             |
| 57                                                                                                              | “Sends” the template to the browser with all the notes loaded from the previous query on line 34.                                                                                                                                                                                                                               |



## Run and test the page.

Run the project and access the link:

[http://127.0.0.1:5000/todo](http://127.0.0.1:5000/todo)

You should see something similar to this:

![todoExample](/WebDev/_shared/Projects/ANH/images/todoExample.png)

Create a new Entry and reload the page.

![todoExampleCreateEntry](/WebDev/_shared/Projects/ANH/images/todoExampleCreateEntry.png)

# ‘Edit Todo’ Route

This route will handle both the update and delete functions.

Add the following route code to `app.py`

![todoEditRoute](/WebDev/_shared/Projects/ANH/images/todoEditRoute.png)

```python
@app.route("/todoedit/<todo_id>", methods=["POST", "GET"])
def edit_note(todo_id):
    if request.method == "POST":
        db.session.query(todo).filter_by(id=todo_id).update({
            "text": request.form['text'],
            "done": True if request.form['done'] == "on" else False
        })
        db.session.commit()
    elif request.method == "GET":
        db.session.query(todo).filter_by(id=todo_id).delete()
        db.session.commit()
    return redirect("/todo", code=302)
```

## Code explanation

| Line  | Explanation                                                                                                                                                                                                                                                                                                                                                                                  |
| ----- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 59-60 | Creates the route and python function. This is different from other routes as it accepts a variable in the route. <todo_id> is anything that is in the url after the /todoedit/ in the browser. For instance if the url is [http://127.0.0.1:5000/tododit/5](http://127.0.0.1:5000/tododit/5) then todo_id is 5. In this case, it will refer to the the entry in the table with 5 as the ID. |
| 61    | Checks if the form has been POSTed to the server. This will be True when the user submits the form in todo.html created by the line : <form method="POST" action="/todoedit/{{ [http://todo.id/](http://todo.id/) }}">                                                                                                                                                                       |
| 62-65 | This first queries the database to find the entry with the ID matching todo_id and updates it with the text in text field and the done field whether it is ticked or not.                                                                                                                                                                                                                    |
| 66    | Commits any changes to the database.                                                                                                                                                                                                                                                                                                                                                         |
| 67    | Checks if the form has been submitted using the GET method. This will be True when the user submits the form in todo.html created with the line: <form method="GET" action="/todoedit/{{ [http://todo.id/](http://todo.id/) }}">                                                                                                                                                             |
| 68    | Finds the entry in the database with the ID matching todo_id and deletes it.                                                                                                                                                                                                                                                                                                                 |
| 69    | Commits the change to the database.                                                                                                                                                                                                                                                                                                                                                          |
| 70    | redirects the browser to /todo after any changes have been made.                                                                                                                                                                                                                                                                                                                             |

---

# Navbar Update

Open base.html and add a new link to the TODO mini app.

![todoTemplateUpdate](/WebDev/_shared/Projects/ANH/images/todoTemplateUpdate.png)
```html
<a class="nav-link" href="/todo">ToDo List</a>
```

![[commonBlocks#Commit & Push]]

# VET Competency

This task, or parts of it, can be used towards **ICTICT210 - Operate database applications** competency.

[training.gov.au](https://training.gov.au/Training/Details/ICTICT210)