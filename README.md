# MicroPython Lite-Rest Server
This server contains a minimal REST Server with a simple interface.


## Example Usage

```python
import json
 
from src.lite_server.web_server import WebServer
 
 
def start_webserver(sensor):
    server = WebServer()
 
    @server.GET("/hello_world")
    def hello_world():
        print("Hello World")

	# The response object will be automatically generated from the return value of the Function
        return json.dumps({"msg": "Hello World!"})

    @server.POST("/post_example")
    def post_example(response):
	# The response object can also be manipulated manually.  Get get the response object, simply add a resposne argument to the function.
        response.set_status(200)
        response.send()
        machine.reset()

def connect(cb):
    import network
    sta_if = network.WLAN(network.STA_IF)
    if not sta_if.isconnected():
    	wifi_name = "wifi"
	wifi_pass = "password"

        print(f"connecting to WiFi: {wifi_name}.")
        sta_if.active(True)
        sta_if.connect(wifi_name, wifi_pass)

	# Noop until connected
        while not sta_if.isconnected():
            pass

    print('network config:', sta_if.ifconfig())
    cb()
 
 def main():
    cb = lambda: start_webserver(sensor)
    connect(cb)

 if __name__ == "__main__":
 	main()
```
