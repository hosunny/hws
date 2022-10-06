# 1. . N:1 True or False

    (1) T

    (2) F (DB api 를 통해 참조 가능)

    (3) T

    (4) F (유니크하다면 가능)

# 

# 2. ForeignKey column name

* answer_id
* articles_comment

# 

# 3. N:1 model manager

* question.comment_set.all

# 

# 4. next parameter

* 405에러
  
  ```python
  @require_POST
  def delete(request, article_pk):
      if request.user.is_authenticated:
          article = get_object_or_404(Article, pk=article_pk)
          article.delete()
          return redirect('articles:index')
     return redirect('articles:detail', article_pk)
  ```
