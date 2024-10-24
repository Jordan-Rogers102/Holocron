$\color{black} \fcolorbox{lightgreen}{lightgreen} {Overview}$

The goals for this topic are:

- Add a Database
- Configure codespaces
- Implement a Contact Form

<aside> <img src="/icons/list_orange.svg" alt="/icons/list_orange.svg" width="40px" /> $\utilde {\color{black} \fcolorbox{darkorange}{darkorange} {Table of Contents}}$

</aside>

$\color{black} \fcolorbox{lightblue}{lightblue} {Submission}$

In the Google Classroom Assignment, submit the following:

- Screenshots of the database having been updated through the Contact form.

---

# Video

Watch the video/s supplied to understand the topics for this week.

[https://www.youtube.com/watch?v=_lD0ow-leUk&ab_channel=RyanCather](https://www.youtube.com/watch?v=_lD0ow-leUk&ab_channel=RyanCather)

$\utilde {\color{black} \fcolorbox{darkorange}{darkorange} {Commit and Push to Github}}$

---

# Theory

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/8b184e85-619e-4821-953f-43ab6c909423/eda7e39b-4f2b-41ca-beba-f011a427ddef/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/8b184e85-619e-4821-953f-43ab6c909423/415b2638-7838-4b59-97ca-36f2e472fba3/Untitled.png)

---

# Practical Tasks - Database Configuration

## Install SQLite

The first thing you need to do is install sqlite in the codespace instance.

Once the project is open, go to the Terminal Tab and enter the following commands:

`sudo apt update`

`sudo apt install sqlite3`

Hitting enter after each command.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/8b184e85-619e-4821-953f-43ab6c909423/2b266f2c-a43c-424d-b2ee-dff2d90a8b25/Untitled.png)

## Extensions

Install the following Extensions

- Database Client JDBC
- MySQL

Both extensions written by Weijan Chen

# Practical Tasks - Contact

## Code Snippets

- `config.py`
    
    ```python
    import os
    basedir = os.path.abspath(os.path.dirname(__file__))
    
    class Config(object):
        SECRET_KEY = os.environ.get('SECRET_KEY') or 'you-will-never-guess'
        # Database configuration
        SQLALCHEMY_DATABASE_URI = os.environ.get('DATABASE_URL') or 'sqlite:///' + os.path.join(basedir, 'site.db')
        SQLALCHEMY_TRACK_MODIFICATIONS = False
    ```
    
- `forms.py`
    
    ```python
    from flask_wtf import FlaskForm
    from wtforms.validators import DataRequired, Email, EqualTo, ValidationError
    from wtforms import StringField, SubmitField, IntegerField, PasswordField, FileField
    from flask_wtf.file import FileRequired
    from models import User
    
    class ContactForm(FlaskForm):
        name = StringField("Name", validators=[DataRequired()], render_kw={"class": "border border-primary rounded text-primary bg-light"})
        email = StringField("Email", validators=[DataRequired(), Email()], render_kw={"class": "border border-primary rounded text-primary bg-light"})
        message = StringField("Message", validators=[DataRequired()], render_kw={"class": "border border-primary rounded text-primary bg-light"})
        submit = SubmitField('Submit', render_kw={"class": "btn btn-primary btn-block"})
    
    ```
    
- `models.py`
    
    ```python
    from app import db, login
    from datetime import datetime
    from flask_login import UserMixin
    from werkzeug.security import generate_password_hash, check_password_hash
    
    class Contact(db.Model):
        id = db.Column(db.Integer, primary_key=True, autoincrement=True)
        name = db.Column(db.Text)
        email = db.Column(db.Text)
        message = db.Column(db.Text)
        dateSubmitted = db.Column(db.DateTime)
    
        def __init__(self, name, email, message):
            self.name = name
            self.email = email
            self.message = message
            self.dateSubmitted = datetime.today()
    
    class User(UserMixin, db.Model):
        id = db.Column(db.Integer, primary_key=True)
        email_address = db.Column(db.String(255), unique=True)
        name = db.Column(db.String(255))
        password_hash = db.Column(db.String(255))
        user_level = db.Column(db.Integer)
        active = db.Column(db.Boolean)
    
        def set_password (self, password):
            self.password_hash = generate_password_hash(password)
    
        def check_password (self, password):
            return check_password_hash(self.password_hash, password)
    
        def is_admin(self):
            if self.user_level == 2:
                return True
            else:
                return False
    
        def update_details(self, email_address, name):
            self.email_address = email_address
            self.name = name
    
    @login.user_loader
    def load_user(id):
        return User.query.get(int(id))
    ```
    
- `app.py` - imports
    
    ```python
    from flask import Flask, render_template, request, redirect, url_for, flash
    from config import Config
    from flask_sqlalchemy import SQLAlchemy
    from flask_login import current_user, login_user, LoginManager, logout_user, login_required
    ```
    
- `app.py` - app configuration
    
    ```python
    app.config.from_object(Config)  # loads the configuration for the database
    db = SQLAlchemy(app)  # creates the db object using the configuration
    login = LoginManager(app)
    login.login_view = 'login'
    
    from forms import ContactForm, LoginForm, RegistrationForm, ResetPasswordForm, UserProfileForm
    from models import User, Contact
    ```
    
- `app.py` - routes
    
    ```python
    @app.route("/contact", methods=["POST", "GET"])
    def contact():
        form = ContactForm()
        if form.validate_on_submit():
            new_contact = Contact(name=form.name.data, email=form.email.data, message=form.message.data)
            db.session.add(new_contact)
            db.session.commit()
            # flash("Your message has been sent to administrators.")
            return redirect(url_for("homepage"))
        return render_template("contact.html", title="Contact Us", form=form, user=current_user)
    
    ```
    
- `contact.html`
    
    ```html
    {% extends 'base.html' %}
    
    {# Place the content for the rowTwoColOneContent in this block #}
    {% block rowTwoColOneContent %}
        Sidebar content.
    {% endblock %}
    
    {# Place the content for the rowTwoColTwoContent in this block #}
    {% block rowTwoColTwoContent %}
        <form action="" method="post" novalidate>
            {{ form.hidden_tag() }}
            <p>
                {{ form.name.label }}<br>
                {{ form.name(size=32) }}<br>
                {% for error in form.name.errors %}
                    <span style="color: red;">[{{ error }}]</span>
                {% endfor %}
            </p>
            <p>
                {{ form.email.label }}<br>
                {{ form.email(size=32) }}<br>
                {% for error in form.email.errors %}
                    <span style="color: red;">[{{ error }}]</span>
                {% endfor %}
            </p>
            <p>
                {{ form.message.label }}<br>
                {{ form.message(size=32) }}<br>
                {% for error in form.message.errors %}
                    <span style="color: red;">[{{ error }}]</span>
                {% endfor %}
            </p>
            <p>{{ form.submit() }}</p>
        </form>
    {% endblock %}
    
    {# Place the content for the cellContent3 in this block #}
    {% block cellContent3 %}
        Footer
    {% endblock %}
    ```
    

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