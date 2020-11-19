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

Sublime Snippet for Form
Form Snippet
```xml
<snippet>
	<content><![CDATA[
<form action="{% url '${1}' ${2} %}" method="${3:post}">
	{% csrf_token %}
	${4}
</form>
]]></content>
	
	<tabTrigger>djform</tabTrigger>
	<scope>text.html.basic</scope>
</snippet>
```

Generic List View
```python
from django.views import generic

from polls.models import Question

class IndexView(generic.ListView):
	template_name = 'example/index.html'
	context_object_name = 'first_five_examples'

	def get_queryset(self):
		return Example.objects[:5]
```

Generic Detail View
```python
from django.views import generic

from polls.models import Example

class DetailView(generic.DetailView):
	# Model name in template is 'example' as long as 'Example' is a Django Model
	model = Example
	# Override default template name
	template_name = 'example/detail.html'
```

### Template Control structure

for-loop
```html
{% for item in item_list%}
  
{% endfor %}
```

Counter in for-loops:
```html
{{ forloop.counter }}
```

if/else
```html
{% if True %}
  <!-- Handle case for True -->
{% else %}
  <!-- Handle case for False -->
{% endif %}
```

if/else Sublime Snippet
```xml
<snippet>
	<content><![CDATA[
{% if ${1} %}
	${2}
{% endif %}
]]></content>
	<tabTrigger>djif</tabTrigger>
	<scope>text.html.basic</scope>
</snippet>

```

### URL Handling
Use path name to determine URL in single app project
```python
# File: urls.py
path('<int:example_id>/', example_controller.detail, name='detail'),

# File: example.html
<a href="{% url 'detail' example.id %}">{{ example.text }}</a>
```

Sublime HTML Snippet
```xml
URL Snippet
```xml
<snippet>
	<content><![CDATA[
{% url '${1}' ${2}%}
]]></content>
	
	<tabTrigger>djurl</tabTrigger>
	<scope>text.html.basic</scope>
</snippet>
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
