#### How to deal with sessions

```python
from django.contrib.sessions.models import Session

s = Session.objects.get(pk='2b1189a188b44ad18c35e113ac6ceead')
s.expire_date
```

#### How to deal with coonections

```python
from django.db import connection
coonections.queries
```
