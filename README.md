# Django Social Login (Using `social-auth-app-django`)

This guide walks you through setting up **Google**, **LinkedIn**, **Facebook**, and **GitHub** login in Django using the `social-auth-app-django` package.

---

## 🔧 Prerequisites
Install the following packages:

```bash
pip install social-auth-app-django
```

Add the required apps in your `settings.py`:

```python
INSTALLED_APPS = [
    # Your apps
    'django.contrib.sites',
    'social_django',
    # ...
]

SITE_ID = 1
```

---

## ⚙️ Add Authentication Backends

```python
AUTHENTICATION_BACKENDS = (
    'django.contrib.auth.backends.ModelBackend',
    'social_core.backends.google.GoogleOAuth2',
    'social_core.backends.linkedin.LinkedinOAuth2',
    'social_core.backends.facebook.FacebookOAuth2',
    'social_core.backends.github.GithubOAuth2',
)
```

---

## 🔑 Add Social Keys to `settings.py`

### Google
```python
SOCIAL_AUTH_GOOGLE_OAUTH2_KEY = 'your-google-client-id'
SOCIAL_AUTH_GOOGLE_OAUTH2_SECRET = 'your-google-client-secret'
SOCIAL_AUTH_GOOGLE_OAUTH2_REDIRECT_URI = 'http://localhost:8000/auth/complete/google-oauth2/'  # Replace with your domain
```

### LinkedIn
```python
SOCIAL_AUTH_LINKEDIN_OAUTH2_KEY = 'your-linkedin-client-id'
SOCIAL_AUTH_LINKEDIN_OAUTH2_SECRET = 'your-linkedin-client-secret'
SOCIAL_AUTH_LINKEDIN_OAUTH2_SCOPE = ['r_liteprofile', 'r_emailaddress']
```

### Facebook
```python
SOCIAL_AUTH_FACEBOOK_KEY = 'your-facebook-app-id'
SOCIAL_AUTH_FACEBOOK_SECRET = 'your-facebook-app-secret'
SOCIAL_AUTH_FACEBOOK_SCOPE = ['email']
```

### GitHub
```python
SOCIAL_AUTH_GITHUB_KEY = 'your-github-client-id'
SOCIAL_AUTH_GITHUB_SECRET = 'your-github-client-secret'
```

---

## 🌐 URLs Configuration
In your `urls.py`:

```python
from django.urls import path, include

urlpatterns = [
    path('auth/', include('social_django.urls', namespace='social')),
]
```

---

## 👤 Login Buttons (Frontend)
You can use Django template tags for links:

```django
<a href="{% url 'social:begin' 'google-oauth2' %}">Login with Google</a>
<a href="{% url 'social:begin' 'linkedin-oauth2' %}">Login with LinkedIn</a>
<a href="{% url 'social:begin' 'facebook' %}">Login with Facebook</a>
<a href="{% url 'social:begin' 'github' %}">Login with GitHub</a>
```

---

## ⚙️ Middleware
Ensure these are in your `settings.py`:

```python
MIDDLEWARE = [
    # ...
    'social_django.middleware.SocialAuthExceptionMiddleware',
    # ...
]
```

---

## 📁 Templates
To access the current social login data:

```django
{% if user.is_authenticated %}
  Hello, {{ user.get_username }}!
{% endif %}
```

---

## 🔄 Redirect URLs
Set redirect URLs in your `settings.py`:

```python
LOGIN_URL = 'login'
LOGIN_REDIRECT_URL = '/'
LOGOUT_REDIRECT_URL = '/'
```

---

Now you can support **Google**, **LinkedIn**, **Facebook**, and **GitHub** login in your Django app using `social-auth-app-django`!

Let me know if you want to enable Apple, Twitter, or Microsoft login next. ✅

