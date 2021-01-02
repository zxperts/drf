#Django notes

django-admin startapp users


class UsersConfig(AppConfig):
    name = 'users'

pip install pillow

python manage.py shell
from djnago .contrib.auth.models import user

__in ordezr to ger the user__
user =user.objects.filer(username='ashutosh').first()

__to see the user__
>>user
__to get the user __
>>user.profile
>>user.profile.user



### Building REST APIs With Python & Django
>pip install djangorestframework
django-admin startproject mysite
cd mysite
django-admin startapp movies


ading the project to git 
- Creer un dosier dans giHub
- Creer un dossier dans Pqycharm
- Faire un commit & un push 
- Définir le remote


----

### Create the model
>pip install django
pip3 install djangoframework
python manage.py makemigrations
>python manage.py migrates

Create the superuser

>python manage.py createsuperuser

-- 
>pyhton manage.py runserver

### Installation de l'environement virtuel

>pip install virtualenv

go to the directory
>virtualenv my_env

to use , you need to activate
cd to th directory
>cd scripts
>activate

When it's activated you will have (env)

to desactivate 
>deactivate

when you are in your (env)
you can install django
>pip install django

>django-admin startproject mysite

>python manage.py runserver

### Creation of a app

creation of a app
>django-admin startapp newapp

You can create a movie model 
then you register the app in the settings : 
>'newapp',

or this way

>'movies.apps.MoviesConfig',
the ndo the migration
>python manage.py makemigrations
>python manage.py migrates

to add data, create a superusr
>python manage.py createsuperuser

go to   the server and add data
But before register the model in the Adlin.oy
>from .models import Movies
>admin.site.register(Movies)

### Create view and templates

####views.py
```python
from django.shortcuts import render
from .models import Movies
# Create your views here.
def moive_list(request):
    movie_objects = Movies.objects.a11()
    return render(request,'newapp/movie_list.htm1',{'movie_objects':movie_objects})
```
####movie_list.html
templates>newapp>movie_list.html

```python
{% for movie_item in movie_objects %}
    {{ movie_item.name }}
{% endfor %}
```

####urls.py
```python
from django.contrib import admin
from django.urls import path
from newapp import views
urlpatterns = [
    path('admin/', admin.site.urls),
    path('moviesl',views.movie_list,name='movie_list'),
]
```

### Pagination

####views.py
```python
from django.shortcuts import render
from .models import Movies
# Create your views here.
def moive_list(request):
    movie_objects = Movies.objects.a1l()

    paginator = Paginator(movie_objects,4)#here
    page = request.GET.get('page')
    movie_objects = paginator.get_page(page)

    return render(request,'newapp/movie_list.htm1',{'movie_objects':movie_objects})
```

####movie_list.html

```python
{% for movie_item in movie_objects %}
    {{ movie_item.name }}
{% endfor %}

{% if movie_objects.has_previous %}#here
    <a href="?page=1">First</a>
    <a href="?page={{ movie_objects.previous_page_number }}">Previous</a>
{% endif %}

Page: {{ movie_objects.number }} of {{ movie_objects.paginator.num_pages}}

{% if movie_objects.has_next %} 
    <a href="?page={{ movie_objects.next_page_numb }}">Next</a>
    <a href="?page={{ movie_objects.paginator.num_pages }}">Last</a>
{% endif %}

```

### Adding Search Functionality

####movie_list.hmtl
```python
<form action="" method="GET">#here
    <input type="search" name="movie_name">
    <button type="submit">Search</button>
</form>
 
{% for movie_item in movie_objects %}
    {‌{ movie_item.name }}
</br>
{% endfor %}
 
{% if movie_objects.has_previous %}
    <a href="?page=1">First</a>
    <a href="?page={‌{ movie_objects.previous_page_number }}">Previous</a>
{% endif %}
 
Page: {‌{ movie_objects.number }} of {‌{ movie_objects.paginator.num_pages }}
 
{% if movie_objects.has_next %}
    <a href="?page={‌{ movie_objects.next_page_number }}">Next</a>
    <a href="?page={‌{ movie_objects.paginator.num_pages }}">Last</a>
{% endif %}
```

####views.py
```python
def movie_list(request):
    movie_objects = Movies.objects.all()
 
    movie_name = request.GET.get('movie_name')#here
 
    if movie_name != '' and movie_name is not None:
        movie_objects = movie_objects.filter(name__icontains=movie_name)
 
    paginator = Paginator(movie_objects,4)
    page = request.GET.get('page')
    movie_objects = paginator.get_page(page)
 
    return render(request,'newapp/movie_list.html',{'movie_objects':movie_objects})
```


### User Permissions

Staff permissions 
