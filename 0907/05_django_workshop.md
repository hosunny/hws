![](C:\Users\HoSunny\AppData\Roaming\marktext\images\2022-09-07-21-57-24-image.png)

```python
from contextlib import redirect_stderr
from multiprocessing import context
from django.shortcuts import render, redirect
from django.contrib.auth.forms import AuthenticationForm
from django.contrib.auth import login as auth_login
from django.contrib.auth import logout as auth_logout

# Create your views here.
def login(request):
    if request.method == 'POST':
        form = AuthenticationForm(request, request.POST)
        if form.is_varid():
            auth_login(request, form.get_user())
            return redirect('articles:index')

    else:
        form = AuthenticationForm()
    context = {
        'form': form,
    }
    return render(request, 'accounts/login.html', context)

def logout(request):
    auth_logout(request)
    return redirect('articles:index')
```