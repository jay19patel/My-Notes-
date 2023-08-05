# Create Djnago Project 
- django-admin startproject myapis

# Run Server 
- python manage.py runserver 

# Create App 
- python manage.py startapp API 

# Setup New App
- add app in setting "INSTALLED_APPS" => 'CRUDAPI.apps.CrudapiConfig',
- add app url path in project url
- create  app url file 
- create url  path 
- create view function
- link together and test using HttpResponse

# Setup Rest 
- install restframework => pip install djangorestframework
- add in setting "INSTALLED_APPS" => 'rest_framework',

- import some moduls from restFramework in view.py file
```py
from rest_framework.decorators import api_view  # for GET POST Methods 
from rest_framework.response import Response # for our costom respone in rest framework 

@api_view(["GET"])
def HomeAPI(request):
    data = {"Text":"Hi Jay"}
    return Response(data)

```

# Basic Setup Done :> 


# Rest API CRUD 
 C = Create 
 R = Read 
 U = Update
 D = Delete 

 - create urls paths  for all fucntionality in  urls.py
 - create function in views.py

# Create Database and Manage them (Models.py)
- create model for our data 
- migrate our model uisng makemigtations and migrate 
- create superuser for our admin pannel 
```python
python manage.py makemigrations
python manage.py migrate
python manage.py createsuperuser
```

- import models file in view file and use our model call to fetch data 
- fetch data using
```py
 data = Profile.objects.all()
 ```
# Problem 
=> our Models data are python objcet formate ,so can not parsh the data in response
=> Need to serialization of our data 


# Serialization
- create Serializer file => Serializer.py
- import serializers
- import our model
- create our meta class to Abstact our custom data 

```py
from rest_framework import serializers
from .models import Profile

class MyProfileSerializer(serializers.ModelSerializer):
    class Meta:
        model = Profile # model 
        fields = "__all__" # fields we need  also use list for 1,2 objects 
```

- import this serializer in views.py file
- first get model data and then pass thos data in serializers class so serializers return json formate data
- pass the serializers file into response 
- our api is ready (GET)


# POST METHOD 
- get data from other side using request.data 
- pass this data in serializer as a reverse 
- our data are posted but need to save so save using save()
```py
mydata = MyProfileSerializer(data = request.data)
if mydata.is_valid():
   mydata.save()
```

# Here  serializer is give model objcet to json data and json data to model objcet using serializer.data 

# Update 
- get id 
- display the data for reference 
- update change ("PATCH" ,"PUT")
- PUT  => All Change
- PATCH => One field Change


# Patch 
- need to pass the instance and partial=True in  serializer 
- need to valid our serializer data and then next task like save()
```py
mydata = Profile.objects.get(id=id)
upseri = MyProfileSerializer(instance=mydata, data = request.data, partial=True)
```

# Get => get only one data (id=id) return instance 
# Filter => multiple values (name="jay") return list or QuerySet 