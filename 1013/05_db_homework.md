# 1. MTV

* model
  
  * 응용프로그램의 데이터 구조를 정의하고 데이터베이스의 기록을 관리(추가, 수정, 삭제)

* template
  
  * 파일의 구조나 레이아웃을 정의
  
  * 실제 내용을 보여주는 데 사용(presentation)

* view
  
  * HTTP 요청을 수신하고 HTTP 응답을 반환
  
  * Model을 통해 요청을 충족시키는데 필요한 데이터에 접근
  
  * 그리고 탬플릿에게 응답의 서식 설정을 맡김

# 2. 404 Page not Found

(a) : articles

(b) : views

(c) : views.index, name='index'

# 3. templates and static

(a) : settings.py

(b) : TEMPLATES

(c) : STATICFILES_DIRS

# 4. Migration

```bash
1) python manage.py makemigrations (articles)
2) python manage.py showmigrations articles
3) python manage.py sqlmigrate articles <migration-name>
4) python manage.py migrate (articles)
```

# 5. ModelForm True or False

1) F: 데이터를 전달하는 body의 유무 (POST 요청은 body, GET 요청은 params로 데이터를 전달)

2) T
3. F: AuthenticationForm은 ModelForm이 아닌 일반 Form을 상속 받는다 

4. T

# 6. media 파일 경로

```python
# settings.py

# 사용자가 업로드 한 파일을 보관할 디렉토리의 절대 파일 시스템 경로
MEDIA_ROOT = BASE_DIR / 'crud' / 'uploaded_files'

# MEDIA_ROOT에서 제공되는 미디어 파일을 처리하는 URL
MEDIA_URL = '/media/'
```

# 7. DB True or False

1) T

2) F: SQL 명령어는 대소문자 구분을 하지 않는다.

3) T

4) T

5) F: 여러개의 테이블 생성이 가능하다.

# 8. on_delete

(a) PROTECT

# 9. like in models

(a) ManyToManyField

(b) related_name

# 10. follow in models

- accounts_user_followings
- from_user_id`, `to_user_id
