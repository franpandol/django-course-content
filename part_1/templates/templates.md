https://docs.djangoproject.com/en/4.1/ref/templates/

Templates in django are the third part of the pattern MVT (Model, View, Template) used by the framework. 
The templates are the part that the user sees, and they are written in HTML.
Let's use the views to render a template with a context. This is our first contact with the V in MVT. The function defined in views.py will fill the template with data from the database. The template will be rendered and returned to the user.


# views.py

from django.shortcuts import render

def home(request):
    context = {
        'posts': Post.objects.all()
    }
    return render(request, 'posts/home.html', context)

# home.html

{% extends 'posts/base.html' %}
{% block content %}
    <h1>Blog Home</h1>
    {% for post in posts %}
        <h2>{{ post.title }}</h2>
    {% endfor %}
{% endblock content %}

And in our template we'll se a list of posts.


Another example of a template is the following:

# views.py
from django import template

t = template.Template("""
<html>
<head>
    <title>{{ title }}</title>
</head>
<body>
    {{ body }}
</body>
</html>
""")
print(t.render(template.Context({"title": "My Title", "body": "My Body"})))


In this example, we first create a Template instance with a string containing our template code. We then use the Template object's render() method to render the template with a given Context. The Context is a dictionary-like object that allows us to specify values for variables used in the template.

In the template code, we use double curly braces ({{ }}) to insert values from the Context into the rendered template. In this example, we insert the value of the "title" variable into the <title> element and the value of the "body" variable into the <body> element.

The output of this code example will be the following HTML:

<html>
<head>
    <title>My Title</title>
</head>
<body>
    My Body
</body>
</html>


Django also provides a set of built-in template tags and filters that can be used in your templates. Template tags and filters are used to modify how a value is displayed in the rendered template. For example, the "upper" filter converts a string to uppercase:

{{ "foo"|upper }}


In this example, the "foo" string will be converted to uppercase and inserted into the template. The output of this code would be "FOO".

There are many different template tags and filters available in Django. For more information, see the Django documentation on template tags and filters.

If you need to create custom template tags or filters, you can do so by creating a Django app and adding your custom tags and filters to the app's "template_tags" module. For more information, see the Django documentation on creating custom template tags and filters.

In summary, Django templates are a powerful way to generate HTML dynamically. By understanding how Django compiles and renders templates, you can create custom template tags and filters to generate HTML exactly the way you want it.


Django language template syntax is a way to define how Django templates should be rendered. The code examples below show how to use {% and {{ }} in your templates to display data from your Django models.

To display a list of objects in your template, use the {% for %} tag:

{% for obj in object_list %}
{{ obj.name }}
{% endfor %}


If you want to display a single object in your template, use the {{ object }} tag:

{{ object.name }}


You can also use the {% if %} tag to check if an object exists:

{% if object %}
{{ object.name }}
{% endif %}

If you want to display a link to an object, use the {% url %} tag:

<a href="{% url 'object_detail' object.id %}">{{ object.name }}</a>

The {% block %} tag is used to define a block of content that can be overridden by child templates:

{% block content %}
This is the default content.
{% endblock %}


Child templates can override the content block by using the {% extends %} tag:

{% extends "base.html" %}

{% block content %}
This content will be displayed in the child template.
{% endblock %}

Django template language syntax

Django's template language is designed to strike a balance between power and ease. It's designed to feel comfortable to those used to working with HTML. If you have any background in programming, Django's template language will make a lot of sense.

The basic syntax of the Django template language is quite simple. Consider the following example:

```
{{ variable }}
```

This would output the value of ```variable```. If ```variable``` is a string, it will be output as-is. If it's a number, it will be converted to a string before being output.
