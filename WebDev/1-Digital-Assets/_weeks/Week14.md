$\color{black} \fcolorbox{lightgreen}{lightgreen} {Overview}$

The goals for this topic are:

- User Access Level
- Administrator Tools
    - Navbar updates
    - Reseting User Passwords
    - Disabling User Accounts

$\color{black} \fcolorbox{darkorange}{darkorange} {Table of Contents}$


$\color{black} \fcolorbox{lightblue}{lightblue} {Submission}$

In the Google Classroom Assignment, submit the following:

- Short video demonstrating functionality.

---

# Video

Watch the video/s supplied to understand the topics for this week.

[https://www.youtube.com/watch?v=c0CNZEAAOxw&ab_channel=RyanCather](https://www.youtube.com/watch?v=c0CNZEAAOxw&ab_channel=RyanCather)

---

# Resources

N/A

---

# Theory

N/A

---

# Practical Tasks

## Contact Messages Page

So far, users can send messages through the contact form, however the only way to view those messages is to access the database directly, which is not user-friendly and is a security issue. The next logical step is to build a page to dynamically load the table and display the messages to the user through the webpage.

## Route

Open `app.py` and create a new route.
![[week14ContactRoute.png]]



```python
@app.route('/contact_messages')
@login_required
def view_contact_messages():
```

Load all the entries in the contact table and store them in a variable.

> [!info]  The code `Contact.query.all()` reads the entire Contact table from the database and stores it in the `contact_messages` variable.



![[week14ContactQueryAll.png]]

```python
contact_messages = Contact.query.all()
```

Using this `contact_messages`, send the messages to a template page called `contactMessages.html`.

![[week14ContactTemplate.png]]


```python
return render_template("contactMessages.html", title="Contact Messages", user=current_user, messages=contact_messages)
```

## Contact Messages Template

Duplicate `index.html` and name the new file `contactMessages.html`.

To display the contact messages from the database, output the user's name, email address, message and the date it was submitted. This can be done using the bootstrap grid system as previously used.

Remove the contents of the `rowTwoColTwoContent` block and add the new `div`.
![[week14ContactTemplateContainer.png]]



```python
<div class="container-fluid">
        
</div>
```

To create a structure that will create as many rows as needed to display the whole table, the temples can dynamically create rows using a loop.

This **for** loop will iterate over the entries in `messages` (which is the `contact` table). Each time the loop iterates, it’s accessing a different record in the table.

> [!info]  The first time, it will be accessing the first entry in the table, the second time it will access the second entry etc.


![[week14ContactTemplateLoop.png]]

```python
<div class="container-fluid">
    {% for message in messages %}

    {% endfor %}
</div>
```

Each entry will be a row, so a new `div` tagged with `row` is needed inside the for loop.

![[week14ContactTemplateContainerRow.png]]

```html
<div class="row">

</div>
```

Output each of the fields in the record (except for the ID) in different columns.

![[week14ContactTemplateContainerRowFields.png]]

```html
<div class="col-3"> {{ message.name }}</div>
<div class="col-3"> {{ message.email }}</div>
<div class="col-3"> {{ message.message }}</div>
<div class="col-3"> {{ message.dateSubmitted }}</div>
```

## Test the route

Run the site and login. Modify the URL by adding `/contact_messages` to the end.

You should see a page similar to this (with different messages).

![[week14ContactDemo.png]]

## Extension

The Date Submitted output isn’t very user-friendly. How could this be improved?

> [!info]- Answer
Update `contactMessages.html` to change how the date is outputed by placing `.strftime('%H:%M - %d/%m/%Y')` after the `datetime` output.
![[week14ContactTemplateTimeFix.png]]

How could the administrator control which messages they’ve seen or responded to? What would need to be added to the database and webpage?

## User Access Level

So far in the development process, there is very little access control.

> [!info]  Access control is the term to cover which users can access certain pages and other resources.


A Quick Summary of what is implemented so far:

- In the User table in the database, there is a `user_level` field, which is defined as an integer.
- A 1 in this field means standard user. A 2 means the user is an administrator.
- The User model has a function - `is_admin()` - which will return `True` if the user_level is set to 2.
- Some routes have `@login_required` defined which requires the user to be logged in or will redirect the user to the login page.
![[week14UserAccessLevel.png]]

This is not _great_ security and can use a lot of work.

Ideally, only Administrators will be able to access certain pages of the website, and standard users will be redirected if they attempt to access those resources.

For instance, only administrators should be able to view all the messages on the [Contact Messages](https://www.notion.so/Contact-Messages-727997aeeb73406a91fb930af1d5a6cd?pvs=21) Page. Currently, **any** logged-in user can view that page (if they know the link)

## Update Contact Messages Route

Open `app.py` and find the `contact_messsages` route.

![[week14ContactRouteUpdateStart.png]]


To implement access control, before the Contact table is loaded and the template is rendered, first implement an `if` statement to check to see if the current user is an admin.

If the user is an administrator (level 2) then the page will load as it did previously.

![[week14ContactRouteCheckAdmin.png]]



```python
if current_user.is_admin():
```

Include an `else` clause to redirect the user to the home page if they are not an administrator.

![[week14ContactRouteAdminElse.png]]


```python
else:
    return redirect(url_for("homepage"))
```

## Update the Navbar

The `is_admin()` function can also be used in the base template to control which links administrators see vs regular users.

Currently there is a check to see if the current_user is logged in or not and displays the relevant links.

Add in a check to see if the user is an admin, and if so, show the link to the contact messages route.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/8b184e85-619e-4821-953f-43ab6c909423/548013ef-02ce-4118-bcde-e05455597bcd/Untitled.png)

## Test the implementation

Try to view the site as a regular user and then and administrator.

To change the access level, you’ll need to view the User table, change the value in the `user_level` field and write the changes back to the database.

Attempt to access the URL without logging in, and it should redirect you to the login page.

Attempt to access the URL logged in as a user with an access level set to 1.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/8b184e85-619e-4821-953f-43ab6c909423/6d66212a-9ec5-4377-85b9-622c3e41e864/Untitled.png)

Attempt to access the URL logged in as a user with an access level set to 2.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/8b184e85-619e-4821-953f-43ab6c909423/955c79e7-946b-4570-ac52-4fda59c3e44a/Untitled.png)

## Continue Implementing Access Control

What other pages should be limited to administrators only? Any that need to be, just add the same structure as was implemented for the contact messages route:

```python
if current_user.is_admin():
	# Normal Route code. For administrators only.
else:
    return redirect(url_for("homepage"))
```

## Administrator Tools

This section of the project focuses on Administrator functionality.

It is _generally_ a bad idea to allow anyone, apart from a core group of people, direct access to the database, which means that most functions need to be configured to be allowed through a web interface.

Administrator functionality that would require a web interface could be:

- Resetting other users passwords
- Removing or disabling user accounts
- Removing or disabling photos uploaded
- etc.

## Navbar updates

Update the navbar component in `base.html` to add links to the administrator functionality.

Look for the `{% if user.is_admin() %}` code and replace the existing links to be a dropdown menu.

![[week14TemplateNavbarAdmin.png]]

```html
<li><a class="nav-link" href="/contact_messages">Contact Messages</a></li>
<li><a class="nav-link" href="/admin/list_all_users">List all Users</a></li>
```

## Reseting User Passwords

## Listing All Users

To be able to access individual users to reset their passwords, a new route can be added to list all the users current in the system and providing a link to the direct url, such as : [http://127.0.0.1:5000/reset_password/6](http://127.0.0.1:5000/reset_password/6)

Before creating the route code, create the structure for the HTML template to load.

Create a new HTML file in the templates folder called `listAllUsers.html` and include the following code.

```python
{% extends 'base.html' %}

{# Place the content for the cellContent1 in this block #}
{% block rowOneContent %}

{% endblock %}

{% block rowTwoColOneContent %}
  
{% endblock %}

{# Place the content for the cellContent2 in this block #}
{% block rowTwoColTwoContent %}
  
{% endblock %}

{% block rowThreeContent %}
  <div class="footerText">Copyright 2024.</div>
{% endblock %}
```

In the `rowTwoColTwoContent` block add the code to loop over the number of users given, and automatically generating URLs for the reset password functionality defined below.

Save the file.

![[week14ListUsers.png]]

```html
<div class="container-fluid">
    {% for user in users %}
        <div class="row">
            <div class="col-md-4">{{ user.email_address }}</div>
            <div class="col-md-4"><a href="/reset_password/{{ user.id }}">Reset Password</a></div>
        </div>
    {% endfor %}
</div>
```

Open `app.py` and Start by defining the route.

![[week14UserListRoute.png]]

```python
@app.route('/admin/list_all_users')
@login_required
def list_all_users():
```

The code to load all the user details is simple enough, querying the entire user table, however this route needs to be limited so that only administrators can access it. If a user accesses it who is **not** an administrator, it will redirect them back to the front page.

![[week14UserListAdminCheck.png]]


```python
if current_user.is_admin():
    all_users = User.query.all()
    return render_template("listAllUsers.html", title="All Active Users", user=current_user, users=all_users)
else:
    flash("You must be an administrator to access this functionality.")
    return redirect(url_for("homepage"))
```

When the site is run and the url accessed, the administrator will see a page similar to this:

![[week14UserListAdminDemo.png]]



## Reset User Password Route

The site already allows for the user to reset their own password. The process for administrators to reset other peoples passwords is very similar.


To allow administrators to reset other peoples passwords, you can reuse `ResetPasswordForm` and the majority of the code shown with slight tweaks. The main one of these tweaks is the addition of the `userid` as a variable in the route and the function.

Enter the function in `app.py`.

```python
@app.route('/reset_password/<userid>', methods=['GET', 'POST'])
@login_required
def reset_user_password(userid):
    form = ResetPasswordForm()
    user = User.query.filter_by(id=userid).first()
    if form.validate_on_submit():
        user.set_password(form.new_password.data)
        db.session.commit()
        flash('Password has been reset for user {}'.format(user.name))
        return redirect(url_for('homepage'))
    return render_template("passwordreset.html", title='Reset Password', form=form, user=user)
```

The differences between the existing reset password route and this one can be seen here.

![[week14AdminResetPasswordRoute.png]]



Notice the `/reset_password/<userid>` in the route and `reset_user_password(userid)` in the function header. This allows for the browser to access a URL such as [http://127.0.0.1:5000/reset_password/6](http://127.0.0.1:5000/reset_password/6). Where the `6` indicates the user id to be accessed as can be seen below.

![[week14ResetPasswordAdminDB.png]]

Additionally, the User.query code has been moved to be run before the if statement. This is so that the user details can be loaded to display on screen (as indicated in the render_template code with `user=user`). This allows the intended users email address to be shown instead of the `current_user` details.

Test the functionality to ensure it works.

> [!info] It may be useful to register a test account to practice the resetting of passwords on.


## Disabling User Accounts

User accounts can be disabled or deleted for any number of reasons - an account could have been made in error, legal issues, or the user just wishes to get rid of the account for some reason. Whatever the reason, it may be better to _disable_ the account rather than delete it.

To enable the disabling of accounts will require a few changes throughout the system:

1. The Login process needs to only allow users to login with active accounts.
2. User Registration needs to default active to true.
3. Administrators need to be able to enable and disable accounts as needed.

There may be other changes required, however these are the main ones.


> [!important] The Database and model already has support for enabling and disabling of user accounts through the `active` field.

### Login

The login process does not need to be changed significantly - the only addition is a check to ensure the user account is active (the field is `1`) before the login process proceeds.

This is only a minor change to the existing code.

> [!info]  It would be useful to add a flash message to the user if the login process fails, instead of just redirecting them back to the user page.


![[week14UserNotActive.png]]



### Administrator Control

To allow administrators to enable and disable user accounts, there are a number of approaches to take.

**One** easy method is to update the `listAllUsers.html` file to show if the account is enabled or disabled, and to generate a link to flip the account status (enabled→disabled or disabled→enabled).

Save the file.
![[week14TemplateCheckUserActive.png]]


```html
<div class="col-md-3">
    {% if user.active %}
        Enabled
    {% else %}
        Disabled
    {% endif %}
</div>
<div class="col-md-3"><a href="/admin/user_enable/{{ user.id }}">Enable/Disable Account</a></div>
```

Open [`app.py`](http://app.py) and create a new route for `/admin/user_enable`

This route loads the user identified by their user id, then flips the status. The changes are written back to the database.

Notice that this route doesn’t display a template to the user, just redirects them back to the `list_add_users` route. The user performing this function will see the changes reflect in the user list.

![[week14AdminDisableUser.png]]


```python
@app.route('/admin/user_enable/<userid>')
@login_required
def user_enable(userid):
    user = User.query.filter_by(id=userid).first()
    user.active = not user.active
    db.session.commit()
    return redirect(url_for("list_all_users"))
```

### Extension

Update the `user_enable` route to limit access to administrators only.

Hint: Look at the `list_all_users` route for suggestions.

Open `models.py` and add a new variable to the `User` class to reflect the new addition to the database.

> [!info] Create an account to test the process - check the database to ensure that the new account has been created correctly.


Similarly to login, the registration process only needs a small addition to make the account active by default.

---

# Additional Information

---

# Vet Competencies

This week, the following VET competencies are being being addressed. Please enter the relevant details in your supplied VET competency documentation.

## Core

|Code|Title|
|---|---|
|BSBSUS211|Participate in sustainable work practices|
|BSBTEC202|Use digital technologies to communicate in a work environment|
|BSBWHS211|Contribute to the health and safety of self and others|
|ICTICT213|Use computer operating systems and hardware|
|ICTICT214|Operate application software packages|
|ICTICT215|Operate digital media technology packages|

## Electives

|Code|Title|
|---|---|
|CUADIG201|Maintain interactive content|
|CUADIG202|Develop digital imaging skills|
|ICTICT206|Install software applications|
|ICTICT207|Integrate commercial computing packages|
|ICTICT210|Operate database applications|
|ICTICT216|Design and create basic organisational documents|
|ICTICT219|Interact and resolve queries with ICT clients|
|ICTICT221|Identify and use specific industry standard technologies|
|ICTICT222|Research and share ICT solutions for Indigenous users|
|ICTSAS203|Connect hardware peripherals|
|ICTSAS211|Develop solutions for basic ICT malfunctions and problems|
|ICTWEB306|Develop web presence using social media|
|BSBTWK201|Work effectively with others|
|BSBTEC303|Create electronic presentations|
