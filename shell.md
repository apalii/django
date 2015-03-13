Model class : 
```python
class Task(models.Model):

    class Meta():
        db_table = 'task'
        ordering = ['date']

    STATUSES = (
        (u'Scheduled', u'Scheduled'),
        (u'Done', u'Done'),
        (u'In progress', u'In progress'),
        (u'Postponed', u'Postponed'),
        (u'Partially', u'Partially'),
        (u'Cancelled', u'Cancelled'),
        (u'Failed', u'Failed'),
    )
    ticket = models.CharField(max_length=30)
    date = models.DateTimeField()
    customer = models.CharField(max_length=30)
    task = models.CharField(max_length=200)
    executor = models.CharField(max_length=20)
    status = models.CharField(max_length=20, choices=STATUSES)

    def __unicode__(self):
        return "{} : {}".format(str(self.id), self.ticket)
```
### Shell actions :

```python
from app_tasks.models import Task as a
from django.utils import timezone

In [7]: instance = a(ticket='Test', task='some text', date=timezone.now(), likes=3)
In [8]: instance.save()
In [9]: instance.id
Out[9]: 3
```
#### Filtering
```python
Article.objects.filter(title__startswith='Qwerty')
Article.objects.filter(title='Qwerty')

Article.objects.all().filter(title='Qwerty').filter(body__startswith='something')
```
#### Updating
```python

>>> t.objects.filter(status__startswith='Sch')
[<Task: 1 : 400456>, <Task: 3 : 425321>]
>>> t.objects.filter(id='1').update(status='Schduled')
1
>>> t.objects.filter(id='3').update(status='Schduled')
3
```
