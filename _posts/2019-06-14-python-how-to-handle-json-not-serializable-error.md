---
title: "python: how to handle json not serializable error"
date: 2019-06-14 20:55:19
categories: python json
---

While using json.dumps() or flask's jsonify to make something into json format, you may face the following error.

```
TypeError: Object of type ??? is not JSON serializable
```

This error is raised because the above type ??? does not support the conversion to string. So you may handle the issue by providing your own custom conversion function to the json encoder. This is how to do it.

```python 
# if the type is date
def json_default(value): 
    if isinstance(value, datetime.date): 
        return value.strftime('%Y-%m-%d') 
    raise TypeError('not JSON serializable') #you may choose not to raise the Error though 

data = {'date': datetime.date.today()} 
json_data = json.dumps(data, default=json_default)
```

```python 
# if the type is bytes
def json_default(value): 
    if isinstance(value, bytes): 
        return value.decode('utf-8') 
    raise TypeError('not JSON serializable')

data = {'data': bytecodes} 
json_data = json.dumps(data, default=json_default)
```

It's a bit different for jsonify to make a custom handler for unsupported types.

```python 
import decimal
from flask import Flask, json

class MyJSONEncoder(json.JSONEncoder):

    def default(self, obj):
        if isinstance(obj, decimal.Decimal):
            # Convert decimal instances to strings.
            return str(obj)
        return super(MyJSONEncoder, self).default(obj)


app = Flask(...)
app.json_encoder = MyJSONEncoder
```