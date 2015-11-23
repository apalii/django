sometimes you can forget what does what, when, and where when dealing with json. 
I know I have to look up the same thing over and over at times. 
This post is everything you need to deal with json "day-to-day" with Django.

### JSON to Dict
One of the first things we, usually, do is convert json data that we get back from a web service call, or from a webhook, into a python datastructure.
```python
import json
json_data = '{"hello": "world", "foo": "bar"}' 
data = json.loads(json_data)
```
The key element from this is the json.loads which loads a string of json and converts the data to a python dict. From there you get to use it like normal.

###Dict to JSON
```python
import json
data = {'baz': 'goo', 'foo': 'bar'}
json_data = json.dumps(data)
```
Normally you want to get your data into json from your dict, or model, which is just as easy using json.dumps. It converts your dict to a string of json so you can return it to in a response.

### HttpResponse with JSON
There are a couple of key parts to returning json properly. You need to have a string of json, and a proper content type.
```python
import json
from django.http import HttpResponse

def fbview(request):
    data = {'foo': 'bar', 'hello': 'world'}
    return HttpResponse(json.dumps(data), content_type='application/json')
```
With this you will send back json properly formatted and with the proper content type so everyone knows what is going on with the data.

### JSONRequestResponseMixin from django-braces
Finally, if you are working with class based views you can use a very convenient mixin in django-braces. JSONRequestResponseMixin which gives you some built-in response methods to return your dicts and models back as json, and it handles everything else.
```python
class APIView(CsrfExemptMixin, JsonRequestResponseMixin):
    def post(self, request, *args, **kwargs):
        data = {'foo': 'bar', 'hello': 'world'}
        return self.render_json_response(data)
```
As you can probably guess the render_json_response method does what the function based view above does by converting the dict to json and returning the proper response.
