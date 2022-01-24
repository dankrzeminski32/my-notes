# Python Django

## Creating a django project

-   Make sure you are in a virtual environment
-   Make sure you pip install django

Let's start our project

Inside your project folder run this in shell,

```
django-admin startproject "project-name" .
```

The `.` at the end let's django know that we are already in our working environment and that there is no need to add a root `"project-name"` folder

We should now have `venv\`, `"project-name"\`, and `manage.py` in our project folder

In the root folder run a `python manage.py runserver`, this will let you know if it is working

![manage.py shell](./img/pythonManagePyShell.png)

![manage.py shell](./img/pythonManagePyHTML.png)

This runs a web server written entirely in python, made for development.

> **NEVER USE THIS IN PRODUCTION, IT IS ONLY MADE FOR DEVELOPMENT**

We will stick to something like apache for production.

## Creating apps within our django project

Projects vs. apps

What’s the difference between a project and an app? An app is a web application that does something – e.g., a blog system, a database of public records or a small poll app. A project is a collection of configuration and apps for a particular website. A project can contain multiple apps. An app can be in multiple projects.

to create an app in our project...

```
python manage.py startapp "app-name"
```

This creates a top level module if you ran that in the root with manage.py

Apps come with this file structure inside of them...

```
"app-name"/
    __init__.py
    admin.py
    apps.py
    migrations/
        __init__.py
    models.py
    tests.py
    views.py
```

## Views

Inside our app we have a views.py file

A view function, or view for short, is a Python function that takes a web request and returns a web response. This response can be the HTML contents of a web page, or a redirect, or a 404 error, or an XML document, or an image . . .

Let's add this to our views.py file (at the top)

```
from django.http import HttpResponse
```

When a page is requested, django creates an HttpRequest object.

This HttpRequest object contains metadata about the request.

each view is responsible for returning an HttpResponse object.

let's add a view to views.py

```
def index(request):
    return HttpResponse("Hello world")
```

In order to call this view we need to map it to a url

Create a `urls.py` file in your **APP** folder, not project folder

in `urls.py` add these references,

```
from django.urls import path
from . import views
```

This imports our necessary modules into our file

now me must add paths to our `urls.py` file,

```
urlpatterns = [
    path('', views.index, name='index')
]
```

These will all add views under url app/your-views

The **first** parameter describes the path of the views route.

the **second** parameter describes which view we want to reference.

the **third** gives our url a metadata type name to be used for other stuff?

Now we must configure this group of url paths under it's app domain.

So we head to the **project folder -> urls.py**

```
from django.contrib import admin
from django.urls import include, path

urlpatterns = [
    path('admin/', admin.site.urls),
    path('app-name/', include('app-name.urls')) //we add all of our project/app-name/URLS
]
```

## Database Setup

By default, django uses **SQLite**.

**SQLite** is included with python, so no need to worry about installing anything.

When making a production site, we may want to use a more scaleable database like **postgreSQL**

> If you wish to use another database, install the appropriate database bindings and change the following keys in the DATABASES 'default' item to match your database connection settings:
> ENGINE – Either 'django.db.backends.sqlite3', 'django.db.backends.postgresql', 'django.db.backends.mysql', or 'django.db.backends.oracle'. Other backends are also available.
> NAME – The name of your database. If you’re using SQLite, the database will be a file on your computer; in that case, NAME should be the full absolute path, including filename, of that file. The default value, BASE_DIR / 'db.sqlite3', will store the file in your project directory.
> If you are not using SQLite as your database, additional settings such as USER, PASSWORD, and HOST must be added. For more details, see the reference documentation for DATABASES.

[good reference for database basics](https://docs.djangoproject.com/en/4.0/intro/tutorial02/)
