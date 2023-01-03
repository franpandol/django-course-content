create a folder static and inside a folder css in our apps folder, for example posts/static/css
inside css lets write our rules

after this we have to create our static folder to hold a copy to serve in the website
mkdir static

Let's set the path of this folder in settings.py

STATIC_URL = '/static/'
STATIC_ROOT = os.path.join(BASE_DIR, 'static')

If we have static files that do not belong to any app we can tell django where to find them using the 
STATICFILES_DIRS setting

STATICFILES_DIRS = [
    os.path.join(BASE_DIR, "static"),
]

After this we have to run the command collectstatic
this command will copy all the static files from the apps to the static folder

python manage.py collectstatic

Now we can use the static files in our templates

{% load static %}
<link rel="stylesheet" href="{% static 'css/style.css' %}">

We can also use the static files in our views

from django.contrib.staticfiles.storage import staticfiles_storage
from django.views.generic import TemplateView

class HomePageView(TemplateView):
    template_name = "home.html"

    def get_context_data(self, **kwargs):
        context = super().get_context_data(**kwargs)
        context["image_url"] = staticfiles_storage.url("images/image.png")
        return context



Check the commit 81762b5