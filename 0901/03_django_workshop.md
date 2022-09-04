![](C:\Users\HoSunny\AppData\Roaming\marktext\images\2022-09-04-20-59-57-image.png)

![](C:\Users\HoSunny\AppData\Roaming\marktext\images\2022-09-04-21-00-24-image.png)



# url

* crud/urls

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('articles/', include('articles.urls')),
]
```

* articles/urls

```python
from django.urls import path
from . import views

app_name = 'articles'

urlpatterns = [
    path('index/', views.index, name = 'index'),
    path('new/', views.new, name = 'new'),
    path('create/', views.create, name = 'create'),
    path('<int:pk>/', views.detail, name = 'detail'),
]
```

# view

```python
from django.shortcuts import render, redirect
from .models import Article

def index(request):
    articles = Article.objects.all()
    context = {
        'articles': articles,
    }
    return render(request, 'articles/index.html', context)

def new(request):
    return render(request, 'articles/new.html')

def detail(request, pk):
    article =Article.objects.get(pk=pk)
    context = {
        'article': article,
    }
    return render(request, 'articles/detail.html', context)

def create(request):
    title = request.POST.get('title')
    content = request.POST.get('content')

    article = Article(title=title, content=content)
    article.save()

    return redirect('articles:index')
```



# template

* base

```python
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.2.0-beta1/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-0evHe/X+R7YkIZDRvuzKMRqM+OrBnVFBL6DOitfPri4tjfHxaWutUpFmBp4vmVor" crossorigin="anonymous">
    <title>Document</title>
</head>
<body>
    {% block content %}{% endblock content %}
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.2.0-beta1/dist/js/bootstrap.bundle.min.js" integrity="sha384-pprn3073KE6tl6bjs2QrFaJGz5/SUsLqktiwsUTF55Jfv3qYSDhgCecCxMW52nD2" crossorigin="anonymous"></script>
</body>
</html>
```

* index

```python
{% extends 'base.html' %}

{% block content %}
    <h1>INDEX</h1>
    <a href="{% url 'articles:new' %}">NEW</a>
    <br>
    <br>
    <br>
    {% for movie in movies %}
        <p>제목: {{ article.title }}</p>
        <p>내용: {{ article.content }}</p>
        <a href="{% url 'articles:detail' article.pk %}">DETAIL</a>
    {% endfor %}

{% endblock content %}
```

* new

```python
{% extends 'base.html' %}

{% block content %}
    <h1>NEW</h1>
    <form action="{% url 'articles:create' %}" method="POST">
        {% csrf_token %}
        <label for="title">Title</label>
        <input type="text" name='title' id="title"><br>
        <label for="content">Content</label>
        <textarea name="content" id="content" cols="30" rows="8"></textarea><br>
        <input type="submit">
    </form>
    <a href="{% url 'articles:index' %}">BACK</a>

{% endblock content %}
```

* detail

```python
{% extends 'base.html' %}

{% block content %}
    <p>{{ article.title }}</p>
    <p>{{ article.content }}</p>
{% endblock content %}
```



# model

```python
from django.db import models

# Create your models here.
class Article(models.Model):
    title = models.CharField(max_length=20, null=True )
    content = models.TextField()
```
