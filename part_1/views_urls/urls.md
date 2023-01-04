# URLs (Class 5)

In Django, a URL is the path to a view. 

Django comes with a built-in URL dispatcher that maps URL patterns to views. URL patterns are simply regular expressions that are used to match against a URL path.

Views are mapped to URL patterns in the URLconf. When a user requests a URL, Django uses the URLconf to match the URL path to a view and then calls the view to get the response.

Django's built-in URL dispatcher makes it easy to map URLs to views. All you need to do is to create a URL pattern and map it to a view. This patterns are located in urls.py

Every Django project has a urls.py file. This file contains a list of mappings that tell Django which view to call when a user requests a specific URL.


```python
# urls.py
from django.urls import path
from .views import detail, home

urlpatterns = [
    path("<slug:slug>", detail, name="blog-detail"),
    path("<int:id>", detail, name="blog-detail"),
    path("", home, name="blog-home"),
]
```

The first argument in the path function is the URL pattern. The second argument is the view that will be called when a user requests the URL. The third argument is the name of the URL pattern. This name is used to refer to the URL in other parts of the project.
In this example we use two different types of URL patterns. The first one is a slug, and the second one is an integer. The slug is a string that contains only letters, numbers, underscores or hyphens. The integer is a number. The slug is used to identify a post by its title, and the integer is used to identify a post by its id.

### Including other URLconfs

```python
# urls.py
from django.contrib import admin
from django.urls import path, include


urlpatterns = [
    path("admin/", admin.site.urls),
    path("posts/", include("posts.urls")),
]
```

The include() function allows referencing other URLconfs. When Django encounters include(), it chops off whatever part of the URL matched up to that point and sends the remaining string to the included URLconf for further processing.
This allows you to include other URL patterns in your project. In this example we include the URL patterns from the posts app. This means that when a user requests a URL that starts with posts/, Django will look for the URL patterns in the posts/urls.py file.
This enable us to have a different URLconf for each app in our project. This is a good practice because it allows us to have a clean and organized project.