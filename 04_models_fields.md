# Django Model Fields

Django models define the structure of your database tables. Each model is a Python class that subclasses `django.db.models.Model`. Within each model, you define class attributes that represent the fields in the database table.

## Common Field Types

### `CharField`
A string field, for small- to large-sized strings. For large text, use `TextField`.

```python
from django.db import models

class MyModel(models.Model):
  name = models.CharField(max_length=100)
```

### `TextField`
A large text field. Use this for storing large amounts of text.

```python
class MyModel(models.Model):
  description = models.TextField()
```

### `IntegerField`
An integer field. Values from -2147483648 to 2147483647 are safe in all databases supported by Django.

```python
class MyModel(models.Model):
  age = models.IntegerField()
```

### `BooleanField`
A true/false field.

```python
class MyModel(models.Model):
  is_active = models.BooleanField(default=True)
```

### `DateField`
A date field.

```python
class MyModel(models.Model):
  birth_date = models.DateField()
```

### `DateTimeField`
A date and time field.

```python
class MyModel(models.Model):
  created_at = models.DateTimeField(auto_now_add=True)
```

### `ForeignKey`
A many-to-one relationship.

```python
class MyModel(models.Model):
  related_model = models.ForeignKey('RelatedModel', on_delete=models.CASCADE)
```

### `ManyToManyField`
A many-to-many relationship.

```python
class MyModel(models.Model):
  related_models = models.ManyToManyField('RelatedModel')
```

### `OneToOneField`
A one-to-one relationship.

```python
class MyModel(models.Model):
  related_model = models.OneToOneField('RelatedModel', on_delete=models.CASCADE)
```

## Field Options

### `null`
If `True`, Django will store empty values as `NULL` in the database. Default is `False`.

### `blank`
If `True`, the field is allowed to be blank. Default is `False`.

### `choices`
A sequence of 2-tuples to use as choices for this field.

```python
class MyModel(models.Model):
  STATUS_CHOICES = [
    ('draft', 'Draft'),
    ('published', 'Published'),
  ]
  status = models.CharField(max_length=10, choices=STATUS_CHOICES)
```

### `default`
The default value for the field.

```python
class MyModel(models.Model):
  created_at = models.DateTimeField(default=timezone.now)
```

### `unique`
If `True`, this field must be unique throughout the table.

```python
class MyModel(models.Model):
  email = models.EmailField(unique=True)
```

### `verbose_name`
A human-readable name for the field.

```python
class MyModel(models.Model):
  first_name = models.CharField(max_length=30, verbose_name='First Name')
```

### `help_text`
Extra help text to be displayed with the form widget.

```python
class MyModel(models.Model):
  name = models.CharField(max_length=100, help_text='Enter your full name')
```

## Conclusion

Django model fields provide a powerful way to define the structure and constraints of your database tables. By understanding and utilizing these fields, you can create robust and efficient database schemas for your Django applications.