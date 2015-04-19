```
pip install django-tastypie

INSTALLED_APPS = (
+   'tastypie',
)

urlpatterns = patterns('',
+   url(r'^api/', include(task_resource.urls)),
)
create file api.py with the following code inside:
from tastypie.resources import ModelResource
from tastypie.constants import ALL
from models import Task
class TaskResource(ModelResource):
    class Meta:
        queryset = Task.objects.all()
        resource_name = 'task'
        filtering = {'task': 'contains'}

After that it is possible to use REST-ful API services:

http://tasks-215255.euw1.nitrousbox.com/tasks/api/task/?format=json
http://tasks-215255.euw1.nitrousbox.com/tasks/api/task/3/
http://tasks-215255.euw1.nitrousbox.com/tasks/api/task/?format=json&task__contains=App
```
