# Django Google Auth

1. Install django-allauth `pip install django-allauth`

2. In settings.py make the changes like below:

```python

'''
    Add the lines below at end of file
'''

INSTALLED_APPS = INSTALLED_APPS + [
    'django.contrib.sites',
    'allauth',
    'allauth.account',
    'allauth.socialaccount',
    'allauth.socialaccount.providers.google'
]

STATIC_URL = '/static/'

SITE_ID = 1


AUTHENTICATION_BACKENDS = (
 'django.contrib.auth.backends.ModelBackend',
 'allauth.account.auth_backends.AuthenticationBackend',
)

LOGIN_REDIRECT_URL = '/'

SOCIALACCOUNT_PROVIDERS = {
    'google': {
        'SCOPE': [
            'profile',
            'email',
        ],
        'AUTH_PARAMS': {
            'access_type': 'online',
        }
    }
}
```


3. Include allauth.urls in urls.py

```python
'''
    At end of urls.py in project folder
'''
urlpatterns = urlpatterns + [
    path('accounts/', include('allauth.urls')),
]
```


4. Create an django app and create a file with below html template to display login page, Add the application into INSTALLED_APPS in settings.py


```html
{% load socialaccount %}
<html>

<head>
    <title>Auth Page</title>
</head>

<body>
    <h1>Django Application</h1>
    {% if user.is_authenticated %}
    <p>Welcome, {{ user.username }} !</p>

    {% else %}
    <h1>Google Login</h1>
    <a href="{% provider_login_url 'google' %}">Login with Google</a>
    {% endif %}

</body>

</html>
```

In the urls.py update the content like below so the page can be reached 

```python
urlpatterns = urlpatterns + [
    path('', TemplateView.as_view(template_name="social_app/index.html")),
    path('accounts/', include('allauth.urls')),
]

```

5. Run migrations and create a superuser. Then login to the django admin console and create a new Social Application with the client id and secret from the application created in google developers console.