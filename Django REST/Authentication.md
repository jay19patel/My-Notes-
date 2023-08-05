# Authentication
- REST FRAMEWORK DJANGO INBUILD 
    - Basic Authentication ( User name and password )
    - Token Auth (Token-based HTTP Authentication)
    - Session Auth (Session id )
    - Custom Auth
- THIRD PARTY PACKAGES
    - JSON web token Auth (Token-based )

## Most used  Authentication Techniqe 
### JWT Authentication
#### 1. simple_jwt
- install jwt for django rest 
```py
# Install jwt 
pip install djangorestframework-simplejwt

#  Add in setting.py 
#  THIS IS DEFAULT AUTHENTICATION  THIS IS APPLAY ALL THE FUNCTIOSN SO IT IS NOT NESSESORY
REST_FRAMEWORK = {
    'DEFAULT_AUTHENTICATION_CLASSES': [
        'rest_framework_simplejwt.authentication.JWTAuthentication',
    ],
}
```
```py
# import jwt_views 
from rest_framework_simplejwt import views as jwt_views
# Just Add t this in App urls.py file 
   path('api/token/', jwt_views.TokenObtainPairView.as_view(), name='token_obtain_pair'),
   path('api/token/refresh/', jwt_views.TokenRefreshView.as_view(), name='token_refresh'),

```
- simple we go "api/token/" and  create our token 
- use this token for accessing other urls
```py
#  use Decorater for passing which function we need to have Authentication Functionality
# imprt this 
from rest_framework.decorators import permission_classes
from rest_framework.permissions import IsAuthenticated
#  use this Decorater in any Function
@permission_classes([IsAuthenticated])
```
- for access this method we need to pass the token  use post man and select bearer token and pass our key which we get previews 

#### 2. PyJWT

- create registration api
- create login api
- in our login function
##### Genrate JWT token and set Cookies 
```py
#  install PyJWT
pip install PyJWT
import jwt
# create payload for jwt
payload = {
    "mypayload" = payloadata # mainly we use id 
    "exp" = expire time 
    "iat" =  current time
}
#  create jwt token
 token = jwt.encode(payload,"secret key",algorithm = "HS256").decode("utf-8")

#  need to pass the token in response but we need to pass as a cookies 

response = Response()
response.set_cookie(key="jwt", value = token httponly = True)

response.data={
    "jwt" : token,
    "message":"JWT Authentication"
}

return response
```


- need to install django-cors-headers
```py 
pip install django-cors-headers
 ```
 - also add  in config file in setting.py
 and  also add some config at bottom

 ```py
AUTH_USER_MODEL = 'users.user'
CORS_ORIGIN_ALLOW_ALL = True
CORS_ALLOW_CREDENTIALS = True

 ```
##### Access JWT token and get Cookies and Authenticate Cookies 
 - in our user view function , we need to authenticate user 
 - need user cookies 
 ```py
token  = request.COOKIES.get('jwt')
paylod = jwt.decode(token,"secret key",algorithm = ["HS256"])

# we get a payload if we have  apropiate token in cookies
 ```



### Custom Authentication 
- create own authentication class
- create one file Authenicatme.py
```py
# import BaseAuthentication
from rest_framework.authentication import BaseAuthentication
from rest_framework.exceptions import AuthenticationFailed # if fail 
from django.contrib.auth.models import User # for current loged user 


class CustomAPIKeyAuthentication(BaseAuthentication):
    def authenticate(self, request):
        api_key = request.META.get('HTTP_API_KEY')

        if api_key == 'jaypatelkey':
            try:
                user = User.objects.get(username='jaypatel36')
                return (user, None)
            except User.DoesNotExist:
                raise AuthenticationFailed('Invalid API key.')
        else:
            raise AuthenticationFailed('Authentication credentials not provided.')

    def authenticate_header(self, request):
        return 'API-Key'
```

- which function we need authenication simple add decorater and pass the our class
```py
from rest_framework.decorators import authentication_classes
from .Authme import CustomAPIKeyAuthentication # Import from our created class 
@authentication_classes([CustomAPIKeyAuthentication])
def test():
 return Response(data)
```


# Class Base Authentication 

```py
from rest_framework.permissions import IsAuthenticated

#  in our class
permission_classes = [IsAuthenticated] # simple pass this objet in class 
```