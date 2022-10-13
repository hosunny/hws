# TodoApp

```django
# base.html
  <div class='container'>
  {% if request.user.is_authenticated %}
    <a href="{% url 'todos:new' %}">NEW</a>
  {% else %}
    <a href="{% url 'accounts:login' %}">login</a>
    <a href="{% url 'accounts:signup' %}">signup</a>
  {% endif %}
  {% block content %}
  Todos
  {% endblock %}
  </div> 
```

## 1. user 대체

```python
# accounts/models.py

from django.contrib.auth.models import AbstractUser


class User(AbstractUser):
    pass
```

```python
# settings.py

AUTH_USER_MODEL = 'accounts.User' 
```

---

## 2. 회원 가입

```python
# accounts/forms.py

from django.contrib.auth import get_user_model
from django.contrib.auth.forms import UserCreationForm


class CustomUserCreationForm(UserCreationForm):

    class Meta(UserCreationForm.Meta):
        model = get_user_model()
        fields = UserCreationForm.Meta.fields
```

```python
# accounts/urls.py

from django.urls import path
from . import views

app_name = 'accounts'
urlpatterns = [
    path('signup/', views.signup, name='signup'),
]
```

```python
# accounts/views.py

from django.shortcuts import render, redirect
from .forms import CustomUserCreationForm


def signup(request):
    if request.method == 'POST':
        form = CustomUserCreationForm(request.POST)
        if form.is_valid():
            form.save()
            return redirect('accounts:login')
    else:
        form = CustomUserCreationForm()

    context = {
        'form': form,
    }
    return render(request, 'accounts/signup.html', context)
```

```django
<!-- accounts/templates/accounts/signup.html -->

{% extends 'base.html' %}
{% block content %}
  <h2>Sign Up</h2>
  <form action="" method="post">
    {% csrf_token %}
    {{ form.as_p }}
    <button>SignUp!</button>
  </form>
{% endblock %}
```

---

## 3. login

```python
# accounts/urls.py

from django.urls import path
from . import views

app_name = 'accounts'
urlpatterns = [
    path('signup/', views.signup, name='signup'),
    path('login/', views.login, name='login'),
]
```

```python
# accounts/views.py

from django.shortcuts import render, redirect
from django.contrib.auth import login as auth_login
from django.contrib.auth.forms import AuthenticationForm
from .forms import CustomUserCreationForm


def login(request):
    if request.method == 'POST':
        form = AuthenticationForm(request, request.POST)
        if form.is_valid():
            user = form.get_user()
            auth_login(request, user)
            return redirect(request.GET.get('next') or 'todos:index')
    else:
        form = AuthenticationForm()

    context = {
        'form': form,
    }
    return render(request, 'accounts/login.html', context)
```

```django
<!-- accounts/templates/accounts/login.html -->

{% extends 'base.html' %}
{% block content %}
  <h2>Login</h2>
  <form action="" method="post">
    {% csrf_token %}
    {{ form.as_p }}
    <button>login</button>
  </form>
  <a href="{% url 'accounts:signup' %}">Signup</a>
{% endblock %}
```

## 4. Todo 목록

```python
# todos/urls.py

from django.urls import path
from . import views

app_name = 'todos'
urlpatterns = [
    path('', views.index, name='index'),
]
```

```python
# todos/views.py

from django.shortcuts import render, redirect
from django.contrib.auth.decorators import login_required

# Create your views here.
@login_required
def index(request):
    todos = request.user.todo_set.all()
    context = {
        'todos': todos,
    }
    return render(request, 'todos/index.html', context)
```

```django
<!-- todos/index.html -->

{% extends 'base.html' %}
{% block content %}
  <h1>INDEX</h1>
  {% for todo in todos %}
  <div>
    <h1>할 일: {{ todo.title }}</h1>
    <p>작성자: {{ todo.author }}</p>
    <p>완료여부: {{ todo.completed }}</p>
    <hr>
  </div>
  {% endfor %}
{% endblock %}
```

---

## 5. Todo 생성

```python
# todos/models.py

from django.db import models
from django.conf import settings

# Create your models here.
class Todo(models.Model):
    author = models.ForeignKey(settings.AUTH_USER_MODEL, on_delete=models.CASCADE)
    title = models.CharField(max_length=100)
    completed = models.BooleanField(default=False)
```

```python
# todos/forms.py

from django import forms
from .models import Todo

class TodoForm(forms.ModelForm):
    class Meta:
        model = Todo
        fields = ['title', 'completed',]
```

```python
# todos/urls.py

from django.urls import path
from . import views

app_name = 'todos'
urlpatterns = [
    path('', views.index, name='index'),
    path('new/', views.new, name='new'),
]
```

```python
# todos/views.py

from django.shortcuts import render, redirect
from django.contrib.auth.decorators import login_required
from .forms import TodoForm

...

@login_required
def new(request):
    if request.method == 'POST':
        form = TodoForm(request.POST)
        if form.is_valid():
            todo = form.save(commit=False)
            todo.author = request.user
            todo.save()
            return redirect('todos:index')
    else:
        form = TodoForm()

    context = {
        'form': form,
    }
    return render(request, 'todos/new.html', context)
```

```django
<!-- todos/new.html -->

{% extends 'base.html' %}
{% block content %}
  <h2>New</h2>
  <form action="" method="post">
    {% csrf_token %}
    {{ form.as_p }}
    <button>New</button>
  </form>
{% endblock %}
```
