# MicroPython Lite-Rest Server
This server contains a minimal REST Server with a simple interface.


## Examples

### Create the Server
```python
from src.lite_server.web_server import WebServer
 
server = WebServer()

```

### GET Request

```python
import json

@server.GET("/hello_world")
def hello_world():
    print("Hello World")

    # The response object will be automatically generated from the return value of the Function
    return json.dumps({"msg": "Hello World!"})
```

### POST Request
```python
@server.POST("/post_example")
def post_example(response):
    # The response object can also be manipulated manually.  Get get the response object, simply add a resposne argument to the function.
    response.set_status(200)
    response.send()
    machine.reset()
```
