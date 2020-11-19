# Django Commands and other helpful stuff

## Artifact creation
Creates a new project
```bash
django-admin startproject <projectname>
```

Creates an new app
```bash
python manage.py startapp <appname>
```

## Infrastructure

Runs the dev server
```bash
python manage.py runserver
```

## Models

Nicer object names
```python
class MyObject:
  # ...
  
  def __str__(self):
    return "show information"
```

Run all unapplied database migrations
```bash
python manage.py migrate
```

Generate migrations for app
```bash
python manage.py makemigrations <appname>
```

Show resulting SQL from migration
```bash
python manage.py sqlmigrate <appname> <migration-id>
```

## Views

Simple detail view for single object
```python
from django.shortcuts import get_object_or_404, render

from example.models import Example

def detail(request, question_id):
	example = get_object_or_404(Example, pk=example_id)
	return render(request, 'example/detail.html', {'example': example})

```

### Template Control structure

for-loop
```html
{% for item in item_list%}
  
{% endfor %}
```

if/else
```html
{% if True %}
  <!-- Handle case for True -->
{% else %}
  <!-- Handle case for False -->
{% endif %}
```

### URL Handling
Use path name to determine URL in single app project
```python
# File: urls.py
path('<int:example_id>/', example_controller.detail, name='detail'),

# File: example.html
<a href="{% url 'detail' example.id %}">{{ example.text }}</a>
```


Use path name to determine URL in multi app project
```python
# File: urls.py
app_name = 'example'
urlpatterns = [
...,
path('<int:example_id>/', example_controller.detail, name='detail'),
]

# File: example.html
<a href="{% url 'example:detail' example.id %}">{{ example.text }}</a>
```

## Admin interface

Create superuser
```bash
python manage.py createsuperuser
```

Register model to admin interface
```python
# File: <appname>/admin.py

from django.contrib import admin

from .models import <myModel>

admin.site.register(<myModel>)
```

## Misc

Check for issues in the application
```bash
python manage.py check
```
