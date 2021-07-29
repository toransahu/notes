<h1>Python Django</h1>

[TOC]

To Do:
* Project Structure
    * REST App
    * App
* Working: Re-phrase
* Django Form
* UUID


Source:
* https://docs.djangoproject.com/en/1.11/contents/
* https://docs.djangoproject.com/en/1.11/topics/
* https://www.ibm.com/developerworks/library/os-django/index.html
* https://www.edureka.co/blog/django-tutorial/

# Intro
* Django is an open source Web development framework for the Python
* Designed to be loosely coupled and tightly cohesive, meaning that different parts of the framework, while connected to one another, are not dependent on one another
* DRY principle

## Why should we use Django
* modular
* ease the administration by auto-generated web admin
* pre-packaged APIs
* template system to avoid code duplication
* enables to define URL for gives function
* seperates business logic from HTML
* everything is in python


# MVC Architecture
* MTV - Model, Template, View
* Similar to MVC

## Models
* Describes database schema & data structure


### Fields

- BinaryField
- BigAutoField
- BigIntegerField
- CharField
- DateField
- DateTimeField
- DecimalField
- DurationFields
- EmailField
- IntegerField
- BooleanField
- TextField
- ImageField
- FileField
- FilePathField
- FloatField
- GenericIPAddressField
- AutoField

- ForeignKey
    - ManytoOne solution
- ManyToMany
- OneToOne

- SlugField
- TimeField
- URLField
- UUIDField

#### Field Options
- blank
- null
- primary_key
- max_length
- choices
- validators
- db_columns
- db_index
- db_tablespace
- default
- editable
- help_text
- error_messages
- auto_now
- auto_now_add
- unique
- unique_for_date
- unique_for_month
- unique_for_year
- verbose_name


## Views
* Same as Controller in MVC
* Controls what a user sees
* it retrieves data from appropriate model, executes any calculation on data and pass it to template
* 5 Module Name: HttpResponse, template.render(templatename),from django.shortcuts import render(req,temp_name,context), get_object_or_404,

## Templates
* Same as View in MVC
* describes how user sees data & info
* describes how tha data recieved from views should be changed/formatted for display on the page
    
**Note:**  According to Django the framework + URL config feature itself is known as **Controller.**
    
![arch](https://cdn.edureka.co/blog/wp-content/uploads/2017/08/Architecture-Django-Tutorial-Edureka-1.png)
    
# Project Structure
```HTTP
                             Project (just a container)/
                             |  
                             |-----project/
                             |     |--__init__.py 
                             |     |--settings.py
                             |     |--urls.py
                             |     └--wsgi.py
                             |
                             |-----app1/  
                             |  
                             |  
                             |  
                             |-----app2-RESTful/  
                             |  
                             |  
                             |  
                             |-----manage.py  
                             |  
                             |  
                             |  
                             └-----db.sqlite3  
```

* Project: main project package
    * settings.py: python module (module level) represents django settings
    * urls.py: represents site-wide urls configuration (includes apps also)
    * wsgi.py: Web-server-gateway-interface: djangos's primary deployement platform
        * wsgi.py gets created on "startproject"
        * contains "application" callable & "DJANGO_SETTINGS_MODULE" django setting eviroment variable
            * DJANGO_SETTINGS_MODULE: locates setting file, default: project_name.settings.py
            * application: used by server to communicate with code, default: get_wsgi_application()
* App1
* App2- REST-ful

## WSGI: Web Server Gateway Interface
* an interface between web server & application
* contains some statements, set of rules
* its not a software/library/framework
* WSGI compliant server will able to communicate with a WSGI compliant web app
* in WSGI, WSGI application has to be callable & it needs to be given to web server, so web server can call web application whenever it receives a request

## Rename Django Project
- Your django project structure
```
ProjectName/
         manage.py 
         ProjectName/ 
                 __init__.py 
                 settings.py 
                 urls.py 
                 wsgi.py
```

- changes required at 4 places
    - settings.py
```
ROOT_URLCONF = 'NewProjectName.urls'
WSGI_APPLICATION = 'NewProjectName.wsgi.application'
```
    - wsgi.py
```
os.environ.setdefault("DJANGO_SETTINGS_MODULE", "NewProjectName.settings")
```
    - manage.py
```
os.environ.setdefault("DJANGO_SETTINGS_MODULE", "NewProjectName.settings")
```


# Workflow

1. runserver --> web-server gateway interface WSGI--> DJANGO_SETTING_MODULE env var -->by default project.Setting.py (site folder) --> ROOT_URLCONF --> url.py (site url file location) -->

2. Browser --> URL --> DNS + PortNo from application (protocol based)--> IP + port --> http request--> Server -->web-server gateway interface WSGI--> DJANGO_SETTING_MODULE env var -->by default project.Setting.py (site folder) --> ROOT_URLCONF --> url.py (site url file location) --> urlpattern --> url scanning --> matched view --> model + http response + template --> web page

## django-admin.py Vs manage.py
* Django-admin.py: It is a Django's command line utility for administrative tasks.
* Manage.py: It is an automatically created file in each Django project. It is a thin wrapper around the Django-admin.py.

### Uses
#### Clean Database
```bash
python manage.py flush
```

#### Load initial data / fixtures
- src: https://coderwall.com/p/mvsoyg/django-dumpdata-and-loaddata

```bash

#prerequisites- <app_dir>/<fixtures>/<fixture_file.json>
#else provide fixture files path
python manage.py loaddata <fixture_file_name>
```

#### dump data / save DB data
- src: https://coderwall.com/p/mvsoyg/django-dumpdata-and-loaddata

```bash
#whole db
python manage.py dumpdata > [db.json]

#app wise
python manage.py dumpdata [app_name] > [app.json]

#table/model wise
python manage.py dumpdata [app.model (in small)] > [app_model.json]

#exclude some table
python manage.py dumpdata --exclude [app.model (in small)] > [db.json]

#specify indentation
python manage.py dumpdata --indent 4 > [db.json]

#specify output format
python manage.py dumpdata --format [json/xml/yaml] > [db.json]


#backup whole db fresh (without any Integrity Issue)
python manage.py dumpdata --exclude auth.permission --exclude contenttypes > db.json
```

#### Check production readyness
```bash
python manage.py check --deploy 
```

#### Run Dev server
```bash
python manage.py runserver 0.0.0.0:8000
```

#### makemigrations into files
```bash
python manage.py makemifrations <app_name>
```

#### migrate changes into db
```bash
python manage.py migrate
```

#### makemigrations into files
```bash
python manage.py makemifrations <app_name>
```


#### Clean Migration Files

# Features
* Admin Interface (CRUD: Create, Retrieve, Update, Delete)
* Templating
* Form Handling
* Internationalization
* Session, User management, role-based permissions
* ORM (Object-Relational Mapping)
* Testing Framework
* Best Documentation

# Database
* site folder
* setting.py
* DATABASES
* fill dict entries
    * ENGINE: type of db
        * django.db.backends.sqlite3
        * django.db.backends.mysql
        * django.db.backends.postgresql_psycopg2
        * django.db.backends.oracle 
    * NAME: name of database
    * USERNAME(optional)
    * PASSWORD(optional)
    * HOST(optional)

```python

DATABASES = {
    'sqlite3': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
    },
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'employees',
        'USER': 'test',
        
        'HOST': 'localhost',
        'PORT': '',
    }
    
}

```

* (optional) are required in case of DB other than sqlite.

## Set CharSet 
By deafult django uses `latin1`, its better to use unicode `utf8` to support all types of language characters.
So, Put this in settings.py:
```python
DATABASE_OPTIONS = dict(charset="utf8")
```

## MySQL
### Prerequisites
```bash
sudo apt install python-dev libmysqlclient-dev
pipenv install mysqlclient
```

- login to `root`
```bash
sudo mysql -u root -p
```

- create another user & grant all access
```bash
use `<db_name>`
CREATE USER 'dev'@'localhost' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON *.* TO 'dev'@'localhost' WITH GRANT OPTION;
```

- use `dev` user in django

- install workbench (optional)
```bash
sudo apt install  mysql-workbench
```



## Do Django models support multiple-column primary keys?
**Ans** No. Only single-column primary keys are supported. But using the **unique_together** model option we can achieve it.

## Does Django support NoSQL databases?
**Ans** No. Not officially. But can using 3rd party forks like Django non-rel.


## Using Multiple Databases in Django
Different ways of using multiple databases:
* QuerySet's "using" Method
    ```python
    # This will run on the 'default' database.
    Author.objects.all()

    # So will this.
    Author.objects.using('default').all()

    # This will run on the 'other' database.
    Author.objects.using('other').all()
    ```

* Model.save()'s "using" Parameter
        ```python
        choice_one = Choice.objects.get(pk=1)
        choice_one.text = "New Text"
        choice_one.save(using = "Polls_DB")
        ```
* Database Routing
    

## Migrations in Django
* applies changes in models to database tables
    * like deleteing/adding models/fields
* commands
    * **makemigrations**
        * creates migration files as per changes in models
        * inside app-->migrations-->0001_initial.py, contains Migration class with all the operations/changes
        * does not applies changes in DB
        ```python
            python manage.py makemigrations
        ```
    * **migrate**
        * applies migration files to DB
        ```python
            python manage.py migrate
        ```
    * **sqlmigrate**
        * generates sql from migration files
        ```python
            python manage.py sqlmigrate polls_app 0001_initial
        ```



# ORM - Object Relational Mapper
* defines your data model entirely in python
* provides rich & dynamic database-access API

## QuerySet Features:
### Iteration
```python
for e in Entry.objects.all():
    print(e.headline)
```    
### Slicing
### len()
```python
record_count = len(Entry.objects.all()) # will return length of result list
```

###  list()
```python
entry_list = list(Entry.objects.all()) # convert to list
```

### bool()
```python
bool(Entry.objects.filter(age=21)) # same as EXISTS, will return True if there are results
```

## QuerySet Operations:

### Field Lookups
- Parameter passed using "," comma == AND
- For OR, use exclude()
- field__gt: greater than
- field__gte: greater than equal to 
- field__lt: less than
- field__lte: less than equal to
- list slicing [:5] == for starting 5 records
- list slicing some_queryset.reverse()[:5] == for last 5 records
- field__exact
- field__iexact: non-casesensitive match
- field__contains : Entry.objects.get(headline__contains='Lennon'), same as LIKE %Lennon%
- field__icontains : Entry.objects.get(headline__icontains='LeNnon'), same as ILIKE %LenNon%
- field__in : Entry.objects.filter(id__in=[1, 3, 4]), same as SELECT ... WHERE id IN (1, 3, 4);
- field__startswith: Entry.objects.filter(headline__startswith='Lennon')
- field__istartswith: Entry.objects.filter(headline__istartswith='LeNnon')
- field__endswith: Entry.objects.filter(headline__endswith='Lennon')
- field__iendswith: Entry.objects.filter(headline__iendswith='Lennon')
- field__range : Entry.objects.filter(pub_date__range=(start_date, end_date)), same as SELECT ... WHERE pub_date BETWEEN '2005-01-01' and '2005-03-31';
- field__date:
    - Entry.objects.filter(pub_date__date=datetime.date(2005, 1, 1))
    - Entry.objects.filter(pub_date__date__gt=datetime.date(2005, 1, 1))
- year
- month
- day
- week
- week_day
- quarter
- time : Entry.objects.filter(pub_date__time=datetime.time(14, 30))
- hour
- minute
- second
- isnull : Entry.objects.filter(pub_date__isnull=True), same as SELECT ... WHERE pub_date IS NULL;
- regex : Entry.objects.get(title__regex=r'^(An?|The) +')
- iregex : Entry.objects.get(title__iregex=r'^(An?|The) +')

### Custom Lookups & Transforms
- e.g. : title__slug='first-blog'
- TODO

### queries which do not return QuerySet
- get()
    - returns object
    - MultipleObjectsError
- get_or_create()
- update_or_create()
- bulk_create()
- count()
    - return count
- in_bulk()
- iterator()
- latest()
- earliest()
- first()
- last()
- aggreagte()
    - returns dict
- exists()
    - return True/False
- delete()
    -  returns the number of objects deleted and a dictionary with the number of deletions per object type.
- update()
    -  returns the number of objects updated


### all()
- same as SELECT *

### distinct()
- same as SELECT DISTINCT

```python
Author.objects.distinct()
Entry.objects.order_by('blog').distinct('blog') # write parameters in same order in both
Entry.objects.order_by('blog').distinct('blog') # if 'blog' is foreign Model, then by deafult order_by will take it as 'blog__name', so explicity define it as 'blog__id' or 'blog__pk', else will not produce any result
```

### filter()

### select_for_update()
- will lock the row(s) till end of transaction

### raw()
- raw(raw_query, params=None, translations=None)

### F() 
- for updating (increment/decrement) column value without fetching the current value in python memory 

```python
from django.db.models import F

User.object.filter(pk=1).update(salary = F('salary') + 1000) # here F is usefull
```

### order_by()
```python
User.objects.filter(age=21).order_by('-salary', 'name') # negative salary means in descending order
User.objects.filter(age=21).order_by('?') # random order (expensive)
User.objects.order_by('id') 
```

### exclude()
```python
Entry.objects.exclude(pub_date__gt=datetime.date(2005, 1, 3)) # __gt: greater than
```                      

### annotate()
```python
from django.db.models import Count

u = User.objects.annotate(Count('
```

### reverse()
- to reverse the order

### values()
- returns dictionary object instead list query result

```python
Blog.objects.values()
Blog.objects.values('id', 'name')
```

### values_list()
- same as values() but returns tuple

### extra()
- extra(select=None, where=None, params=None, tables=None, order_by=None, select_params=None)
- Sometimes, the Django query syntax by itself can’t easily express a complex WHERE clause. For these edge cases, Django provides the extra() QuerySet modifier — a hook for injecting specific clauses into the SQL generated by a QuerySet.

### only()
- opposite to defer
- name those, which should not get deferred except rest

### defer()
- to defer some fields from a large data base
- passing field to it will not load those columns in queryset from DB, 
- but we can access to field if we need by calling 
- we can never defer pk

### dates()

### datetimes()

### none()
- returns null queryset 
- instance of EmptyQuerySet

### union()
- same as SELECT * FROM TABLE1 UNION SELECT * FROM TABLE2
- queryset1.union(queryset2)

### intersection()

### difference()

### select_related()
- returns Foreign key related objects without hitting database

```python
#Hits the database.
e = Entry.objects.get(id=5)

#Hits the database again to get the related Blog object.
b = e.blog


#Hits the database.
e = Entry.objects.select_related('blog').get(id=5)

#Doesn't hit the database, because e.blog has been prepopulated
#in the previous query.
b = e.blog
```

### prefetch_related()
- To solve the `1 + N` problem in all types of ORM
    - after Django 1.4

### using()
- for choosing databse for the queryset

## `1 + N` Problems
TODO


# Models

## Query Manager
- A class
- An interface through which database query operations are performed to Django models
- by default Manager for each Model is **objects**
- e.g. Questions.**object**.all()

### Manager names
- if you want to rename **objects**
- e.g.

```python
from django.db import models

class Person(models.Model):
    #...
    people = models.Manager()

#Uses    
Person.objects.all()    #AttributeError  
Person.people.all()    
```

### Custom Manager
- if you want to define some more query methods
- Extend models.Manager class
- Code: https://gist.github.com/toransahu/62cd045891656b90f7e18a492e9b81db

## Inheritance style in django?
### Abstract base class
- you define a base class model as a abstract class
    - cannot instantiate
    - cannot use as a regular model
    - cannot create a table in db
- you want to reuse the code for attributes (fields/methods) of the base class into other models
    - each child model will have their own table in db
- e.g.

```python
class CommonInfo(models.Model):
    name = models.CharField(max_length=100)
    age = models.PositiveIntegerField()

    class Meta:
        abstract = True

class Student(CommonInfo):
    home_group = models.CharField(max_length=5)
```
    
### Multi-table Inheritance
* This style is used when subclassing an existing model & need each model to have its own database table
- e.g.

```python
from django.db import models

class Place(models.Model):
    name = models.CharField(max_length=50)
    address = models.CharField(max_length=80)

class Restaurant(Place):
    serves_hot_dogs = models.BooleanField(default=False)
    serves_pizza = models.BooleanField(default=False)
```

- All of the fields of Place will also be available in Restaurant, although the data will reside in a different database table. So these are both possible:

```bash
Place.objects.filter(name="Bob's Cafe")
Restaurant.objects.filter(name="Bob's Cafe")
```

- Note: The inheritance relationship introduces links between the child model and each of its parents (via an automatically-created OneToOneField)

### Proxy models
* You can use this model, If you only want to modify the Python level behavior of the model (means any methods/functions), without changing the models fields
- unlike multi-table inheritance, 
    - if we only want to 
        - add some methods
        - change the default manager
        - change the default ordering
    - and at the same time we don't want to create different tables for each model
    - we can inherit the base model & can define child models as proxy
- e.g.

```python
from django.db import models

class Person(models.Model):
    first_name = models.CharField(max_length=30)
    last_name = models.CharField(max_length=30)

class MyPerson(Person):
    class Meta:
        proxy = True

    def do_something(self):
        #...
        pass
```        

## Extend User Model (Custom User Model)
Some modifications on top of Django's default User Model just to fit our web appplication.  
Source: https://simpleisbetterthancomplex.com/tutorial/2016/07/22/how-to-extend-django-user-model.html

**4 Ways to extend existing User Model:**

### Using a Proxy Model
- Proxy Model: 
    - Model inheritance without creating a new table in database.
    - Used to change the deafult behaviour of an existing model (e.g. methods, ordering by) without affecting exisitng database table
- When used: When you don't need to save extra information in the databse, but want to add extra methods or change query Manager
- Code: https://gist.github.com/toransahu/676d4a8c29b5cbd7737ff1c0a0b4dfc4

### Using One-To-One Link with a User Model (Profile)
- One-To-One Link:
    - one to one relationship between two Django Models
    - Both Models are normal django model
    - implemented using models.OneToOneField(SomeModelHere)
- When Should Use
    - when you need to store some extra information about the exisitng User Model that's not related to authentication process
    - called as User Profile
- How to Use
    - Create User model & Profile model
    - Create OneToOneField in Profile model of User model
    - Define **signals** so our Profile model will be automatically created/updated when we create/update User instances
    - We'll use **post_save** signals for this purpose
    - follow e.g. https://gist.github.com/toransahu/f0bd7313c24605ce92d38a7b09caf4b4

### Creating a Custom User Model Extending AbstractBaseUser
- Custom User Model Extending AbstractBaseUser
    - a new User model inheriting AbtractBaseUser class
    - require extra care & AUTH_USER_MODEL reference in settings.py
    - ideally it should be done in starting of the project
- When Should Use
    - when specific requirement in authentication process
    - e.g. change identification token from username to emailId or mobile_number
- Code: https://gist.github.com/toransahu/4a6314f40676a75b0288953f5c0e8b1c    

### Creating a Custom User Model Extending AbstractUser
- Custom User Model Extending AbstractUser
    - a new User model inheriting AbtractUser class
    - require extra care & AUTH_USER_MODEL reference in settings.py
    - ideally it should be done in starting of the project
- When Should Use
    - when we are perfectly happy with how Django handles the authentication process and we don't want to change anything on it
    - yet we want to add some extra information directly in the User model without having to create extra class like Profile
- Code: https://gist.github.com/toransahu/0ce910494dedb8b9f2774b751f45b559    

Whenever we define custom User Model like this

```python
from django.db import models
from django.contrib.auth.models import AbstractUser

class User(AbstractUser):
    name = models.CharField(max_length=100, blank=True, null=True)
```

we need to specify custom user model in settings.py like
```python
AUTH_USER_MODEL = ‘your_app.User'
```
and we can refer this User model in our code either as
```python
User = get_user_model()
```

or  
```python
User = settings.AUTH_USER_MODEL # use when define a foreign relationship, to make it resuable app
```

### Conclusion
**Proxy Model:** You are happy with everything Django User provide and don’t need to store extra information.  
**User Profile:** You are happy with the way Django handles the auth and need to add some non-auth related attributes to the User.  
**Custom User Model from AbstractBaseUser:** The way Django handles auth doesn’t fit your project.  
**Custom User Model from AbstractUser:** The way Django handles auth is a perfect fit for your project but still you want to add extra attributes without having to create a separate Model.


## class `Meta` Options
TODO:

# Views
## Function Based Generic View
* with template (by rendering)
    ```python
    from django.shortcuts import render

    def home(request):
        return render(request, 'home.html')
    ```
* without template : using HttpResponse
    ```python
    from django.http import HttpResponse

    def home(request):
        return HttpResponse("Hello World")
    ```
* Need to write conditional branch for different HTTP request type like POST, GET, PUT
* Need to provide view method name in URL
* Disadvantage: Cannot extend

## Class Based View
* Module: from django.views import View
* Inherit View class
* Need to define get(), post() like HTTP methods
* Need to provide ClassName.as_view() in URL
* Advantage: Can be extended by sub classes

```python
from django.http import HttpResponse
from django.views import View

class MyView(View):
    def get(self, request):
        # <view logic>
        return HttpResponse('result')
```

## Class Based Generic View
* Module: from django.views.generic import ListView
* Can inherit ListView, TemplateView... class
* No need to define request handler methods
* set model attribute to Model Class
* Need to provide ClassName.as_view() in URL

```python
from django.views.generic import ListView
from books.models import Publisher

class PublisherList(ListView):
    model = Publisher
```

# URLs
## using view function

```python
urlpatterns=[
    path('/',views.home(),name='home'),]
```

## using class based view

```python
urlpatterns=[
    path('/',views.IndexView.as_view(),name='index'),]
```

## including app urls

```python
from django.urls import path, include

urlpatterns = [
        path('', include('home.urls')),]
```

## django 2.0: using path

```python
from django.urls import path, include
```

## django <=1.9: using url

```python
from django.conf.urls import url
```



# Static files
## In Production
* set STATIC_ROOT in settings.py
* run manage.py collectstatic

## In Developement

```python
STATICFILES_FINDERS = (
    'django.contrib.staticfiles.finders.FileSystemFinder',
    'django.contrib.staticfiles.finders.AppDirectoriesFinder'
)

STATICFILES_DIRS = [
    os.path.join(BASE_DIR, 'static'),
    '/var/www/static/',
]
STATIC_URL = '/static/'
```

# Templates
* Contains
    * Markups
        * JS, CSS, HTML, XML
    * django tags
        * Variables/Logic blocks
            * {% extends 'home/base.html' %}
            * {% load static %}
        * Comments
            * {# CSS files#}


#  Middlewares
- Middleware is framework of hooks to Django's request/response processing
- its light and low-level plugin system for making global changes in Django's input/output
- each middleware component in responsible for performing some **specific task**
- Some usage of middlewares in Django is:
    * Session management
    * User authentication
    * Cross-site request forgery protection
    * Content Gzipping, etc.

## Custom Middleware
- a middleware factory (i.e. outer function or a class) is a callable
    - it takes an argument called `get_response`
        - `get_response` might be an actual Django `view` if the middleware is last listed 
        - else, `get_response` might be a **next middleware** 
    - and it returns a `middleware` (or ultimately a `response`)
        - a `middleware` is also a callable which takes an arg called `request`
        - and it returns a `response`

### Function Based Custom Middleware

```python
def simple_middleware(get_response):
    # One-time configuration and initialization.

    def middleware(request):
        # Code to be executed for each request before
        # the view (and later middleware) are called.

        response = get_response(request)

        # Code to be executed for each request/response after
        # the view is called.

        return response

    return middleware
```

### Class Based Custom Middleware

```python
class SimpleMiddleware:
    def __init__(self, get_response):
        self.get_response = get_response
        # One-time configuration and initialization.

    def __call__(self, request):
        # Code to be executed for each request before
        # the view (and later middleware) are called.

        response = self.get_response(request)

        # Code to be executed for each request/response after
        # the view is called.

        return response
```


# Settings
## Place in settings.py
## Separated into production & development environments like
    - base_settings.py
    - dev_settings.py
    - prod_settings.py
    - settings.py

## STRICT SEPERATION FROM CODE
### Python Decouple
- Source: https://pypi.org/project/python-decouple/
- Usage
- Where the settings data are stored?
    - Ini file
    - Env file
- How it works?
    - Understanding the CAST argument


# Signals
Signals are a strategy to allow decoupled applications to get notified when some event occurs.  
Source: https://simpleisbetterthancomplex.com/tutorial/2016/07/28/how-to-create-django-signals.html

- where to create `<signals_module>.py`?
    - anywhere
    - recommended: inside apps

## Built-in Signals
- django.db.models.signals.pre_init:
`receiver_function(sender, *args, **kwargs)`

- django.db.models.signals.post_init:
`receiver_function(sender, instance)`

- django.db.models.signals.pre_save:
`receiver_function(sender, instance, raw, using, update_fields)`

- django.db.models.signals.post_save:
`receiver_function(sender, instance, created, raw, using, update_fields)`

- django.db.models.signals.pre_delete:
`receiver_function(sender, instance, using)`

- django.db.models.signals.post_delete:
`receiver_function(sender, instance, using)`

- django.db.models.signals.m2m_changed:
`receiver_function(sender, instance, action, reverse, model, pk_set, using)`

## Request/Response Signals

- django.core.signals.request_started:
`receiver_function(sender, environ)`

- django.core.signals.request_finished:
`receiver_function(sender, environ)`

- django.core.signals.got_request_exception:
`receiver_function(sender, request)`

## Way of connecting/registering signals

### using `<signal>.connect`
- Need to register signals inside ready() in `AppConfig` class in `<app>.apps.py`
- Need to define `default_app_config = '<app>.apps.<App>Config'` in `<app>.__init__.py`
    - ignore if `'<app>.apps.<App>Config'` is inside `INSTALLED_APPS` insettings.py
- Issues: In django 2.0+, not working fine. Throwing error: `AppRegistryNotReady: Apps aren't loaded yet.`
- e.g.: https://gist.github.com/toransahu/c3870b4ad58bde5a9b9563f7e0883729

### using `receiver()` decorator
- Only need to import signals inside ready() in `AppConfig` class in `<app>.apps.py`
- Need to define `default_app_config = '<app>.apps.<App>Config'` in `<app>.__init__.py`
    - ignore if `'<app>.apps.<App>Config'` is inside `INSTALLED_APPS` insettings.py
- No issues till yet
- e.g.: https://gist.github.com/toransahu/c3870b4ad58bde5a9b9563f7e0883729


# Asynchronous Signals Using Celery
- src
    - https://simpleisbetterthancomplex.com/tutorial/2017/08/20/how-to-use-celery-with-django.html
    - http://docs.celeryproject.org/en/latest/django/first-steps-with-django.html


## Installation
### Task Queue System - Celery

```bash
pip install celery

```

### Message Broker System - RabbitMQ
- src: http://docs.celeryproject.org/en/latest/getting-started/brokers/rabbitmq.html#broker-rabbitmq

```bash
sudo apt install rabbitmq-server
```

## Setup
- no need to define any setup, but can set credentials for rabbitmq-server

## Code

### Enable Celery
- Define celery instance in project level inside celery.py
- Load celery when django starts
    - import the celery instance app to __init__.py in project package

### Write Task
- code: https://gist.github.com/toransahu/d01c7374c5317a908b99ac03cf24cc11

- create tasks.py inside django app
    - celery searches for tasks inside `tasks.py` modules

- either import celery app instance & use
    ```python
    from backend.celery import app
    @app.task
    def foo():
        pass
    ```
- or use `shared_task`
    ```python
    from celery import shared_task
    @shared_task
    def foo():
        pass
    ```    
- set broker_url inside settings.py
    - every celery config variables start with `CELERY_`

    ```python
    CELERY_BROKER_URL = 'amqp://localhost'
    ```

- start rabbitmq
    - starts automatically on boot

    ```bash
    sudo systemctl enable rabbitmq-server
    sudo systemctl start rabbitmq-server
    ```

- start celery worker
    - need to run inside src folder
    - need to be in virtual env

    ```bash
    celery -A project_name worker -l info
    ```

- or create script to start celery
    - cd ethereal-machines-backend/src (where manage.py is)
    - vim start_celery.sh
        - make sure to write #! /bin/bash in first line
    - chmod a+x start_celery.sh
    - start_celery.sh should look like this: https://gist.github.com/toransahu/31874def1bd661db676d0dfe02e1c651


## Celery vs RabiitMQ
- Celery is a queue Wrapper/Framework which takes away the complexity of having to manage the underlying AMQP mechanisms/architecture that come with operating RabbitMQ directly

- Celery is just a very high level of abstraction to implement the producer / consumer of events. It takes out several painful things you need to do to work for example with rabbitmq. Celery itself is not the queue. The events queues are stored in the system of your choice, celery helps you to work with such events without having to write the producer / consumer from scratch.

--------------------------------------------------------------------------------------------------------------------


# State Management
* Session:
* Anonymous Session
* Cookies

## Theory
### Stateless
* Meaning navigating from one web page to another will not retain infos of first one.
* There is no persistence between one request and the next, and there is no way the server can tell whether successive requests come from the same person
* e.g. HTTP, REST

This lack of state is managed using sessions.

## Session
* are a semi-permanent, two-way communication between your browser and the web server.  
* The session framework lets you store and retrieve arbitrary data on a per-site-visitor basis
* It stores data on the server side and abstracts the sending and receiving of cookies
* can be implemented through middleware
* In client side cookies contain a session ID  not the data itself (unless youre using the cookie based backend)

```python
INSTALLED_APPS = [
    'django.contrib.sessions',
    ]

MIDDLEWARE = [
    'django.contrib.sessions.middleware.SessionMiddleware',
    ]
```

### Anonymous Session
* to keep track of data relevant to your visit
* the web server can only record what you did, not who you are

### Enabling the session
* Using middleware
* MIDDLEWARE_CLASSES in setting.py should contain 'django.contrib.sessions.middleware.SessionMiddleware'
* by deafult enabled

### Configuring The Session Engine
* by default stored in database using the model django.contrib.sessions.models.Session
* can be configured to store session data on file system or in cache

### Using Database-Backed Sessions
* need to add 'django.contrib.sessions' to your INSTALLED_APPS setting

### Using Cached Sessions
* for better performance, for making web pages more responsive
* local memory cache backend doesnt retain data long enough to be a good choice
* use third-party like Memcached cache backend, else use file system or DB based session
* two different implementation:
    * Only cache
        * Set SESSION_ENGINE to "django.contrib.sessions.backends.cache"
    * Cache + DB (Persistent)
        * set SESSION_ENGINE to "django.contrib.sessions.backends.cached_db"
        * every write to the cache will also be written to the database
        * use the database if the data is not already in the cache

### Using File-Based Sessions
* have to set the SESSION_ENGINE settings to django.contrib.sessions.backends.file

### Using Cookie-Based Sessions


## Cookies
### What
- An HTTP cookie (web cookie, browser cookie) is a small piece of data that a server sends to the user's web browser. 
- The browser may store it and send it back with the next request to the same server. 
- module: http.cookies

### Why
- Typically, it's used to tell if two requests came from the same browser — keeping a user logged-in, for example. 

### How
- It remembers stateful information for the stateless HTTP protocol.

### Uses:
- Session management
    - Logins, shopping carts, game scores, or anything else the server should remember
- Personalization
    - User preferences, themes, and other settings
- Tracking
    - Recording and analyzing user behavior


## Cache
### Why
- The performance of web sites and applications can be significantly improved by reusing previously fetched resources. 
- Web caches reduce latency and network traffic and thus lessen the time needed to display a representation of a resource. 
- By making use of HTTP caching, Web sites become more responsive.



# Architecture - Django Production Servers

<img src="https://www.sayonetech.com/media/2015/06/18/django-host_.png">

Source : https://www.sayonetech.com/blog/how-host-your-django-project-production-server/#.WgSKV3VL9Xo

## Web Server
- the outermost tier of the Backend(3-tiers)
* Apache, nginx, lighttpd, cherokee
- used as proxy, reverse proxy, load balancer, static data (css, html, images) dispatcher and cache
- it can't talk directly to Django applications

### nginx (Pronounced as: Engine X)

## Application Server
- the middle tier of the Backend(3-tiers)
* Gunicorn, mod_python, mod_wsgi, mod_uwsgi, FastCGI
- is used to handle all dynamic requests, basically based on URL pattern (view call)
- the Interface between the web server and the python app so that the app(or any python framework) understands the incoming requests
- create a Unix socket, and serve responses to nginx via the wsgi protocol - the socket passes data in both directions

### gunicorn (Pronounced as: gee-unicorn)
- inspired from Ruby's Unicorn

## DB
- the third tier of the Backend(3-tiers)
* MySQL/ Postgres/ Other databases 


## Asynchronous Task Queue
### Celery
- Celery is an asynchronous task/job queue based on distributed message passing 
    - requires an external solution to send and receive messages
        - i.e. Message Brokers like RabbitMQ, Redis
    - focused on real-time operation, but supports scheduling as well

### Cron jobs

## Message Broker Solutions
### RabbitMQ
### Redis
### Amazon SQS

## Caching Solution
### Memcached


## Monitoring
When our project is hosted, we need to monitor it using some tools to check its performance, its error logs and  user interactions.We have some tools available for this.

### Graphite 
- Graphite provides real-time visualization and storage of numeric time-series data on an enterprise level.

### Statsd 
- A network daemon that runs on the Node.js platform and listens for statistics, like counters and timers, sent over UDP or TCP and sends aggregates to one or more pluggable backend services (e.g.,Graphite).

### Sentry - logging 
-  Sentry is a modern error logging and aggregation platform.

### New Relic 
- A software analytics tool suite used by developers, ops, and software companies to understand how your applications are performing in development and production.

### Supervisor
- a process control system
- a client/server system 
    - which allows its users to monitor and control a number of process in UNIX-like OS
- similar to `launchd`, `daemontools`, and `runit`
- monitors projects
- starts on boot
- Supervisord starts processes as its subprocesses, and can be configured to automatically restart them on a crash
- accurately shows the up/down times of the processes
- can asign priorities to the processes
- can group the processes

## Stack Flow

- User requests from browser.
- Request reaches Nginx.
- If (request is staic)
    - Nginx serves the request.
- Else if (request is dynamic)
    - Nginx forwards the request to Application server (Gunicorn).
    - Gunicorn receives the request, executes corresponding python (Flask) code.
    - Gunicorn returns the response to Nginx.
- Nginx serves the response to the user.



## Working
You need both Nginx and Gunicorn (or something similar) for a proper Django deployment
The complete answer is both Nginx and Gunicorn handle the request. Basically, Nginx will receive the request and if it's a dynamic request (generally based on URL patterns) then it will give that request to Gunicorn, which will process it, and then return a response to Nginx which then forwards the response back to the original client.



# Deployment - Production Environment

## How to deploy django application in Production
* https://devcenter.heroku.com/articles/getting-started-with-python#introduction
- https://developer.mozilla.org/en-US/docs/Learn/Server-side/Django/Deployment
* DEBUG = False
* change default SECRET_KEY (used for CRSF protection) and hide it somewhere else
* Run manage.py check --deploy (to check the default list of changes mentioned by django)

** checklist ** https://docs.djangoproject.com/en/1.10/howto/deployment/checklist/

## checklist
- in settings
    - must be set properly for Django to provide the expected level of security;
    - are expected to be different in each environment;
    - enable optional security features;
    - enable performance optimizations;
    - provide error reporting.
- or Run manage.py check --deploy
    - to list all the factors listed below
- take care of these things if releasing source code 


## critical settings
- SECRET_KEY
    - Instead of hardcoding the secret key in your settings module, consider loading it from an environment variable or file
    ```python
    import os
    SECRET_KEY = os.environ['SECRET_KEY']


    with open('/etc/secret_key.txt') as f:
        SECRET_KEY = f.read().strip()
    ```
    - avoid committing it to source control

- DEBUG : set to False


## Environment Related Settings
- ALLOWED_HOSTS
    - When DEBUG = False, Django doesn’t work at all without a suitable value for ALLOWED_HOSTS.
    - This setting is required to protect your site against some CSRF attacks
- CACHE
    - change it for production performance otimization
    - default for developement is 'local-memory caching'
    - instead use cache servers like Memcached
        - using  'cached sessions'
        - Cache servers often have weak authentication. 
        - Make sure they only accept connections from your application servers.
- DATABASE
    - Database passwords are very sensitive. Keep them in environment  variable or in file same as SECRET_KEY
    - For maximum security, make sure database servers only accept connections from your application servers.
    - If you haven’t set up backups for your database, do it right now!
- EMAIL_BACKEND and related settings
    - If your site sends emails, these values need to be set correctly.
        - modify the DEFAULT_FROM_EMAIL and SERVER_EMAIL settings
    - By default, Django sends email from webmaster@localhost and root@localhost. 
- STATIC_ROOT and STATIC_URL
    - Static files are automatically served by the development server. 
    - In production, you must define a STATIC_ROOT directory where collectstatic will copy them.
- MEDIA_ROOT and MEDIA_URL
    - Media files are uploaded by your users. They’re untrusted! 
    - Make sure your web server never attempts to interpret them. 
    - For instance, if a user uploads a .php file, the web server shouldn’t execute it.

## HTTPS
- Any website which allows users to log in should enforce site-wide HTTPS to avoid transmitting access tokens in clear. 
- In Django, access tokens include the login/password, the session cookie, and password reset tokens. 
- Note: You can’t do much to protect password reset tokens if you’re sending them by email
- web server must redirect all HTTP traffic to HTTPS, and only transmit HTTPS requests to Django.
    - because: the same session cookie is used for HTTP and HTTPS. 
- Once you’ve set up HTTPS, enable the following settings.
    - CSRF_COOKIE_SECURE
        - Set this to True to avoid transmitting the CSRF cookie over HTTP accidentally.
    - SESSION_COOKIE_SECURE
        - Set this to True to avoid transmitting the session cookie over HTTP accidentally.

## Performance Optimizations
- DEBUG = False
- CONN_MAX_AGE
- TEMPLATES
    - Enabling the cached template loader often improves performance drastically, as it avoids compiling each template every time it needs to be rendered. 

## Error Reporting
- LOGGING
    - Review your logging configuration before putting your website in production, and check that it works as expected as soon as you have received some traffic
- Customize the default error views
    - Django includes default views and templates for several HTTP error codes. You may want to override the default templates by creating the following templates in your root template directory: 404.html, 500.html, 403.html, and 400.html.

# Testing
* Class level testing for each app

    ```python
    from django.test import TestCase

    class QuestionModelTests(TestCase):
        def test_was_published_recently_with_future_question(self):
            #do something
            self.assertIs(future_question.was_published_recently(), False)
    ```

## Run Test Cases
```bash
python manage.py test appname
```

# Security

## CSRF - Cross Site Request Forgery

### Why CSRF?
- CSRF attack happens in presence of state
- It really boils down to the browsers ability to automatically present login credentials for any request by sending along cookies. If a session id is stored in a cookie the browser will automatically send it along with all requests that go back to the original website. This means that an attacker doesn't actually have to know authentication details to take an action as the victim user. Rather, the attacker just has to trick the victims browser into making a request, and the credentials to authenticate the request will ride along for free.

### Is it required in REST
- No, it will be useless piece of code
- because REST is **stateless** at client-side
- a cookie-less REST endpoint is completely immune from CSRF attacks
- if there is cookie used for authentication, then we need CSRF protection
- HTTP/BasicAuthentication will also need CSRF protection
- also, if any app uses any tech to store state of app at clientside, then its not a RESTful app
- src: https://security.stackexchange.com/questions/166724/should-i-use-csrf-protection-on-rest-api-endpoints




# Django REST Framewok

Django REST framework "djangorestframework" is powerful & flexibal toolkit for creating web APIs.
- https://stackoverflow.com/questions/671118/what-exactly-is-restful-programming

#### Some reasons you might want to use REST framework:
* The Web browsable API is a huge usability win for your developers.
* Authentication policies including packages for OAuth1a and OAuth2.
* Serialization that supports both ORM and non-ORM data sources.
* Customizable all the way down - just use regular function-based views if you don't need the more powerful features.
* Extensive documentation, and great community support.

## REST API
* Representation State Transfer
* An architectural pattern for creating an API that uses HTTP as its communication method
* for designing network based application
* Resource: 
    * If we have endpoint/URI(URL or URN), lets say https://127.0.0.1/coders then we have resource. Here coders is a resource.
    * Its nothing new, we already used to make URLs that way
* Representation:
    * When a client makes a GET request to coders/toran/ client gets following JSON response
    ```JSON
    {
    "nickname": "toran",
    "powerLevel": 5
    }
    ```
    * so, this is representation in the form of JSON having metadata
    * representation also could be XML, HTML
    * the same applies when a client sends a request which contains a 'coder' data, its sends representation
* Representational State:
    * like browsing the web
    * a HTML page is a representation of a resource at current state (or current data) of that resource.
    * When we submit a form, we just send a representation back to the server
* Representational State Transfer
    * a client and server exchange representations of a resource, which reflects its current state or desired state.
    * So, REST is a way for two machines to transfer the state of a resource via representations.


## HTTP Request Methods (HTTP verbs)
HTTP defines a set of request methods to indicate the desired action to be performed for a given resource

- **GET**
    - The GET method requests a representation of a specified resource.
    - GET request should only used for data retrieval. (But can also be used for submit/posting/sending data)
    - a resource is mentioned in URL.
- **POST**
    - Used to modify/update an existing entity of a specified resource.
        - Do mention the object/entity of the resource in the URL to update
        - we should use PUT and PATCH for update
            - PUT would create a new unwanted resource when the resouce doesn't exists while updating that particular resource
            - PATCH is perfect for partial updation
        - But there is no restrictions using POST for updates

    ```HTTP
    POST /questions/<existing_question> HTTP/1.1
    Host: www.example.com/
    ```    
    - Used to submit a new entity/data to a specified resource.
        - Do not mention the object/entity of the resource in the URL while creating it. Otherwise it will give "Resource Not Found" error.
    ```HTTP
    POST /questions/ HTTP/1.1
    Host: www.example.com/
    ```    
    - Causes change in state of the resource
    - Use this if you want server to let the name, the URL object while creating a new one
    - Two simultaneous POST requests works fine (lets say, 1st request is updating some part & 2nd request is updating other part of an object)  
    - The `UPDATE` performed by the POST method might not result in a resource that can be identified by a URI.
    
- **PUT**
    - Used to create a new resource entity or **overrite** (Completely replaces) the existing one.
    - For a new resource entity:
        ```HTTP
        PUT /questions/<new_question> HTTP/1.1
        Host: www.example.com/
        ```
    - To overrite an existing one
        ```HTTP
        PUT /questions/<existing_question> HTTP/1.1
        Host: www.example.com/
        ```    
    - Usefull when you know the name of the entity/object
    - Use this if you want to name the URL object while creating a new one
    - PUT is idempotent, so if you PUT the same object twice, it has no effect (will overrite)
    - Can create or update an object with the same URL  
    
    
- **DELETE**
    - Deletes/destroyes a specified resource object/entity/record.  
    
    
- **PATCH**
    - Used to make partial modification to an existing resource object/entity.
    - Works differently than POST & PUT for update
    - Need to have URL object known
    ```HTTP
    PATCH /users/1 HTTP/1.1
    Host: www.example.com
    Content-Type: application/example
    If-Match: "c0b42b66e"
    Content-Length: 120
    [changes]
    ```
    where [changes] could be JSON/XML like {email:'toran.sahu@yahoo.com'}  
    
    
- **HEAD**
    - Ask for the response same as GET but without response/message body.  
    
    
- **OPTIONS**
    - Used to describe the communication option for the target resource  
    
    
- **CONNECT**
    - Establishes a tunnel to the server identified by the target resource  
    
    
- **TRACE**
    - Performs message loop-back test along the path to the target resource  


**Note:** There is a very common confusion in terminology. **"Resource"**
- In URI "app/questions/1" here "1" is also know as resource and at the same time "questions" is also know as resource.
- Some people around the globe also use "1" as record/entity & "questions" as resource.
- We could generalize "1" as "resource object" and "questions" as "resource class"

## HTTP Response Codes
- 200 (Ok)
- 201 (Created)
- 204 (No Content)
- 304
- 404
- 501 (Not Implemented)


## Serializers
* Module: from rest_framework import serializers
* Provides a way to serialize & deserialize Model instances into representations like JSON.
* **Serialization** is mechanism of converting the state of an object into byte-stream, which can be displayed, stored.
* **Deserialization** is reverse mechanism of serialization.

**Note:** In django its very similar to Django Form class and includes similar validation flags on the various fields, such as required, max_length and default.

### Implementations 
* Inherit classes
    * serializers.Serializer
        * need to write all the fields mentioned in Model (only those, which we want to use here)
        * need to define create() & update() method to create/update new Model instance from validated data (representaion/JSON)
    * serializers.ModelSerializer
        * Inside Meta class mention
            * model inside Meta class; model = Snippet i.e. Class
            * fields = ('id', ....,'title') i.e. tuple
        * Automatically implements default create() and update() methods
        - **Note**: If we want to include `url` in fields, then the base_name (in case of routers) in urls.py should same as the name of Model in lower case, alternatively don't mention base_name
    * serializers.HyperlinkedModelSerializer
        - The only difference is, as in citation you included, that primary and foreign keys are represented by URLs that point to those resources, instead of just actual key values.
        - The benefit is that you will not have to construct resource URLs in your frontend when you want to retrieve related objects.
    
### Relations
- src: http://www.django-rest-framework.org/api-guide/relations/#serializer-relations

### Writable Nested Serializers
- scr: http://www.django-rest-framework.org/api-guide/relations/#writable-nested-serializers
- code: https://gist.github.com/toransahu/221371c981c20f0b9c645019a53b90c7
- by default django does not provides write access in case of nested model objects & their model serializers
- strategy
    - create 2 models
    - assign M2M/Foreign key field in one model
    - write serializers for both the models
        - keep foreign model serializers normal/default
        - for other model serializer write custom code 
            - override create() method
                - handle foreign field data explicitly
                - create post instance from data
                - iterate over list value of foreign field
                    - create instance of image
                    - append image instance to post instance's foreign field
            - override update() method
                
    - write normal viewset for only one : i.e. posts (both is optional)
- Issues faced:
    - if nested fields are char
        - if posting as application/json from django form : works fine
        - if posting as multipart/form-data from django form: validation fails for required fields
            - means data received is empty
        - works fine with python code only iff data & files both are provided
    - if nested fields are image
        - cannot post using django form
        - able to post using custom form: https://github.com/toransahu/multiple-file-upload
        - able to post using python code

### class `Meta` Options
TODO:

#### Misc
- Note:
    1. after serializer.is_valid() we can't save serializer if we have already accessed serializer.data; to avoid this, access serializer.validated_data
    2. custom create & update in serializer - writable nested serializers
    3. datefield attribute: auto_now vs auto_now_add
        - auto_now: 
            - Automatically set the field to now every time the object is saved
            - Useful for "last-modified" timestamps
            - cannot be overriden

        - auto_now_add
            - Automatically set the field to now when the object is first created
            - Useful for creation of timestamps
            - cannot be overriden
    
- Postman:
    - nested: https://medium.com/@darilldrems/how-to-send-arrays-with-get-or-post-request-in-postman-f87ca70b154e

- Try:
    - https://github.com/beda-software/drf-writable-nested
    - https://github.com/alanjds/drf-nested-routers
    - [Base64 ImageField](https://gist.github.com/yprez/7704036)
        
## Views
- Function Based View    
    - Using normal functions like in Django (without using any rest_framework feature)
        - Modules: 
            ```python
            from django.views.decorators.csrf import csrf_exempt
            from django.http import HttpResponse, JsonResponse
            from rest_framework.renderers import JSONRenderer
            from rest_framework.parsers import JSONParser
            ```
        - Approach:
            - write function with conditional branching for different http request methods
            - write a _list function for listing all records (GET) & submiting a record (POST)
            - write a _detail function for fetching, modifying or destroying a specific record by pk, ID or Name
            - use JSON response & parser
        - use @csrf_exempt decorator for safety
        - code: https://gist.github.com/toransahu/1bad12b87dcd160c0de0d29d218d9bf6 
    - Using @api_view() decorator
        - Modules: 
            ```python
            from rest_framework import status
            from rest_framework.decorators import api_view
            from rest_framework.response import Response
            ```
        - Approach:
            - write function with conditional branching for different http request methods
            - write a _list function for listing all records (GET) & submiting a record (POST) 
            - write a _detail function for fetching, modifying or destroying a specific record by pk, ID or Name
            - decorate with @api_view() with parameters like ['GET'], ['GET', 'POST'], ['GET', 'PUT', 'DELETE'] etc
            - By default @api_view() takes GET method if nothing is mentioned
        - code: https://gist.github.com/toransahu/5c99704ec721e461b5f8fa67776a6d74 
- Class Based View
    - By Inheriting APIView class
        - Modules: 
            ```python
            from rest_framework.views import APIView
            from rest_framework.response import Response
            from rest_framework import status
            from django.http import Http404
            ```
        - Approach:
            - write classes and define request handler methods in name of http request method for each http request method 
            - write a List class for listing all records (GET) & submiting a record (POST) 
            - write a Detail class for fetching, modifying or destroying a specific record by pk, ID or Name
        - similar to Django's "View" class
        - Note
            - request handler methods receives REST's Request instance instead django's HttpRequest instance
            - request handler methods may return REST's Response instance instead django's HttpResponse instance
        - set few attributes like
            - authentication_classes = (authentication.TokenAuthentication,)
            - permission_classes = (permissions.IsAdminUser,)
        - code: https://gist.github.com/toransahu/bcdb1a6beb5da0475c8c056837da940f
    - Using mixins
        - Modules:
            ```python
            from rest_framework import mixins
            from rest_framework import generics
            ```
        - Approach:
            - write classes and inherit `generics.GenericAPIView` & mixins as per use
            - write a List class and inherit mixins.ListModelMixin, mixins.CreateModelMixin, generics.GenericAPIView
            - write a Detail class and inherit mixins.RetrieveModelMixin, mixins.UpdateModelMixin, mixins.DestroyModelMixin, generics.GenericAPIView
            - base class providescore functionality & mixin classes provides actions like .list(), .create(), .retrieve(), .update() and .destroy()
        - Code: https://gist.github.com/toransahu/dfc2666307c1628042b99edaba630c07
    - Using generic class-based views
        - Modules:
            ```python
            from rest_framework import generics
            ```
        - Approach:
            - write List class and inherit generics.ListCreateAPIView
            - write Detail class and generics.RetrieveUpdateDestroyAPIView
        - Code: https://gist.github.com/toransahu/ab21d8bf46f45616ccb9285dbd0b201a
        
    - Using ViewSet
        - Modules:
            `from rest_framework import viewsets`
        - Approach:
            - Only need to write a single class, named `ModelNameViewSet` and inhert `viewsets.ModelViewSet`
            - facilitates router for URL writing
        - Advantage:
            - provides create, retrieve, update, and destroy in a single Class def
            - DRY View code
            - DRY URL code
            - can also add custom endpoints as per our need, apart from regular create, retrieve, update, and destroy endpoint provided by ViewSet
         - Code: https://gist.github.com/toransahu/c7d43776065aa6fda05d7389133c68f9
         
### Custom/Disable Request Methods in ViewSet
- By default ViewSets provides All the requests methods
- this technique will give power to override,disable those methods
- to do this use `mixins` with `viewset.GenericViewSet`, or override methods of ViewSet class
- url: https://gist.github.com/toransahu/e02fc30cd0e55e968971c46e59862acb


### mapping for views from ViewSet using `as_view()`
- syntax
    - `{<method>:<action>}`
- patterns
    - {'get': 'list'}
    - {'get': 'retrieve'}
    - {'post': 'create'}
    - {'put': 'update'}
    - {'patch': 'partial_update'}
    - {'delete': 'destroy'}
    
### adding custom routes/action to the existing ViewSet
- https://gist.github.com/toransahu/95781bc23f39192276d011d0aa990470
- http://www.django-rest-framework.org/api-guide/routers/#customizing-dynamic-routes

## URLs

- if using include(<some_other_url.py>)
    - dont provide namespace 
    - if providing namespace inside include
        - define app_name = <appname> in app/urls.py
        
### Routers
REST framework adds support for automatic URL routing to Django, and provides you with a simple, quick and consistent way of wiring your view logic to a set of URLs.

```python
from django.urls import path
from .views import BlogViewSet
from rest_framework.routers import DefaultRouter


router = DefaultRouter()
router.register('', BlogViewSet, base_name='blogs')

urlpatterns = router.urls
```

- **Note:**
    - **Try to keep `base_name` same as Model name, because `view_name` like blog-detail, blog-list comes from Model & not from app's name**
    - **when we create custom actions (similar to -list, -detail) in any View using @detail_route(), we access that action using `base_name` in serializers.** 
    - alternatively remove base_name


### actions using base_name:
- `<base_name>-list`
- `<base_name>-detail`
- `<base_name>-<any_custom>`


### how to use namespace (provided in url patterns)
- using `from django.urls import reverse`
    - `reverse(<namespace>:<base_name>-<action>` or
    - `reverse(<namespace>:<model_name>-<action>`

### adding custom routes/action urls to the existing Router or urlpatterns
- https://gist.github.com/toransahu/95781bc23f39192276d011d0aa990470


## API Versioning
- [Source](http://www.django-rest-framework.org/api-guide/versioning/)
- [e.g.](https://gearheart.io/blog/api-versioning-with-django-rest-framework/)
- Its always a good idea to version your API so that you can make changes in your API without disturbing your current clients.
- e.g. http://127.0.0.1:8000/api/v1/blogs/

### Configurations
- settings.py  

```python
REST_FRAMEWORK = {
    'DEFAULT_VERSIONING_CLASS': 'rest_framework.versioning.NamespaceVersioning'
}
```

- urls.py

```python
urlpatterns = [
    path('admin/', admin.site.urls),
    path('api/v1/blogs/', include('blogs.urls', namespace='v1')),
]
```

- blogs/urls.py

```python
app_name = 'blogs'

router = DefaultRouter()
router.register('', BlogViewSet, base_name='blogs')

urlpatterns = router.urls
```

### Uses
- Once you have set versioning, django will be able to provide value of `request.version` else it will be `None`
- so, apply conditions (`if/else`) in View or serializers
    - if there are changes in fields, then use versioning in serializers
    - else, if there are only changes in some functionalities, (which current client cannot consume), then use versioning in veiws only, like:
        ```python
        def get_serializer_class(self):
            if self.request.version == 'v1':
                return AccountSerializerVersion1
            return AccountSerializer
        ```

## Allow CORS (Cross Origin Resource Sharing) in DRF

- [Source1](https://www.techiediaries.com/django-cors/)
- [Source2](https://github.com/ottoyiu/django-cors-headers)

### Using Custom Middleware class
- need to define for each app
- `python manage.py startapp app`
- create `app/cors.py` and write
    
    ```python
    class CorsMiddleware(object):
    def process_response(self, req, resp):
        response["Access-Control-Allow-Origin"] = "*"
        return response
    ```
- `MIDDLEWARE_CLASSES = ['app.CorsMiddleware']`

### Using package `django-cors-headers`
- works site-wide
- `pipenv install django-cors-headers`
- in `settings.py` `INSTALLED_APPS = ['corsheaders']`
- `MIDDLEWARE_CLASSES = ['corsheaders.middleware.CorsMiddleware',]`, keep in top as possible as
- Allow using any one
    - `CORS_ORIGIN_ALLOW_ALL = True`
    - OR `CORS_ORIGIN_ALLOW_ALL = False` `CORS_ORIGIN_WHITELIST = ['http//:localhost:8000',]`
- also set `ALLOWED_HOSTS = ['192.168.1.121']`
- and run server like `python manage.py runserver 192.168.1.121:8000`


## Creating Schema from API
- provides all the details about api endpoint present in site-wide urls
    - will show all the endpoints
        - actions
            - fields
    - if any authentication is needed
        - it will show schema accordingly; if not authenticated, it will show that much api endpoints only
- need to configure in site-wide urls.py
- source: http://www.django-rest-framework.org/api-guide/schemas/
- `pipenv install coreapi`

```python
from rest_framework.schemas import get_schema_view

schema_view = get_schema_view(title="Server Monitoring API")

urlpatterns = [
    url('^<dollor_sign>', schema_view),
    ...
]
```

## Setting Media URL & ROOT
### Site Wide
### App Based
- define MEDIA_URL & MEDIA_ROOT in settings.py

```python
# Media files
# https://timmyomahony.com/blog/static-vs-media-and-root-vs-path-in-django/

# the relative browser URL to be used when accessing our media files in the browser
MEDIA_URL = 'media/'

# the absolute path to the folder that will hold our user uploads
# to get absolute path without hardcoding
ENV_PATH = os.path.abspath(os.path.dirname(__file__)) + os.sep + os.pardir
MEDIA_ROOT = os.path.join(ENV_PATH, 'media/')
```
- add following code in app/urls.py  

```python
# adding media url
from django.conf import settings # from backend.settings import DEBUG
from django.conf.urls.static import static

# If developement env
if settings.DEBUG is True:
    urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
```    

- want to set upload_to directory dynamically:
    - code: https://gist.github.com/toransahu/8f9407250cee7a729473335bdd7a3f3b
    - here comes, signal things, pre_save, post_save
    

## Permission

### request methods level permissions (in ViewSet)
- this needs when "a user must post only or admin must post only" type of requirements comes 
- url-view: https://gist.github.com/toransahu/e02fc30cd0e55e968971c46e59862acb
- url-permission: https://gist.github.com/toransahu/c40b625165a395fabf772700f3ab2e04

### objects level permission
- TODO

### Exception/Http response
When the permissions checks fail either a "403 Forbidden" or a "401 Unauthorized" response will be returned, according to the following rules:

- The request was successfully authenticated, but permission was denied. — An HTTP 403 Forbidden response will be returned.
- The request was not successfully authenticated, and the highest priority authentication class does not use WWW-Authenticate headers. — An HTTP 403 Forbidden response will be returned.
- The request was not successfully authenticated, and the highest priority authentication class does use WWW-Authenticate headers. — An HTTP 401 Unauthorized response, with an appropriate WWW-Authenticate header will be returned.


## Authentication

Source: http://www.django-rest-framework.org/api-guide/authentication/

### Basic Auth
- module:
    `from rest_framework.authentication import  BasicAuthentication`
- By default used in DRF, whether you mention it in `settings.py` or `views.py` or not
- is only suitable for testing purpose, don't use in production
- if using in production
    - you need to stick to Django Admin Login form page, can't use JSON
    - need to be `HTTPS`
   

### Session Auth
- module
    - `from rest_framework.authentication import SessionAuthentication`
- TODO


### Token Auth

Source: https://stackoverflow.com/questions/14838128/django-rest-framework-token-authentication

- module
    - `from rest_framework.authentication import TokenAuthentication
- Prerequisites
    - add 'rest_framework.authtoken' to INSTALLED_APPS in settings.py
    - mention TokenAuthentication class in
        - views or
            - function based
            
            ```python
            @authentication_classes([TokenAuthentication, ])
            def abcd-detail():
                pass
            
            ```
            
            - class based
            
            ```python
            class Abcd():
                authentication_classes = [TokenAuthentication, ]
            
            ```
                      
        - settings.py
        ```python
        REST_FRAMEWORK = {
            'DEFAULT_VERSIONING_CLASS':
            'rest_framework.versioning.NamespaceVersioning',
            'DEFAULT_AUTHENTICATION_CLASSES': (
                # 'rest_framework.authentication.BasicAuthentication',
                # 'rest_framework.authentication.SessionAuthentication',
                'rest_framework.authentication.TokenAuthentication',
            ),
        }
        ```
- Obtain Token
DRF provides a view which returns a token on correct username & password.
    - include following in urls.py
    
    ```python
    from rest_framework.authtoken.views import obtain_auth_token

    urlpatterns = [path('api-auth-token/', obtain_auth_token),]
    ```
    - call the view as:
    `http POST 127.0.0.1:8000/api-token-auth/ username='admin' password='whatever'`
    
    - will get token like:
    ```json
    {
        "token": "blah_blah_blah"
    }
    ```
- Use the Token in API call
    - put the following in Header
     ```
     key: Authorization  value: Token token_value
     ```
     Please mind the space between Token & token_value
     
    `http GET 127.0.0.1:8000/whatever 'Authorization: Token your_token_value'`
    

### JWT (JSON Web Token)
- src: http://getblimp.github.io/django-rest-framework-jwt/
- quick replacement of Default Token Auth
- Basic Changes Needed:
    - pip install djangorestframework-jwt
    - add in REST_FRAMEWORK setting
        `'DEFAULT_AUTHENTICATION_CLASSES': ( 'rest_framework_jwt.authentication.JSONWebTokenAuthentication', )`
        
    - add view in url
        ```python
        from rest_framework_jwt.views import obtain_jwt_token
        #...

        urlpatterns = [
            '',
            # ...

            url(r'^api-token-auth/', obtain_jwt_token),
        ]
        ```

- jwt setting variables

```python
JWT_AUTH = {
    'JWT_ENCODE_HANDLER':  
    'rest_framework_jwt.utils.jwt_encode_handler',

    'JWT_DECODE_HANDLER':  
    'rest_framework_jwt.utils.jwt_decode_handler',

    'JWT_PAYLOAD_HANDLER':  
    'rest_framework_jwt.utils.jwt_payload_handler',

    'JWT_PAYLOAD_GET_USER_ID_HANDLER':  
    'rest_framework_jwt.utils.jwt_get_user_id_from_payload_handler',

    'JWT_RESPONSE_PAYLOAD_HANDLER':  
    'rest_framework_jwt.utils.jwt_response_payload_handler',

    #'JWT_SECRET_KEY': settings.SECRET_KEY,  #will take from settings.py by default  
    'JWT_GET_USER_SECRET_KEY': None,  
    'JWT_PUBLIC_KEY': None,
    'JWT_PRIVATE_KEY': None,
    'JWT_ALGORITHM': 'HS256',
    'JWT_VERIFY': True,
    'JWT_VERIFY_EXPIRATION': True,
    'JWT_LEEWAY': 0,
    'JWT_EXPIRATION_DELTA': datetime.timedelta(seconds=300),
    'JWT_AUDIENCE': None,
    'JWT_ISSUER': None,

    'JWT_ALLOW_REFRESH': True,  #allowing it to refresh
    'JWT_REFRESH_EXPIRATION_DELTA': datetime.timedelta(days=7),

    'JWT_AUTH_HEADER_PREFIX': 'Token',
    'JWT_AUTH_COOKIE': None,

}
```
        
### django-rest-auth (Register, Login, Logout, Reset, Change..)
- src
    - http://django-rest-auth.readthedocs.io/en/latest/api_endpoints.html
    - https://michaelwashburnjr.com/django-user-authentication/
- not recommanded, is not completely RESTful
    - have issues with `password/reset` & `password/reset/confirm/`
- depends on `django-allauth` for email things


### djoser
- src: http://djoser.readthedocs.io/en/stable/sample_usage.html
- djoser uses following settings for email configuration (which is also used by django's default mail module
    - `from django.core.mail import send_mail`
    
    ```python
    CONFIG_PATH = os.path.join(ENV_PATH, '../configs/')

    EMAIL_USE_TLS = True
    #EMAIL_USE_SSL = True  #Use any one from TLS, SSL
    EMAIL_BACKEND = 'django.core.mail.backends.smtp.EmailBackend'  #default one, production
    #EMAIL_BACKEND = 'django.core.mail.backends.console.EmailBackend'  #for development
    EMAIL_HOST = 'smtp.gmail.com'
    with open(os.path.join(CONFIG_PATH, 'email_pwd')) as f:
        EMAIL_HOST_PASSWORD = f.readline()
    EMAIL_HOST_USER = 'noreply.etherealmachines@gmail.com'
    EMAIL_PORT = 587
    DEFAULT_FROM_EMAIL = EMAIL_HOST_USER
    EMAIL_ADMIN = ('toran.ethereal@gmail.com', )
    ```
- djoser setting variables

```python
DJOSER = {
    'PASSWORD_RESET_CONFIRM_URL': 'auth/password/reset/confirm/{uid}/{token}',
    'ACTIVATION_URL': 'auth/password/reset/confirm/{uid}/{token}',
    'EMAIL': {
        'activation': 'djoser.email.ActivationEmail',
        'confirmation': 'djoser.email.ConfirmationEmail',
        'password_reset': 'djoser.email.PasswordResetEmail',
    },
    # DEFAULT; no need to define here
    'SERIALIZERS': {
        'activation': 'djoser.serializers.ActivationSerializer',
        'password_reset': 'djoser.serializers.PasswordResetSerializer',
        'password_reset_confirm': 'djoser.serializers.PasswordResetConfirmSerializer',
        'password_reset_confirm_retype': 'djoser.serializers.PasswordResetConfirmRetypeSerializer',
        'set_password': 'djoser.serializers.SetPasswordSerializer',
        'set_password_retype': 'djoser.serializers.SetPasswordRetypeSerializer',
        'set_username': 'djoser.serializers.SetUsernameSerializer',
        'set_username_retype': 'djoser.serializers.SetUsernameRetypeSerializer',
        'user_create': 'djoser.serializers.UserCreateSerializer',
        'user_delete': 'djoser.serializers.UserDeleteSerializer',
        'user': 'djoser.serializers.UserSerializer',
        'token': 'djoser.serializers.TokenSerializer',
        'token_create': 'djoser.serializers.TokenCreateSerializer',
    },
}
```

### django-templated-mail
- djoser uses it to create mail template & send mails
- few setting variables:
    - DOMAIN
    - SITE_NAME

## Testing

### Testing ViewSet using:
- APITestCase
- Token Authentication
- APIRequestFactory
- Source: https://gist.github.com/toransahu/706bd1de705e21f3be000e1517f7cae8


# Security
- https://stormpath.com/blog/where-to-store-your-jwts-cookies-vs-html5-web-storage
- http://kylebebak.github.io/post/django-rest-framework-auth-csrf

- django-jwt (JWT_AUTH_COOKIE ) is not safe
    - https://github.com/GetBlimp/django-rest-framework-jwt/issues/338

- if SessionAuthentication is enabled, then CSRF will be used (if ON)
    - https://stackoverflow.com/questions/30871033/django-rest-framework-remove-csrf
- if JWTAuthentications is enabled, then CSRF is automatically disabled

## Vulnerabilities

### CSRF (Cross Site Request Forgery) 


### XSS (Cross Site Script)

## Vulnerables

### Web Client Local/ Session Storage
- XSS

### Cookies (JWT/Auth)
- CSRF
- ajax call : https://gist.github.com/bengolder/aa9033efc8959dc38e5d


# Misc

## Running Multiple Host (website) from Single Django Project
- source: http://effbot.org/zone/django-multihost.htm


## Get request URL string
```python
from django.contrib.sites.shortcuts import get_current_site


print('query_params are:', request.build_absolute_uri())  #returns url with domain
print(request.get_full_path())  #returns url without domain
print(get_current_site(request).domain, request.get_host())  #both returns host or domain
```

## Get slugs from url
if you have any 
- url like: http://127.0.0.1:8000/auth/password/reset/confirm/Mw/4vw-d9cdc8954482ecf8e253/
- url pattern like: path('password/reset/confirm/<slug:uid>/<slug:token>/', password_reset_confirm, name='password_reset_confirm_custom_get')
then code to fetch uid & token will be: https://gist.github.com/toransahu/68663e302f87a9c32a1dcd0654408577

## Microservice Based on REST
- https://www.fullstackpython.com/microservices.html
- https://martinfowler.com/articles/microservices.html
- https://dev.otto.de/2016/03/20/why-microservices/
- with flask: https://medium.com/@ssola/building-microservices-with-python-part-i-5240a8dcc2fb
- django to flask based microservice - https://medium.com/greedygame-media/how-we-broke-up-our-monolithic-django-service-into-microservices-8ad6ff4db9d4
- https://blog.rapid7.com/2016/09/15/microservices-please-dont/

