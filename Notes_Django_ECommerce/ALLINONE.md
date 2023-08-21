# Basic File Structure 
1. ## Create venv 
```py
pip install virtualenvwrapper-win
mkvvirtualenv env 
# Activate 
workon env
```

2. ## File Structure 

	- __init__.py => Consider as python package
	- wsgi.py => application + Webserver (synchronouss)
	- asgi.py =>  (synchronous,Asynchronous)
	- setting.py => IMP (all information contains)
	- url.py => information of urls and url attached with app
	- manage.py => run server 
	- __pycache__ => Conatin all file data for fast execution 

3. ## Setting.py
	- BASE_DIR => give base directory path 
	- SECRET_KEY => key 
	- DEBUG => True (Error Kya chhe te batavse )	
		          False (Error Hase To pan Nay batavse )
	- DEBUG False => Need Add Domain in ALLOWED_HOSTS =[xyz.com]
	- INSTALLED_APPS => All Apps 
	- MIDDLEWARE => list of MIDDLEWARE (panding samajvanu )
	- DATABASES => Database configuration
	- AUTH_PASSWORD_VALIDATORS => Use for Validation
	- STATIC_URL => '/static/' or 'www.xyz.com'(Path of Static files )

4. ## urls.py
	path(route,view,kwargs=None,name=None)
	route => url path (.../homepage/)
	view => fuction name or link with function
	url trigger the function which we create in views.py 

5. ## template render
	render(request,template_name,context=dict_name,content_type=MIME_type,status,None,using=None)
 Note : if we need to create individual  templates folder  then create same folder "templates" is all apps and then add file name 
  like("template/app1/homepage.html") #HomeAPP
  like("template/app2/LoginPage.html") # Authentication App

6. ## DTL (Django Template Language )
- in django templats we use filters in templates "|"
- syntext ={{name|upper}} 
```py
{{ date_variable|date:"D d M Y" }}
{{ variable|default:"No value available" }}
{{ some_list|length }}
{{ text|lower }}
{{ list_variable|slice:":3" }}
{{ list_of_strings|join:", " }}
{{ long_text|truncatechars:100 }}#chars/words
{{ multiline_text|linebreaks }}
{{ boolean_variable|yesno:"Yes,No,Maybe" }}
{{ float_number|floatformat:2 }}
{{ text_with_urls|urlize }}
{{ text_with_urls|striptags }}#tag remove kari dese
# ....etc
```
- ## if else in template 
```py

{% if condition %}
    # Content to display when the condition is true
{% else %}
    # Content to display when the condition is false
{% endif %}
```
- ## For loops
```py
forloop.counter # The current iteration of the loop, starting from 1.
forloop.counter0 # The current iteration of the loop, starting from 0.
forloop.revcounter # The reverse iteration count, starting from the total number of items.
forloop.revcounter0 # The reverse iteration count, starting from the total number of items minus 1.
forloop.first # Boolean indicating whether it's the first iteration.
forloop.last # Boolean indicating whether it's the last iteration.
```
- ## https://docs.djangoproject.com/en/3.2/ref/templates/builtins/


7. ## Static files 
-  collection of assets such as CSS, JavaScript, images, and other files that are used to style and enhance the functionality of a web application. 
```py
# setting.py
STATIC_URL = '/static/' #prefix static/img.jpg
STATIC_ROOT = os.path.join(BASE_DIR,'staticfiles')# c drive thi path
STATICFILES_DIRS = [ BASE_DIR, 'static'] 

```



8. ## include with with 
- add file wusing include 

```py
{% include "navbar" with p = 'Jay' only %}
```
- using with only we pass the values 




# Advance
1. ## Cookies 
- Cookies are small pieces of text sent to your browser by a website you visit. They help that website remember information about your visit, which can both make it easier to visit the site again and make the site more useful to you.
- usefull and harmfull both 

2. ## ORM 
- Object Relational Mapping (ORM) is a technique used in creating a "bridge" between object-oriented programs and, in most cases, relational databases.
- Autometicly Create databases schema from defined classess
- python django na class use kari ne mysql database ni queary create kari ne database manage and manupilate kari sakiye 

3. ## Model 
- A Django model is the built-in feature that Django uses to create tables, their fields, and various constraints
- show model mysql query 
```py
python manage.py sqlmigrate appname  0001
```
=> model methods 
 - all()
 - filter()
 - get()

4. ## Form (IMP)
- Create own form and pass in tamplate to uer fillthe form 
- user present 
```py
{{form}}
{{form.as_table}}
{{form._as_p}}
{{form._as_ul}}
{{form.field_name}}
```

- clean data recive from form 
```py
form = myformtest(request.POST)
clean_form = form.cleaned_data #as a dictionary 
```

- Custo =m validation in form 

```py
# in form .py
class Studen(models.Model):
	username = form.Charfield()
 # Our Custom Validation Method 
	def clean_name(self):
		valname = self.cleaned_data['name']
		if len(valname)<5:
			raise form.ValidationError("Enter Valid Username")
		return Valname

 # Full Form
 def clean(self):
  cleaned_data = super().clean()
		valname = self.cleaned_data['name']
  ....same as Above
```


```py
# Use Django Validators form django.core import validators

def functionname(value):
 condition 
class Student(form.Form):
 name = form.CharField(validators = [functionname])
 form django.core import validators
```

- also We pass the model in form so we directly get data of model using form and update delete and get models data
```py
class  Registration (forms.ModelForms):
	class Meta:
		model = modelname
		fields = ["name","etc"]
		labels = {"name":"Eneter name"}
		help_text = {"name":"Eneter Full name"}
		error_messages = {"name":{'required':"Nam likhana Jaruri he"}}
  widgets = {'name':forms.CharFields}
```