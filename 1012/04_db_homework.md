# 1. M:N True or False

* T

* T

* F

# 2. Like in templates

(a) user (or request.user)

(b) article.like_users.all

# 3. Follow in views

(a) user_pk

(b) followers

(c) filter

(d) remove

(e) add

# 4. User AttributeError

```python
from django.contrib.auth.forms import UserCreationForm
from django.contrib.auth import get_user_model

class CustomUserCreationForm(UserCreationForm):

   class Meta(UserCreationForm.Meta):
       model = get_user_model()
       fields = UserCreationForm.Meta.fields
```

# 5. related_name

* M:N 관계 설정 시에 `related_name`이 없다면 자동으로 `article_set` 매니저를 사용할 수 있도록 하는 데 이 매니저는 기존에 N:1 관계에서 이미 사용 중인 매니저이기 때문.

# 6. follow templates

(a) person.followings.all

(b) person.followers.all

(c) user

(d) person

(e) person.pk
