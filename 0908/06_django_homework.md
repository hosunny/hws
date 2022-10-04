# 1. login validation

```python
django.contrib.auth.context
```

 

# 2. Login 기능 구현

(a): AuthenticationForm

(b): login

(c): form.get_user()

# 

# 3. who are you?

* AnonymousUser



# 4. 암호화 알고리즘

```python
from django.contrib.auth import update_session_auth_hash

update_session_auth_hash(requeast, form.user)
```



# 5. Logout 기능 구현

* logout 의 이름이 겹친다. 따라서 둘 째 줄의 logout 을 auth_logout로 고치면 해결된다.
