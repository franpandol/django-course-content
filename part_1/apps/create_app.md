# Creating our first app (Class 3)

Django introduces a concept called apps. Apps in django are like submodules.
We will have apps like friends and birthdays in a calendar system. Or in a blog system
we will have apps like blog and posts. Let's create our first app 'birthdays':

    $ python manage.py startapp birthdays

    birthdays
    ├── __init__.py
    ├── admin.py
    ├── apps.py
    ├── models.py
    ├── tests.py
    ├── views.py
    └── migrations
        ├── __init__.py

Let's dive deep into the files created.

###models.py
django uses a pattern called MVT - The M is for models.
The models in django are the equivalent of tables in a relational database.
We can see that the models.py file that django created is empty. So let's write
our first model.
    

```python
from django.db import models


class Birthday(models.Model):
    friend = models.CharField(max_length=50)
    date = models.DateField()
    description = models.TextField(blank=True)

    def __str__(self):
        return self.friend

```

First we define a class that inherits from models.Model.
Then we define the fields that our model will have.
* The first field is a CharField that will store the name of the friend.
* The second field is a DateField that will store the date of the birthday.
* And the third field is a TextField that will store a description of the birthday.
You can check the [django documentation](https://docs.djangoproject.com/en/4.1/ref/models/fields/) for more information about the fields.


Finally we override the str method. This method is used to return a string
representation of the model

The next step is to add our app in the settings.py file, modifying the INSTALLED_APPS variable. This will let Django know that our app exists and should be included in the project.

Add the following line to the INSTALLED_APPS list in mysite/settings.py:

```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'birthdays', # <-- Add this line
]
```

Now remember that every time we modify a model we need to create a migration.
This is done by running the command:

```bash
$ python manage.py makemigrations # you can inspect the changes in the migrations folder

$ python manage.py migrate

Migrations for 'birthdays':
    0001_initial.py
```

We can play with our new model by creating a new instance of the model and saving it to the database:

```python
$ python manage.py shell
>>> from birthdays.models import Birthday
>>> b = Birthday(friend='Fran', date='1988-01-01', description='Still alive!')
>>> b.save()
>>> b
<Birthday: Birthday object>
>>> b.friend
'Fran'
>>> b.date
datetime.date(2000, 1, 1)
>>> b.description
'Still alive!'
```

And that's it for today, we have a fully functional model that we can use to store our birthdays.
We will check the rest of the files created in the next chapter.