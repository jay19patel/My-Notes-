## Forgate password // Chnage password 
## first we need to find users email id
```py
# find user email id 
from django.contrib.auth.models import User

username = "jaypatel36" # get name using form 

user_obj = User.objects.filter(username=username).first()
# and then using username we find userdata (email)
user_data = User.objects.get(username=user_obj)
```



## SMTP Config
```py
EMAIL_BACKEND = 'django.core.mail.backends.smtp.EmailBackend'
EMAIL_HOST = 'smtp.example.com'
EMAIL_PORT = 587
EMAIL_USE_TLS = True
EMAIL_HOST_USER = 'your_username'
EMAIL_HOST_PASSWORD = 'your_password'
```


## Create function for Genrating SMTP mail
```py
from django.core.mail import send_mail
def send_forgate_password_mail(email,token):
    subject = "Forgate password link"
    message = f"URL: {token}"
    email_from = settings.EMAIL_HOST_USER
    recipient_list = [email]
    send_mail(subject,message,email_from,recipient_list)
    return True 
```



# STEPs (OTP):
- random 4 number int genarete
- create jwt token and pass the otp and username or email of user
- token save in session
- send email for otp (Print OTP)
- In other html page we get OTP input
- in decodeFunction we get session data
- decode our token
- match inpput and token otp 
- both are same then chnage password




# Google Login 
- import all auth 
```py
pip install django-allauth
```