# MicroPython Lite-Rest Server
This server contains a minimal REST Server with a simple interface.

## Methods
GET and POST are the only two REST calls that have been implemented.

PUT and DELETE have been implemented `optionally` under the Web DAV protocol (Writes files and deletes them from disk).

## Examples

### Create the Server
```python
from src.lite_server.web_server import WebServer
 
server = WebServer(8080, enable_web_dav=False) 
# Default Port is 8008
# Default enable_web_dav is False

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
def post_example(request, response, arg1):
    # Data from the body of the post request will automatically be bound to the function arguments based on the name of the argument.
    # Names of body elements must match the name in the function argument list.
    # Body names must be legal python variable names.
    print(arg1)

    # The request object can be retrieved by adding it to the function arguments.
    print(request)

    # The response object can also be manipulated manually.  Get get the response object, simply add a resposne argument to the function.
    response.set_status(200)
    response.send()
    machine.reset()

    # Any return argument will be ignored if the response body has been set manually.
```

## Built in Web DAV Functions
PUT and DELETE writes direclty to the upython filesystem, and is root accessible.  There is no security, so use this feature cautiously.
