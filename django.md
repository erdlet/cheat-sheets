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

## Operational stuff

Runs the dev server
```bash
python manage.py runserver
```

### Database migration

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

## Admin handling

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

Nicer object names
```python
class MyObject:
  # ...
  
  def __str__(self):
    return "show information"
```
