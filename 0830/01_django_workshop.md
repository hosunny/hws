# 1. intro

```python
from django.contrib import admin
from django.urls import path
from pages import views

urlpatterns = [
    path('admin/', admin.site.urls),
    path('dinner/<str:menu>/<int:people>/', views.dinner),
]
```



# 2. pages

```python
from django.shortcuts import render

def dinner(request, menu, people):
    menu = ['치킨', '피자']
    people = 6
    context = {
        'menu': menu, 
        'people': people,
    }
    return render(request, 'dinner.html', context)
```



# 3. templates

```python

```


