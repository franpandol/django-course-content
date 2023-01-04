# Views (Class 6)

In Django, a view is an endpoint that can be accessed by users to retrieve data. Views are written as Python functions and take a request and return a response.

Django provides a mapping between URL paths and views called URLconf. When a user requests a URL, Django uses the URLconf to match the URL path to a view and then calls the view to get the response. This is a topic that we have already covered in the previous chapter.

The response can be anything, but most often it will be a template that renders some data to the user. For example, you might have a view that renders a list of all the articles on your blog.

Views are usually stored in views.py files. Here's an example of a simple view that renders a template:

```python
from django.shortcuts import render

def my_view(request):
    return render(request, 'my_template.html', {
        'foo': 'bar',
    })
```

This view takes a request and returns a rendered template. The template will have access to the foo variable, which we've set to "bar".

We can also return HttpResponse objects from views. For example, we might want to return an 404 error if the user tries to access a view that doesn't exist:

```python
from django.http import Http404

def my_view(request):
    raise Http404()
```

This view will always return a 404 error.


## The request object

When a user requests a view, Django creates a request object that contains information about the request. This object is passed to the view as the first argument.
We can also access information about the user from the request object. For example, we might want to know what IP address the user is coming from:

```python
def my_view(request):
    ip_address = request.META.get('REMOTE_ADDR')
    # do something with the IP address...
```

The request object has a lot of other information about the user and the request itself. You can explore the request object in the Django shell:

```bash
>>> from django.shortcuts import render
>>> def my_view(request):
...     return render(request, 'my_template.html', {})
>>> request = my_view(None)
>>> type(request)
<class 'django.http.HttpResponse'>
>>> request.content
b'<!DOCTYPE html>\n<html>\n    <head>\n    </head>\n    <body>\n        <h1>My Template</h1>\n    </body>\n</html>'
>>> request.status_code
200
```

The request object is a HttpResponse object, which means it has all the same attributes as a normal HttpResponse object. In this case, we're interested in the content and status_code attributes.

The content attribute is the rendered template, and the status_code attribute is the HTTP status code of the response. In this case, we're getting a 200 response, which means everything is OK.

If we want to access specific information about the user, we can use the request.user attribute. This attribute will give us a User object that represents the currently logged in user:

```python
def my_view(request):
    if request.user.is_authenticated:
        # do something for authenticated users...
    else:
        # do something for anonymous users...
```

This view will do something different depending on whether the user is logged in or not. If the user is logged in, we might want to show them different information than we would for an anonymous user.

The User object has a lot of helpful methods and attributes that we can use to determine things about the user. For example, we can check to see if the user is staff or superuser:

```python
def my_view(request):
    if request.user.is_staff:
        # do something for staff users...
    elif request.user.is_superuser:
        # do something for superusers...
    else:
        # do something for regular users...
```

We can also access any custom attributes that we've added to our User model:

```python
def my_view(request):
    if request.user.is_authenticated:
        print(request.user.profile.favorite_color)
```

This view will print the user's favorite color to the console. We've assumed that we've added a favorite_color field to our UserProfile model.

We can also access any information that's been passed in the URL. For example, if we have a URL like this:

```
/posts/<post_id>/
```

We can access the post_id in our view:

```python
def my_view(request, post_id):
    print(post_id)
```

This view will print the post_id to the console.

We can also access any query parameters that have been passed in the URL. For example, if we have a URL like this:

```
/posts/?page=<page_number>/
```

We can access the page_number in our view:

```python
def my_view(request):
    page_number = request.GET.get('page')
    print(page_number)
```

This view will print the page_number to the console.

In the views.py file is where we will write the code that will handle the requests that come in from the user. We will access the database and return the data to the user. We will also handle any errors that may occur.

In future chapters we will see how to return data from the database to the user. We will also see how to handle errors and how to redirect the user to another page.