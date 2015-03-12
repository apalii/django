Model class : 
```python
class Article(models.Model):
    title = models.CharField(max_length=200)
    body = models.TextField()
    pub_date = models.DateTimeField('date published')
    likes = models.IntegerField()

    def __unicode__(self):
        return self.title
```
### Shell actions :

```python
In [2]: from app_article.models import Article as a
In [5]: a.objects.all()
Out[5]: [<Article: Test 1>, <Article: Test 2>]

In [6]: from django.utils import timezone
In [7]: instance = a(title='Test 777', body='some text', pub_date=timezone.now(), likes=3)
In [8]: instance.save()
In [9]: instance.id
Out[9]: 3
In [10]: a.objects.all()
Out[10]: [<Article: Test 1>, <Article: Test 2>, <Article: Test 777>]
```
#### aditional
```python
Article.objects.filter(title__startswith='Qwerty')
Article.objects.filter(title='Qwerty')

Article.objects.all().filter(title='Qwerty').filter(body__startswith='something')
```
