# Pagination
- Django provides a few classes that help you manage paginated data – that is, data that’s split across several pages, with “Previous/Next” links.


- When we have millions of data in our api then we need to pagination couse all are not fit in one page 
- we create multiple pages for more data 
- use padination for pages 
#### Default Django  Pagination 
```py
# Unnesesory
#  Default pagination 
#  Add this in setting.py file for config
#  THIS IS DEFAULT PAGINATION  THIS IS APPLAY on All
REST_FRAMEWORK = {
    'DEFAULT_PAGINATION_CLASS': 'apps.core.pagination.PageNumberPagination',
    'PAGE_SIZE': 2
}
```
#### Custom Pagination Class 
- create file pagination.py
- create Class and pass pagination.PageNumberPagination
- create our custom pagination

```py
# import in views.py
from rest_framework.pagination import PageNumberPagination
# create Obj 
paginator = PageNumberPagination()
# Add Pages
paginator.page_size = 10
# create variable and pass the our data which we get from models 
result_page = paginator.paginate_queryset(data, request)

# serialize the result page and return those whole 
serializer = PersonSerializer(result_page, many=True)
return paginator.get_paginated_response(serializer.data)
```

- also we create one custom file for pagination
```py
from rest_framework import pagination
class StandardResultsSetPagination(pagination.PageNumberPagination):
    page_size = 10
    page_query_param = 'page'
    page_size_query_param = 'per_page'
    max_page_size = 1000
```
- other step as well as 
- import 
- create obj of our created class
- wraping
- only chnage obj to default rest modul to our new created modul

- how can we route pages ? => ?page=6 ( 6 is page number what we need page ) 



