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
Article.objects.exclude(title='Qwerty')
Article.objects.all().filter(title='Qwerty').filter(body__startswith='something')

>>> Author.objects.distinct()
>>> Entry.objects.order_by('pub_date').distinct('pub_date')
>>> Entry.objects.order_by('blog').distinct('blog')
>>> Entry.objects.order_by('author', 'pub_date').distinct('author', 'pub_date')
>>> Entry.objects.order_by('blog__name', 'mod_date').distinct('blog__name', 'mod_date')
>>> Entry.objects.order_by('author', 'pub_date').distinct('author')
Lastest :
Edition.objects.order_by('-pub_date')[0]

>>> Task.objects.filter(date__gt=now).order_by('date').values()[0]
{'customer': u'ABCom', 'status': u'Scheduled', 'added': datetime.datetime(2015, 9, 28, 14, 31, 58, 556738, tzinfo=<UTC>), 'ip_addr': u'193.28.87.242', 'office': 2, 'task': u'qwqewqw', 'executor': u'qewqweqwe', 'date': datetime.datetime(2015, 9,
30, 14, 31, tzinfo=<UTC>), 'ticket': u'123123', 'customer_id': u'20', u'id': 29, 'added_by': u'TEST_USER12370783'}

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
<br>
--------------------------------------------------
```python
>>> q1 = User.objects.filter(username__in=["a", "b", "c"])
[<User: a>, <User: b>, <User: c>]
>>> q2 = User.objects.filter(username__in=["c", "d"])
[<User: c>, <User: d>]
```
### Union:
```
This combines and removes duplicates. 
Use q1 | q2 to get [ <User:a> , <User: b> , <User: c> , <User: d> ]
```
### Intersection: 
```
This finds common items. Use q1 and q2 to get [ <User: c> ]
```
### Difference: 
```
This removes elements in second set from first. There is no
logical operator for this. Instead use q1.exclude(pk__in=q2) to get [ <User:
a> , <User: b> ]
```

The same operations can be done using the Q objects:
```python
from django.db.models import Q
# Union
>>> User.objects.filter(Q(username__in=["a", "b", "c"]) | Q(username__
in=["c", "d"]))
[<User: a>, <User: b>, <User: c>, <User: d>]

# Intersection
>>> User.objects.filter(Q(username__in=["a", "b", "c"]) & Q(username__
in=["c", "d"]))
[<User: c>]

# Difference
>>> User.objects.filter(Q(username__in=["a", "b", "c"]) &
~Q(username__in=["c", "d"]))
[<User: a>, <User: b>]
```
Note that the difference is implemented using & (AND) and ~ (Negation).
The Q objects are very powerful and can be used to build very complex queries.
However, the Set analogy is not perfect. QuerySets , unlike mathematical sets,
are ordered. So, they are closer to Python's list data structure in that respect.
