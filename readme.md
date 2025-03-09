# Django REST Framework Documentation

## Introduction
Django REST Framework (DRF) is a powerful and flexible toolkit for building Web APIs in Django. This documentation will guide you through the steps to create APIs using DRF.

## Prerequisites
- Python installed on your system
- Django installed (`pip install django`)
- Django REST Framework installed (`pip install djangorestframework`)

## Step 1: Setting Up the Django Project
1. Create a new Django project:
  ```bash
  django-admin startproject myproject
  cd myproject
  ```

2. Create a new Django app:
  ```bash
  python manage.py startapp myapp
  ```

3. Add the app and REST framework to `INSTALLED_APPS` in `myproject/settings.py`:
  ```python
  INSTALLED_APPS = [
    ...
    'rest_framework',
    'myapp',
  ]
  ```

## Step 2: Creating Models
1. Define your models in `myapp/models.py`:
  ```python
  from django.db import models

  class Item(models.Model):
    name = models.CharField(max_length=100)
    description = models.TextField()

    def __str__(self):
      return self.name
  ```

2. Run migrations to create the database tables:
  ```bash
  python manage.py makemigrations
  python manage.py migrate
  ```

## Step 3: Creating Serializers
1. Create a serializer for your model in `myapp/serializers.py`:
  ```python
  from rest_framework import serializers
  from .models import Item

  class ItemSerializer(serializers.ModelSerializer):
    class Meta:
      model = Item
      fields = '__all__'
  ```

## Step 4: Creating Views
1. Create views for your API in `myapp/views.py`:
  ```python
  from rest_framework import generics
  from .models import Item
  from .serializers import ItemSerializer

  class ItemListCreate(generics.ListCreateAPIView):
    queryset = Item.objects.all()
    serializer_class = ItemSerializer

  class ItemDetail(generics.RetrieveUpdateDestroyAPIView):
    queryset = Item.objects.all()
    serializer_class = ItemSerializer
  ```

## Step 5: Configuring URLs
1. Add URL patterns for your API in `myapp/urls.py`:
  ```python
  from django.urls import path
  from .views import ItemListCreate, ItemDetail

  urlpatterns = [
    path('items/', ItemListCreate.as_view(), name='item-list-create'),
    path('items/<int:pk>/', ItemDetail.as_view(), name='item-detail'),
  ]
  ```

2. Include the app URLs in the project’s `urls.py`:
  ```python
  from django.contrib import admin
  from django.urls import path, include

  urlpatterns = [
    path('admin/', admin.site.urls),
    path('api/', include('myapp.urls')),
  ]
  ```

## Step 6: Testing the API
1. Run the Django development server:
  ```bash
  python manage.py runserver
  ```

2. Use a tool like Postman or curl to test your API endpoints:
  - List and create items: `http://127.0.0.1:8000/api/items/`
  - Retrieve, update, and delete an item: `http://127.0.0.1:8000/api/items/<id>/`

## Conclusion
You have now created a basic API using Django REST Framework. You can extend this by adding authentication, permissions, and more complex functionality as needed.

For more information, refer to the [Django REST Framework documentation](https://www.django-rest-framework.org/).