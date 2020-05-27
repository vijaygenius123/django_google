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