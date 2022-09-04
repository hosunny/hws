# 1. 한국어로 번역하기

## 1-1

```python
LANGUAGE_CODE = 'ko-kr'
```

## 1-2

```python
USE_I18N
```



# 2. 경로 설정하기

```python
path('ssafy/', views.ssafy)
```



# 3. Django Template Language

1. `a: menu`

2. `a : forloop.counter0`

3. `a : empty`

4. `a : if`, `b : else`, `c: endif`

5. `a : length`, `b : title`

6. `a : Y년 m월 d일 (D) A h:i`



# 4. Form tag with Django

1. 데이터를 보낼 경호 지정

2. `GET`, `POST`

3. `HOST:PORT/create/?title=안녕하세요&content=반갑습니다&my-site=파이팅`
