# Django Render Shortcut and Templates

## Introduction
This document provides an overview of the `render` shortcut in Django and how to use templates to render HTML content.

## The `render` Shortcut
The `render` shortcut is a convenient way to generate an HttpResponse that includes the rendered text of a template. It combines a given template with a context dictionary and returns an HttpResponse object with that rendered text.

### Syntax
```python
from django.shortcuts import render

def view_name(request):
  context = {
    'key': 'value',
  }
  return render(request, 'template_name.html', context)
```

### Parameters
- `request`: The HttpRequest object.
- `template_name`: The name of the template to be used.
- `context`: A dictionary containing the context data to be passed to the template.

## Templates
Templates in Django are used to separate the presentation layer from the business logic. They are typically HTML files that can include dynamic content using Django Template Language (DTL).

### Creating a Template
Templates are usually stored in a directory named `templates` within your app directory. For example:
```
myapp/
  templates/
    myapp/
      template_name.html
```

### Using Template Tags and Filters
Django templates use tags and filters to add logic and manipulate data within the template.

#### Example Template
```html
<!DOCTYPE html>
<html>
<head>
  <title>{{ title }}</title>
</head>
<body>
  <h1>{{ heading }}</h1>
  <p>{{ content }}</p>
</body>
</html>
```

### Common Template Tags
- `{% for %}`: Loop over a sequence.
- `{% if %}`: Conditional statement.
- `{% block %}`: Define a block that can be overridden in child templates.

### Common Template Filters
- `{{ variable|filter }}`: Apply a filter to a variable.
- `{{ name|lower }}`: Convert a string to lowercase.
- `{{ date|date:"D d M Y" }}`: Format a date.

## Example Usage
### views.py
```python
from django.shortcuts import render

def home(request):
  context = {
    'title': 'Home Page',
    'heading': 'Welcome to the Home Page',
    'content': 'This is the content of the home page.',
  }
  return render(request, 'myapp/home.html', context)
```

### home.html
```html
<!DOCTYPE html>
<html>
<head>
  <title>{{ title }}</title>
</head>
<body>
  <h1>{{ heading }}</h1>
  <p>{{ content }}</p>
</body>
</html>
```

## Conclusion
Using the `render` shortcut and templates in Django allows you to efficiently separate your application's logic from its presentation, making your code cleaner and more maintainable.