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
    'social_core.backends.twitter.TwitterOAuth',
)
```

---

## 🔑 Add Social Keys to `settings.py`

### Google

### 🧩 Step 1: Set Up Google App
1. Go to [Google Cloud Console](https://console.cloud.google.com)
2. Create a project or use existing
3. Navigate to **APIs & Services > Credentials**
4. Create **OAuth 2.0 Client ID** (Web Application)
5. Add redirect URI: `http://localhost:8000/google/callback/`
6. Copy **Client ID** and **Client Secret**

```python
SOCIAL_AUTH_GOOGLE_OAUTH2_KEY = 'your-google-client-id'
SOCIAL_AUTH_GOOGLE_OAUTH2_SECRET = 'your-google-client-secret'
SOCIAL_AUTH_GOOGLE_OAUTH2_REDIRECT_URI = 'http://localhost:8000/auth/complete/google-oauth2/'  # Replace with your domain
```

### LinkedIn

### 🧩 Step 1: Set Up LinkedIn App
1. Go to [https://www.linkedin.com/developers/apps](https://www.linkedin.com/developers/apps)
2. Create a new app.
3. Add the OAuth redirect URL: `http://localhost:8000/linkedin/callback/`
4. Copy the **Client ID** and **Client Secret**.

```python
SOCIAL_AUTH_LINKEDIN_OAUTH2_KEY = 'your-linkedin-client-id'
SOCIAL_AUTH_LINKEDIN_OAUTH2_SECRET = 'your-linkedin-client-secret'
SOCIAL_AUTH_LINKEDIN_OAUTH2_SCOPE = ['r_liteprofile', 'r_emailaddress']
```

### Facebook

### Setup Steps
1. Go to [Meta Developers](https://developers.facebook.com/)
2. Create a new app → Facebook Login → Web
3. Set redirect URI: `http://localhost:8000/facebook/callback/`
4. Add to `settings.py`:
   
```python
SOCIAL_AUTH_FACEBOOK_KEY = 'your-facebook-app-id'
SOCIAL_AUTH_FACEBOOK_SECRET = 'your-facebook-app-secret'
SOCIAL_AUTH_FACEBOOK_SCOPE = ['email']
```

### GitHub
1. Go to [GitHub Developer Settings](https://github.com/settings/developers)
2. Create a new OAuth App
3. Set callback: `http://localhost:8000/github/callback/`
4. Add to `settings.py`:

```python
SOCIAL_AUTH_GITHUB_KEY = 'your-github-client-id'
SOCIAL_AUTH_GITHUB_SECRET = 'your-github-client-secret'
```

### Add Social Keys to settings.py

```python
SOCIAL_AUTH_TWITTER_KEY = 'your-twitter-api-key'
SOCIAL_AUTH_TWITTER_SECRET = 'your-twitter-api-secret'
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
<a href="{% url 'social:begin' 'twitter' %}">Login with Twitter</a>
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

