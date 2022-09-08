![](C:\Users\SSAFY\AppData\Roaming\marktext\images\2022-09-08-14-24-16-image.png)

```python
{% extends 'base.html' %}

{% block content %}
  <h1>비밀번호변경</h1>
  <form action="{% url 'accounts:change_password' %}" method="POST">
    {% csrf_token %}
    {{ form.as_p }}
    <input type="submit">
  </form>
{% endblock content %}
```
