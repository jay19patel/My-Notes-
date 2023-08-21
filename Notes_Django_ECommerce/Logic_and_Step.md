1. # Setup Project
## Create new project
## create new app
## Install App in Setting.py
## Configure Templates

```py
# in setting.py tebmplate 
  [os.path.join(BASE_DIR,'Templates')]
# BASE_DIR means where our manage.py file are exsit thet path
```
## Configure Static and media File in setting and urls.py
```py
# add STATIC ROOT in setting.py 
STATIC_ROOT = os.path.join(BASE_DIR,'staticfiles')#means data are existe in staticfile file 
# base_dir atle ke manage.py file chhe te file ma static file ma data che m.

# all static file autometicly placed in staticfiles folder
STATICFILES_DIRS = [ BASE_DIR, 'static']
# darek static file autometicly static ni andar avi jase 


MEDIA_URL = '/media/'
MEDIA_ROOT = os.path.join(BASE_DIR,'media')
# media file autometicly create thase jyare product image ,profile ke kayk add thase tyare 
```


```py
# Add static file in url file on project url
from django.conf import settings
from django.conf.urls.static import static

urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
urlpatterns += static(settings.STATIC_URL, document_root=settings.STATIC_ROOT)
# pass the file path of static file in html files 
```
## Create basic HttpResponse in app view.py file 
## Create Template file and Add HTML files
## Configure templates inheritance and partials

2. # User Authentication (Abstraction)
## Django Provide inbuild authentication with less functionality and less userfields 
## We Extends this Functionality and add more fields
## Create App for authentication functinality
## Basic App Configaration
## Create Superuser
## New UserField
    - email
    - username
    - 
## AbstractUser
```py
# in Userauths app
# model.py
from django.contrib.auth.models import AbstractUser
from django.contrib import models

class User(AbstractUser):
  #  here add fields which we need in Users 

#  Add Configartion of new User in setting.py
AUTH_USER_MODEL = 'userauths.User' # appname and Model name 
```
## Multiple Fields In admin Pannel 

```py
# admin.py
from userauths.models import User

class UserAdmin(admin.ModelAdmin):
  list_display =['username','email','etc']

admin.site.register(User,UserAdmin)
```

3. # User Register login
## create form of our model for register
```py
from django.contrib.auth.forms import UserCreationForm
from userauths.model import User 

class UserRegistration(UserCreationForm):
  class Meta :
    model = User
    fields =['what we need ']

```
## create Login page for getting username and password 
## authenticate user input data and  if valid then userd are logdin 
```py
user = authenticate(username=username, password=password)
if user is not None:
    login(request,user)
```


4. # Products Model
### Products 
    - title
    - user
    - price
    - discount
    - image
    - description
    - category
    - sale
    - stock
    - date
## Access Model data in Home funtcion and pass products in html page
## Also Adding Some Fillters 
## Get Filter Id or Data using Get Method and fetch in Function
```py
# all data
products = Products.objects.all()

#  for filltering 
category_id = request.GET.get('category')
price_search  = request.GET.get('valuedata')

products = Product.objects.filter(Q(price__lt=price_search) |  Q(category_id=category_id))

```
## Pass those data in html page and using for loop extract all products 


5. # Products Views 
## Simple Get All Products in Function and pass in model
## Create form in View button and get Product id in function
## Get Object and pass those data in ProductView Template


6. # Filter Products
## Create Get Post Method and get Categoy/Price/Search data in backend
## Using Q
```py 
from django.db.models import Q

# Use
products = Product.objects.filter(Q(title__icontains=search) | Q(description__icontains=search) )
```
## simply we get Filter Products Using Q and Filter methods 
## all Methods for fillter in Django code and CMD Notes 

7. # Add To Cart 
## Create MOdel for Cart Data 
## In Evry Cart Have User identity
## User have One Cart and User have multiple product in cart
## So we need one Cart Id and connect with Multiple Product with this cart 

## UserCart
    - user
    - cart_id
    - is_paid (order/cart)

## UserCartItem
  - usercart
  - products
  - qnty
  - date 
  

## When User try to add item in cart then we also fetch product id and qntity in functon
## We get product id andqnty so we add this data in aporopiate user or orderid 
## get orderid and ad those cart data in order 
## if data alredy in database then only add qntity other wise add whole data in database 
## Create all data in CartPage function and pass those data in cart page so we get all cart items in cart page 
```py
# Update  Cart Qntity 
User_cart = UserCartItem.objects.get(cart=my_order,product=product)
User_cart.qnty = 5
User_cart.total_price=100
User_cart.save()
```



8. # Redirect Page Previes
```py
from django.http import HttpResponseRedirect
return HttpResponseRedirect(request.path_info)
```


9. # Django Count Aggresstion 
# like mate model banavi ne darek click par ek ek event add thase and event count karse 
```py
products = Product.objects.annotate(like_count=Count('savelikes'))
```

10. # Checkou page
## check our data if all details are requires are true then add in database or update
## get all data in checkout page if delivery is done then item is deleted
## Autometicly all task are done when you are taking all problem one by one .
## Under stand problem erorr and requirement and then empliment 


