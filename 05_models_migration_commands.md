# Django Models and Migration Commands

## Creating a New Model

To create a new model in Django, define a class in your `models.py` file that inherits from `django.db.models.Model`.

```python
from django.db import models

class MyModel(models.Model):
  name = models.CharField(max_length=100)
  description = models.TextField()
  created_at = models.DateTimeField(auto_now_add=True)
```

## Making Migrations

After defining your models, you need to create migrations to apply the changes to the database.

```bash
python manage.py makemigrations
```

## Applying Migrations

To apply the migrations and create the corresponding tables in the database, run:

```bash
python manage.py migrate
```