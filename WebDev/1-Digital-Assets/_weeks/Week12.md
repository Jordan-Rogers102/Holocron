$\color{black} \fcolorbox{lightgreen}{lightgreen} {Overview}$

The goals for this topic are:

- Implement a User Management system

<aside> <img src="/icons/list_orange.svg" alt="/icons/list_orange.svg" width="40px" /> $\utilde {\color{black} \fcolorbox{darkorange}{darkorange} {Table of Contents}}$

</aside>

$\color{black} \fcolorbox{lightblue}{lightblue} {Submission}$

In the Google Classroom Assignment, submit the following:

- Screen cast of users registering, logging in and logging out.

---

# Video

Watch the video/s supplied to understand the topics for this week.

[https://youtu.be/8RXUjyVR2Lc](https://youtu.be/8RXUjyVR2Lc)

---

# Resources

## User Table

The focus for this week is creating a user management system. Users will be able to

- register an account
- Login
- Logout

To support the functionality required, a new table needs to be created in the database. The structure of the table can be seen here.

The user will login with their `email_address` and `password`.

Note that the password is stored as `password_hash`. More on that later.

`user_level` will be used to identify if the user is a regular user (1) or an administrator (2).

`name` is just for identification purposes.

![User.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/8b184e85-619e-4821-953f-43ab6c909423/3f7d3949-5880-435d-a977-4f70177e93a0/User.png)

---

# Theory

[Password Hashing](https://www.notion.so/Password-Hashing-82e83087f3904ead85bbf202901d010e?pvs=21)

---

# Practical Tasks

## Code Snippets

- SQL - User Table
    
    ```sql
    
    CREATE TABLE User(  
        id INTEGER NOT NULL PRIMARY KEY AUTOINCREMENT,
        email_address TEXT,
        name TEXT,
        password_hash TEXT,
        user_level INTEGER,
        active BOOLEAN
    );
    ```
    
- base.html updates
    
    Add new links in the navbar to registration and login routes
    
    ```html
    <a class="nav-link" href="/register">Registration</a>
    <a class="nav-link" href="/login">Login</a>
    <a class="nav-link" href="/logout">Logout</a>
    <a class="nav-link" href="/passwordreset">Password Reset</a>
    ```
    
- [app.py](http://app.py) updates
    
    Update the import section.
    
    ```python
    from forms import ContactForm, LoginForm, RegistrationForm
    from models import Contact, User
    ```
    
    Add new routes:
    
    ```python
    @app.route("/register", methods=["GET", "POST"])
    def register():
        form = RegistrationForm()
        if form.validate_on_submit():
            new_user = User(email_address=form.email_address.data, name=form.name.data, user_level=1, active=True) # defaults to regular user
            new_user.set_password(form.password.data)
            db.session.add(new_user)
            db.session.commit()
            return redirect(url_for("homepage"))
        return render_template("registration.html", title="User Registration", form=form)
    
    @app.route('/login', methods=["POST", "GET"])
    def login():
        form = LoginForm()
        if form.validate_on_submit():
            user = User.query.filter_by(email_address=form.email_address.data).first()
            print(user)
            if user is not None and user.check_password(form.password.data):
                # User has been authenticated
                login_user(user)
                print("DEBUG: Login Successful")
                return redirect(url_for("homepage"))
            else:
                print("DEBUG: Login Failed")
                # Username or password incorrect
                return redirect(url_for("login"))
        return render_template("login.html", title="Login", form=form)
    
    @app.route('/passwordreset', methods=['GET', 'POST'])
    @login_required
    def reset_password():
        form = ResetPasswordForm()
        if form.validate_on_submit():
            user = User.query.filter_by(email_address=current_user.email_address).first()
            user.set_password(form.new_password.data)
            db.session.commit()
            flash("Your password has been changed.")
            return redirect(url_for('homepage'))
        return render_template("passwordreset.html", title='Reset Password', form=form, user=current_user)
    
    ```
    
- [forms.py](http://forms.py) updates
    
    Add new forms for Registration and Login
    
    ```python
    class RegistrationForm(FlaskForm):
        email_address = StringField("Email Address (Username)", validators=[DataRequired(), Email()])
        name = StringField("Full Name", validators=[DataRequired()])
        password = PasswordField("Password", validators=[DataRequired()])
        password_confirm = PasswordField("Confirm Password", validators=[DataRequired(), EqualTo("password")])
        submit = SubmitField("Register")
    
        def validate_email_address(self, email_address_to_register):
            user = User.query.filter_by(email_address=email_address_to_register.data).first()
            if user is not None:
                raise ValidationError("Please Use a Different Email Address)")
    
    class LoginForm(FlaskForm):
        email_address = StringField('Email Address', validators=[DataRequired()])
        password = PasswordField('Password', validators=[DataRequired()])
        submit = SubmitField('Sign In')
    
    class ResetPasswordForm(FlaskForm):
        new_password = StringField('New Password', validators=[DataRequired()])
        submit = SubmitField('Submit')
    
    ```
    
- registration.html
    
    ```html
    {% extends 'base.html' %}
    
    {# Place the content for the rowTwoColOneContent in this block #}
    {% block rowTwoColOneContent %}
    Sidebar content.
    {% endblock %}
    
    {# Place the content for the rowTwoColTwoContent in this block #}
    {% block rowTwoColTwoContent %}
    <form action="" method="post">
        {{ form.hidden_tag() }}
    
        <p>
            {{ form.email_address.label }}<br>
            {{ form.email_address(size=64) }}<br>
            {% for error in form.email_address.errors %}
            <span style="color: red;">[{{ error }}]</span>
            {% endfor %}
        </p>
        <p>
            {{ form.name.label }}<br>
            {{ form.name(size=64) }}<br>
            {% for error in form.name.errors %}
            <span style="color: red;">[{{ error }}]</span>
            {% endfor %}
        </p>
        <p>
            {{ form.password.label }}<br>
            {{ form.password(size=32) }}<br>
            {% for error in form.password.errors %}
            <span style="color: red;">[{{ error }}]</span>
            {% endfor %}
        </p>
        <p>
            {{ form.password_confirm.label }}<br>
            {{ form.password_confirm(size=32) }}<br>
            {% for error in form.password_confirm.errors %}
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
    
- login.html
    
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
                {{ form.email_address.label }}<br>
                {{ form.email_address(size=32) }}<br>
                {% for error in form.email_address.errors %}
                    <span style="color: red;">[{{ error }}]</span>
                {% endfor %}
            </p>
            <p>
                {{ form.password.label }}<br>
                {{ form.password(size=32) }}<br>
                {% for error in form.password.errors %}
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
    
- passwordreset.html
    
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
            Resetting Password for user: <div class = "focus">{{ user.email_address }}</div>
        </p>
            <p>
                {{ form.new_password.label }}<br>
                {{ form.new_password(size=32) }}<br>
                {% for error in form.new_password.errors %}
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