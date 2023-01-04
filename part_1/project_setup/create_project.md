# Creating the project (Class 2)

Once we have our environment properly set up, we can create our project. Django provides a command to do this. Let's run it:

```bash
django-admin startproject mysite
```

Let's check our new project folder to understand what we have done.

    mysite
    ├── manage.py
    └── mysite
        ├── __init__.py
        ├── settings.py
        ├── urls.py
        ├── wsgi.py
        ├── asgi.py

**manage.py**
The manage.py file is a command-line utility that allows you to interact with your Django project. It also provides a number of subcommands that you can use to manage things like starting the development server, creating and applying migrations, and running management commands.

For example, 

Django comes with a built-in development server that you can use to test your application. To start the development server run the following command:
  
  ```bash
python manage.py runserver

Performing system checks...
System check identified no issues (0 silenced).
August 31, 2022 - 20:34:29
Django version 4.0.6, using settings 'mysite.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CONTROL-C.
```

You can check the server running if you open your browser in http://127.0.0.1:8000/

Other common manage.py subcommands include migrate, which is used to apply database migrations, and createsuperuser, which is used to create a new user with administrative privileges.

In addition to these built-in subcommands, you can also create your own custom management commands to perform specific tasks within your Django project. This can be useful for automating repetitive tasks or for implementing custom functionality that is specific to your project.

Overall, the manage.py file is a powerful and versatile tool for managing and interacting with a Django project. It is an essential part of any Django project, and it can save you a lot of time and effort when working with your project.

**settings.py**

We will use this file to configure our database, our static files, our templates, our apps, etc.
The official documentation for this file is [here](https://docs.djangoproject.com/en/4.0/ref/settings/).


We are gonna need a database. Django has already one defined by default, an sqlite3 database.

sqlite3 is a file based database. It is very easy to use and it is perfect for development. It is not recommended for production.

```python
#settings.py
DATABASES = {
    "default": {
        "ENGINE": "django.db.backends.sqlite3",
        "NAME": BASE_DIR / "db.sqlite3",
    }
}
```

The migrate command applies the migrations files located in the migrations folder of every django app. This migration files are python files that contain the instructions to create and modify the tables in the database.

The first time you run it it will create the framework base tables.

```bash
python manage.py migrate

Operations to perform:
  Apply all migrations: admin, auth, contenttypes, sessions
Running migrations:
  Applying contenttypes.0001_initial... OK
  Applying auth.0001_initial... OK
  Applying admin.0001_initial... OK
  Applying admin.0002_logentry_remove_auto_add... OK
  Applying admin.0003_logentry_add_action_flag_choices... OK
  Applying contenttypes.0002_remove_content_type_name... OK
  Applying auth.0002_alter_permission_name_max_length... OK
  Applying auth.0003_alter_user_email_max_length... OK
  Applying auth.0004_alter_user_username_opts... OK
  Applying auth.0005_alter_user_last_login_null... OK
  Applying auth.0006_require_contenttypes_0002... OK
  Applying auth.0007_alter_validators_add_error_messages... OK
  Applying auth.0008_alter_user_username_max_length... OK
  Applying auth.0009_alter_user_last_name_max_length... OK
  Applying auth.0010_alter_group_name_max_length... OK
  Applying auth.0011_update_proxy_permissions... OK
  Applying auth.0012_alter_user_first_name_max_length... OK
  Applying sessions.0001_initial... OK
```

Every time  you make a change in your models, you need to run the makemigrations command to create the migration file 
and after that the migrate command to apply the migration and modify the database.

```bash
python manage.py makemigrations
python manage.py migrate
```

**wsgi.py**
WSGI (Web Server Gateway Interface) is a specification that defines how a web server communicates with web applications, and how web applications can be chained together to process one request.

The WSGI specification defines a standard interface between web servers and web applications, which allows for a pluggable architecture. This means that you can use any WSGI-compatible web server to host your Django application, and you can use any WSGI-compatible application framework to develop your application.

In Django, the file wsgi.py is an entry point for WSGI-compatible web servers to serve your Django project. It contains a single WSGI application object that the web server uses to communicate with your Django project. When a request is made to your Django project, the web server will forward it to the WSGI application, which will then handle the request and return the appropriate response. 

The wsgi.py file is an important part of Django's deployment options and is commonly used in production environments. It allows you to use any WSGI-compatible web server to host your Django project, and it provides a standard way for Django to interface with these web servers.

ASGI (Asynchronous Server Gateway Interface) is a specification for building asynchronous web applications. It is similar to WSGI, but is designed to support asyncio and async/await syntax.

In Django, the file asgi.py is an entry point for ASGI-compatible web servers to serve your Django project asynchronously. 


In the next chapter we will create our first app.