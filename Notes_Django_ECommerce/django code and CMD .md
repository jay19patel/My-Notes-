# Basic Django CMD for creating and maanaging

## Creating a Project:
```py
django-admin startproject projectname
```

## Creating Apps:
```py
python manage.py startapp appname
```

## Running the Development Server:
```py
python manage.py runserver
```

## Database Management:
```py
python manage.py makemigrations # Creates database migration files based on changes in your models.
python manage.py migrate # Applies database migrations to update the database schema.
```

## Interactive Shell:
```py
python manage.py shell # Opens an interactive Python shell with Django's environment loaded.
```

## Running Tests:
```py
python manage.py test appname  # Runs tests within the specified app.
```

## Creating a Superuser:
```py
python manage.py createsuperuser # Creates an admin superuser for your project's admin site.
```

## Collecting Static Files:
```py
python manage.py collectstatic # Collects all static files from your apps and places them in a central location.
```

## Inspecting URLs:
```py
python manage.py show_urls: Displays a list of all defined URLs in your project.
```





# Django MOodel Filters 

## Exact Match (exact):
- Filters for exact matches. For example, to find products with a specific name:
``` py
products = Product.objects.filter(name__exact='Example Product')
```

## Case-insensitive Exact Match (iexact):
- Performs a case-insensitive exact match. For example:

``` py
products = Product.objects.filter(name__iexact='example product')
```

## Contains (contains):
Filters for records containing a specified substring. For example:
``` py
products = Product.objects.filter(name__contains='example')
```

## Case-insensitive Contains (icontains):
Performs a case-insensitive substring search. For example:
``` py
products = Product.objects.filter(name__icontains='example')
```

## Greater Than (gt), Less Than (lt), Greater Than or Equal To (gte), Less Than or Equal To (lte):
Filters for records greater than, less than, greater than or equal to, or less than or equal to a specified value. For example:
``` py
products = Product.objects.filter(price__gt=50)
```

## In (in):
Filters for records matching any value in a list. For example:
``` py
products = Product.objects.filter(category__in=['Electronics', 'Clothing'])
```

## Range (range):
Filters for records within a specified range of values. For example:

``` py
products = Product.objects.filter(price__range=(10, 50))
```

## IsNull (isnull):
Filters for records where a specific field is null or not null. For example:
``` py
products = Product.objects.filter(description__isnull=True)
```

## Date and Time Filters (date, year, month, day, hour, minute, second):
Filters for records based on date and time components. For example:
``` py
products = Product.objects.filter(created_at__year=2023)
```

## Multiple Conditions (Q objects):
Allows combining multiple conditions using logical operators (AND, OR, NOT). For example:
``` py
from django.db.models import Q
products = Product.objects.filter(Q(price__lt=20) | Q(category='Clothing'))
```