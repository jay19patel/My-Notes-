# Class Base Views 


### APIView 
- best for cutom CRUD Opartion
- in APIView we can create our custom get(), post(),put(),patch(),delete() methodss
```py 
#  import APIView class 
from rest_framework.views import APIView
```


### ListAPIView (Using GenericAPIS and Mixin )
- easy beacouse we listapi are import all data from mixin and genric apis  
- best for creating get api with functionality (Pagination, Filter ,Search, Orderd by)
- this is Automaticly run the get methods and provide the response without complexity.
- Other Methods 
-import modeul from (from rest_framework.generics import ListAPIView,etc)


ListAPIView: GET (BEST FOR GET METHOD)
CreateAPIView:  POST
UpdateAPIView: POST
DestroyAPIView: POST
ListCreateAPIView: GET POST
RetrieveAPIView:  GET
RetrieveUpdateAPIView:  GET POST
RetrieveDestroyAPIView:  GET POST
RetrieveUpdateDestroyAPIView:  GET POST UPDATE DELETE

- these are used for  build in crud opeation no more write codes default crud opratiosn perform here 


### GenericAPIView: 
- Also Use for custom GET POST PATCH PUT DELETE method 
- A view that provides commonly used behavior for handling model data. It's often used in combination with mixins and serializers to perform CRUD operations on a model.





# APIView Example 

- in url we need pass function name with .as_view()

```py
path('', ProductsPage.as_view()) , 
```

- create classes in views file 
- for get method we need to create get named function
- as well as post , put,patch ,update,delete methods

```py
class ProductsPage(APIView):
    def get(self, request):
        mydata = Products.objects.all()
        data_serialize = MyProductSerializer(mydata,many=True)
        res =Response(data_serialize.data)
        return res
```

# ListAPIView
#### Best For Padination Filter Search and OrderBy
- use simple ListAPIView method in classs  and direct pass
```py
class ProductPage(ListAPIView):
    queryset = Product.objects.all()
    serializer_class=MyProducts_Serializer
    pagination_class =StandardResultsSetPagination

    filter_backends = [DjangoFilterBackend,OrderingFilter,SearchFilter]

   # Search 
    search_fields = ['name', 'price']

   # filter 
    filterset_fields = ['on_sale', 'price']
    
   # Oder by 
    ordering_fields = ['name', 'price']

```


# GenericAPIView Example 

```py
from rest_framework.generics import GenericAPIView
from rest_framework.mixins import ListModelMixin, CreateModelMixin, RetrieveModelMixin, UpdateModelMixin, DestroyModelMixin

class BookListCreateAPIView(GenericAPIView, ListModelMixin, CreateModelMixin):
    queryset = Book.objects.all()
    serializer_class = BookSerializer

    # Get All Data
    def get(self, request):
        return self.list(request)

    # Post New data
    def post(self, request):
        return self.create(request)


class BookRetrieveUpdateDestroyAPIView(GenericAPIView, , UpdateModelMixin, DestroyModelMixin):
    queryset = Book.objects.all()
    serializer_class = BookSerializer

    # get Single Data 
    def get(self, request, pk):
        return self.retrieve(request, pk)

    # put data  Udate 
    def put(self, request, pk):
        return self.update(request, pk)
    
    # Patch Data Update
    def patch(self, request, pk):
        book = self.get_object(pk)
        serializer = self.get_serializer(book, data=request.data, partial=True)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data)
        return Response(serializer.errors, status=status.HTTP_400_BAD_REQUEST)

    # delete data 
    def delete(self, request, pk):
        return self.destroy(request, pk)

```
- get post patch put delete are getting from GenericAPIView
- retrive ,update,destroy etc etc are geting from mixin classses


# In APIView is best for CRUD and also all dobjcets are created in functions
# In ListAPIViews is best for Only Get methdo where we use objects of any files are simple manupliate autometicly 
# In GenericAPIView is besr for CRUD but here Objects are created in class 