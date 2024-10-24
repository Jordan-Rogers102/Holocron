$\color{black} \fcolorbox{lightgreen}{lightgreen} {Overview}$

The goals for this topic are:

- User eXperience (UX) Updates including:
    - Flash Messages
    - Error Handling
    - Current User
    - Navbar Updates

<aside> <img src="/icons/list_orange.svg" alt="/icons/list_orange.svg" width="40px" /> $\utilde {\color{black} \fcolorbox{darkorange}{darkorange} {Table of Contents}}$

</aside>

$\color{black} \fcolorbox{lightblue}{lightblue} {Submission}$

In the Google Classroom Assignment, submit the following:

- Record video of functionality implemented

---

# Video

Watch the video/s supplied to understand the topics for this week.

[https://youtu.be/9Rq9TR5569I](https://youtu.be/9Rq9TR5569I)

---

# Resources

N/A

---

# Theory

N/A

---

# Practical Tasks

## Flash Messages

Messaging is important to any User Interface - users need feedback to confirm if operations have been successful or not.

**Flash** is a addon module for Flask which allows for messages to be sent back to the user. The message is only valid for the _next_ page displayed that contains a flash block.

Luckily the project being built allows for a easy implementation of a flash message system. The template.html can be updated to display any flash messages, and existing routes can add in confirmation messages with a single line of code.

# Import flash

Open `app.py` and add `flash` to the `from flask import….` line of code.

![Screen Shot 2022-08-09 at 9.50.41 am.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7d194475-45c8-4b39-b37a-f3d097bdc197/Screen_Shot_2022-08-09_at_9.50.41_am.png)

# Update Routes

Update routes where feedback is important to the user. For instance, the password reset route. It would be useful for the user to get confirmation that the password has been changed.

To add a flash message, the command is: `flash("Message")`.

<aside> ‼️ As a rule of thumb, add the flash statements near the end of the process but before any return statement, as shown here.

</aside>

![Screen Shot 2022-08-09 at 9.52.45 am.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a35e6c61-1a91-4e5b-a815-460b6aedd3a4/Screen_Shot_2022-08-09_at_9.52.45_am.png)

Add appropriate messages to other routes, such as `loggout`, `contact`, and `User Registration`.

$\utilde {\color{black} \fcolorbox{darkorange}{darkorange} {Commit and Push to Github}}$

# Update Template

Open `templates/base.html` and decide where you want the messages to appear. They could appear just under the navbar, or in another specific place on the website. It is up to you where they will appear.

Wherever the messages are to appear in your code, add the following code block.

```
{% with messages = get_flashed_messages() %}
    {% if messages %}
        <ul class="flashes">
            {% for message in messages %}
                <li><div class="focus">{{ message }}</div></li>
            {% endfor %}
        </ul>
    {% endif %}
{% endwith %}
```

<aside> ‼️ Make sure you don’t put your message output into a block that will be overridden.

</aside>

This example shows that messages will appears just below the navbar.

![Screen Shot 2022-08-09 at 10.18.13 am.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b94bf635-9bac-4aa8-83bf-94c7936cee72/Screen_Shot_2022-08-09_at_10.18.13_am.png)

# Flash CSS

Currently, the messages appear very simply, as a dot list. Ideally the messages need to draw the users attention, so should stand out.

Open `static/site.css` and add the following CSS

```css
.flashes {
    color: red;
    list-style: none
}
```

Test out a flash message and you should see it appear similar to the one shown.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/8b184e85-619e-4821-953f-43ab6c909423/172a54bf-0857-48b2-abe2-adba43c99dad/Untitled.png)

You can expand on this CSS to make the messages stand out even more by updating the CSS, as shown here.

Modify the CSS to make the messages appear the way you wish to.

<aside> 💡 Find CSS code on the web, or use generative AI, to assist you.

</aside>

```css
.flashes {
    padding: 12px;
    border-radius: 3px;
    font-size: 1.2rem;
    margin-bottom: 16px;
    border: 2px solid orange;
    background-color: yellow;
    color: black;
}
```

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/8b184e85-619e-4821-953f-43ab6c909423/559f6c6a-9754-48c0-8144-a017063c8cd6/Untitled.png)

# Demonstration

![2022-08-09 10-19-24.2022-08-09 10_22_39.gif](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b0a8e258-d62d-487c-b66b-da807547bde8/2022-08-09_10-19-24.2022-08-09_10_22_39.gif)

## Error Handling

# Errors!

By this stage of the development process, this screen may be familiar to you.

There are a number of issues with this page.

1. There’s an error in the code that needs to be fixed.
2. The user doesn’t get any information to help them solve the problem.
3. The user loses confidence in the website as the site ‘is broken’.

It is possible to build custom ‘error’ pages to keep the user ‘within’ the website and allow them to continue using the site.

![Screen Shot 2022-08-09 at 10.44.41 am.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b1306bac-1d9a-4f1c-b6c1-d6bdbeb3ecaf/Screen_Shot_2022-08-09_at_10.44.41_am.png)

# HTML Pages

Create a html page in the templates folder called `500.html`. Include the default code for the website:

```html
{% extends 'base.html' %}

{# Place the content for the cellContent1 in this block #}
{% block rowTwoColOneContent %}
    Sidebar
{% endblock %}

{# Place the content for the cellContent2 in this block #}
{% block rowTwoColTwoContent %}

{% endblock %}

{# Place the content for the cellContent3 in this block #}
{% block cellContent3 %}
    Footer
{% endblock %}
```

In `cellContent2`, add a message to the user to indicate that there is a problem, but in a more user friendly way than the example above.

<aside> ‼️ Consider what the user would want to see on this page.

</aside>

![Screen Shot 2022-08-09 at 10.51.28 am.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6d9561b9-7474-473b-9ad8-66195cf6f185/Screen_Shot_2022-08-09_at_10.51.28_am.png)

You can choose how you want the messages to display. Using Bootstraps built-in Alerts can be a quick and easy solution, such as:

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/8b184e85-619e-4821-953f-43ab6c909423/152e2687-affb-4225-891e-ad06e147b5f3/Untitled.png)

```html
<div class="alert alert-danger" role="alert">
  File Not Found!
</div>
```

Repeat this process for a `404.html` error page for if the page doesn’t exist.

# Error Handlers

Open `app.py` and add the following routes.

<aside> 💡 These routes capture any `404` or `500` HTTP errors and instead of showing the standard error for the browser, it will show a custom built error, using based on the template. From a UX point of view, this ‘keeps’ the user within the site and can allow them to rectify the error by returning to other pages.

- 404 error - Not Found
- 500 error - Internal Server Error

You can find information on HTTP errors here: [https://developer.mozilla.org/en-US/docs/Web/HTTP/Status](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)

</aside>

```python
# Error Handlers
@app.errorhandler(404)
def page_not_found(e):
    return render_template("404.html", user=current_user), 404

@app.errorhandler(500)
def internal_server_error(e):
    return render_template("500.html", user=current_user), 500
```

# Test the site!

Run the project and attempt to access a page that doesn’t exist. Make sure the custom error page loads.

![Screen Shot 2022-08-09 at 10.55.44 am.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6ea2df3a-9cfc-4130-a1e6-d95508d9c0f2/Screen_Shot_2022-08-09_at_10.55.44_am.png)

To force the page to load correctly, you may need to **turn off** the FLASK_DEBUG setting. To do so, click on Edit Configurations under the Flask ([app.py](http://app.py)) dropdown.

![Screen Shot 2022-09-05 at 9.16.43 am.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/964bdc8a-8df0-48e8-83b9-edb96fb728da/Screen_Shot_2022-09-05_at_9.16.43_am.png)

Uncheck the box, and click ok.

![Screen Shot 2022-09-05 at 9.17.34 am.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/770623b4-6750-4447-b5db-44e89baab168/Screen_Shot_2022-09-05_at_9.17.34_am.png)

Then, in `index.html` comment out the last line of code to force an error.

![Screen Shot 2022-09-05 at 9.18.34 am.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a5f0e182-bf7a-4c39-a639-3f88142b9d72/Screen_Shot_2022-09-05_at_9.18.34_am.png)

Rerun the site and the 500 error page should appear.

# Example error pages

![pMGfBE5gnyuzxa6BGKAi3Q-970-80.jpg.webp](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/115cde18-ac5d-4fbd-9fb6-80f8a7b5baa8/pMGfBE5gnyuzxa6BGKAi3Q-970-80.jpg.webp)

![mYKbf3DSinvWnEzmHkEnCE-970-80.jpg.webp](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/428d83ef-79cb-487e-96f3-79288a7b055d/mYKbf3DSinvWnEzmHkEnCE-970-80.jpg.webp)

![pbtqaZH7Q9QcrVDnuJomQT-970-80.jpg.webp](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ce00eda7-e74c-4f36-b6f2-f00d630d1e9e/pbtqaZH7Q9QcrVDnuJomQT-970-80.jpg.webp)

## Current User Variable

Flask has a built-in variable called `current_user`. This variable stores the instance of the user that is currently logged in, for instance, their username, password_hash etc. But also has access to any custom functions written for the User model, such as `is_admin().`

This is incredibly useful for the Flask application as this user can be sent to the template to change behaviour. In this case, the nav bar is or will be changing the links based on whether the user is logged in or not. For this to occur, each template needs access to the `current_user` which in turn **requires each route to be updated to send the variable**.

Open `app.py` and **update EVERY route** **rendering a template** to include the additional argument `user=current_user**.**`

For instance, the homepage route needs to have the `render_template` line of code updated as shown.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/8b184e85-619e-4821-953f-43ab6c909423/a5ef45bf-76e9-47b8-9981-7e2bb30576f7/Untitled.png)

## Dynamic Navbar

In this instance, ‘dynamic navbar’ means that the navbar only shows links that are relevant or accessible that the current user can access.

For instance, if the user is not logged in, they will need the login link, however a user already logged in, will need a logout link instead.

---

`current_user` is built into `Flask-Login` allowing you to check to see if the user of the website is logged in or not, and if they are, then access the `User` model you defined in `models.py`. Hence using `user=current_user` on every route.

As the current user details is being sent to the template to be rendered, you can run some checks on that user.

Open `templates/base.html` and find the registration and login links.

![Screen Shot 2022-09-19 at 9.17.10 am.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/da66cdb0-e857-421e-8bb0-488cf238e3b8/Screen_Shot_2022-09-19_at_9.17.10_am.png)

Surrounding these two links, add an `if` statement to check to see if the user is anonymous. This means that the user has **not** logged in yet.

![Screen Shot 2022-09-19 at 9.18.45 am.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3e3ad516-5209-4385-b321-dbc5dafbba55/Screen_Shot_2022-09-19_at_9.18.45_am.png)

```python
{% if user.is_anonymous %}
...
{% endif %}
```

Test this code and you’ll notice that the Registration and Login links only show for users who are not logged in!

The next step is to extend this by adding in an {% else %} section to only show the links that are accessible for users who are logged in.

In the example shown, you can see that the **Registration** and **Login** links are shown if the user is not logged in (`is_anonymous`) and the **Profile**, **Photos**, **Logout** and **Reset Password** Links are shown if the user is logged in (`is_anonymous` is false)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/8b184e85-619e-4821-953f-43ab6c909423/43c10524-aa33-4420-a1e8-2232b6c4ade0/Untitled.png)

---

# Additional Information

N/A

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