---
title: "Django Admin (Class 4)"
---
One nice feature of Django is its ability to create a CRUD interface for your application automatically from the models. The models are the represaentation of the data in the database. Django provides a default admin interface that you can use to manage your application's data. You can also customize the admin interface to suit your needs.

To use the Django admin feature, you first need to create a superuser account by running the following command:

python manage.py createsuperuser

This will prompt you to enter a username, email address, and password for your superuser account. 
You also have to set an url to access the admin interface
This is made in the urls.py file.


```python
# urls.py
from django.contrib import admin
from django.urls import path

urlpatterns = [
    path('admin/', admin.site.urls),
]
```

Once you have created a superuser account, you can log in to the admin interface by visiting the /admin/ URL of your Django project in a web browser.


You will see a list of all the models that are registered with the admin feature. You can use the admin interface to perform a variety of tasks, such as creating and editing records, managing users and groups, and changing the site settings.

One of the benefits of the Django admin feature is that it is customizable, so you can tailor the interface to suit the specific needs of your project. For example, you can change the layout of the admin interface, add custom filters and search fields, and define custom actions for models.

Let's modify our admin interface for the birthday model to show the age of the person.

```python
# birthdays/admin.py
from django.contrib import admin
from birthdays.models import Birthday

class BirthdayAdmin(admin.ModelAdmin):
    list_display = ('name', 'age', 'date')
    list_filter = ('date',)
    search_fields = ('name',)

    def age(self, obj):
        return obj.date.today().year - obj.date.year

admin.site.register(Birthday, BirthdayAdmin)
```
