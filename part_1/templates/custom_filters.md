We are writing the posts using Markdown so we need to convert it to html to show it in a website. Let's create a filter for that. Create a file named `markdown_filter.py` in the `posts` folder and add the following code:


https://docs.djangoproject.com/en/4.1/howto/custom-template-tags/

he app should contain a templatetags directory, at the same level as models.py, views.py, etc. If this doesn’t already exist, create it - don’t forget the __init__.py file to ensure the directory is treated as a Python package.

For example, if your custom tags/filters are in a file called markdown_filter.py, your app layout might look like this:

posts/
    __init__.py
    models.py
    templatetags/
        __init__.py
        markdown_filter.py
    views.py

Install markdown for python
https://python-markdown.github.io/install/
pip install markdown

# markdown_filter.py
from django import template
import markdown

register = template.Library()

@register.filter
def markdown_to_html(text):
    return markdown.markdown(text) 

And in your template you would use the following:

{% load markdown_filter %}
<!DOCTYPE html>
<html>
  <head>
    <title>Posts</title>
  </head>
  <body>
    <h1>Posts</h1>
    {{ post.title }}
    {{ post.content|markdown_to_html|safe }}
    {{ post.date_posted }}
    <ul>
    </ul>
  </body>
</html>

https://python-markdown.github.io/extensions/code_hilite/

