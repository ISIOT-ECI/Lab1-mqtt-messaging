
### Software Engineering for IoT and BigData

### Lab 2 - IoT devices communication

### Exercise to be done by groups of two students.

### Required elements.

1. Elements from [Lab-01]()

### Lab Goal

In this exercise, you and your partner will build two separate IoT devices (microcontroller + electronic circuit) that communicate with each other. Together, these two devices will simulate an scenario where the Device A is in a factory, controlling a manufacturing process, continiously measuring and transmitting the environment parameters of the process. The Device B (placed out of the factory), on the other hand, will receive the aforementioned environment parameters, and based on their values, it will trigger a visual alarms to alert a human operator. The human operator, once the visual alarms are triggered, should be able to decide to stop the process being carried by Device B by pressing a button on the Device A's circuit. The human operator should be able to resume the process when he decides it is convenient, therefore, the environment variables should continue to be transmitted regardless the process is running or stopped.


### Device A - Monitoring device in the factory:
#### Hardware configuration
- A ESP8266 microcontroller, with a photoresistor and a humidity/temperature sensor (DHT11) circuits connected to it, as in [Lab-01]().
- To represent the manufacturing process state, a LED will be also included (ON = process in action, OFF = process stopped)

#### Microcontroller Software
- The manifacturing process should be ON by default.
- The microcontroller must publish, every 2 seconds, the light and temperature readings in a topic on the MQTT broker.
- The requests for stopping or resuming the manufacturing process will be posted as a message on another topic on the MQTT broker. Therefore, the microcontroller should be subscribed to such topic, and continiously check for new messages. In this prototype, the effect of receiving a STOP or RESUME message is simply turning OFF and ON the LED.


### Device B - Remote monitoring and control:
#### Hardware configuration
- A ESP8266 microcontroller, with a two leds, one as an alarm for Temperature and the other as an alarm for Ligh intensity in the environment.
- A push-button circuit, as in [Lab-01](), attached to one of the microcontroller's digital pins.

#### Microcontroller Software
- The microcontroller should be subscribed to the topic (or topics) where temperature and light readings will be published by Device A. When such values are above a given threshold, the corresponding LED should be turned on. Likewise, the LEDs should be turned off once the values are below their corresponding thresholds.
- Pressing the push button should post a STOP or RESUME message (depending on the status of the process) on the corresponding topic. In this case, you should consider using hardware interruputs, as in Lab-01, to detect when the button was pushed.



## Additional considerations

1. It is recommended to use the official micripython's MQTT client libraries: [umqtt.robust](https://github.com/micropython/micropython-lib/tree/master/umqtt.robust).

	You can install these libraries throug [upip (micro pip)](https://docs.micropython.org/en/latest/reference/packages.html), by opening a REPL prompt (as in Lab-00) and entering:

	```python
	import upip
	upip.install('micropython-umqtt.robust')
	```

	You can check the [documentation of this library](https://pypi.org/project/micropython-umqtt.simple/) or the [umqtt.simple source code](https://github.com/micropython/micropython-lib/blob/master/umqtt.simple/umqtt/simple.py) (which is fairly simple and mostly documented) to see the parameters of the *publish*, *subscribe*, *set_callback*, *wait_msg* and *check_msg* methods. Pay special attention to the difference between *wait_msg* and *check_msg*.

2. We suggest to use a free plan of [CloudAMQP](https://www.cloudamqp.com/) as the MQTT broker. Once you have configured your broker, you can check in the instance details its HOST (Load Balanced), USER & VHOST, and PASSWORD. When using this broker with umqtt, take the following into consideration:
	- To make a connection to the broker, the user string is the user given by CloudAMQP, but twice, sepparated by a colon. E.g. if the user is *exegpeeg*, the user is given to the mqtt client as follows:

		```python
		sub = MQTTClient('unique-identifier','thehost.com',1883,'exegpeeg:exegpeeg','ThePassword')
		```
	- The topics must have the above username as a prefix. For example, for the above user to subscribe or to post data on the broker's topic '/feeds/data', it must use 'exegpeeg:exegpeeg/feeds/data'. For example:

		```python
		client.publish('exegpeeg:exegpeeg/feeds/data', '33')
		```

3. In this laboratoriy one of the devices needs to perform two tasks simultaneously: posting data from the sensors, and checking 

4. Use the [microcontroller's unique ID](https://docs.micropython.org/en/latest/library/machine.html) as MQTT client's unique identifier.






	- sub.connect()
	- set callback
	- use either one-shot events poll, or synchronous event poll.

- a publisher (.publish)
- considerations about topics
- Device A: 


 from umqtt.robust import MQTTClient

https://boneskull.com/micropython-on-esp32-part-2/

import upip
upip.install('micropython-umqtt.robust')

 def __init__(self, client_id, server, port=0, user=None, password=None, keepalive=0,
                 ssl=False, ssl_params={}):


import upip
>>> upip.install('uasyncio')                 
                 
https://forum.micropython.org/viewtopic.php?t=7334

                 
client = MQTTClient('52dc166c-2de7-43c1-88ff-f8021142432','hawk.rmq.cloudamqp.com',1883,'ehegpeeg:ehegpeeg','BoUt3xm3z6LTDilYf1yZdCA1BRd3yjxC')

https://makeblock-micropython-api.readthedocs.io/en/latest/public_library/Third-party-libraries/mqtt.html

client.publish('ehegpeeg:ehegpeeg/feeds/data', '33')

client.wait_msg('')

client.publish('sensors/feeds/temperature', '33')
client.publish('sensors/feeds/temperature', '45')      
                 
                 #springboot\u00e9\u0085\u008d\u00e7\u00bd\u00ae
server.port=8080
#mqtt\u00e6\u009c\u008d\u00e5\u008a\u00a1\u00e5\u0099\u00a8\u00e9\u0085\u008d\u00e7\u00bd\u00ae
mqtt.broker.serverUri=tcp://hawk.rmq.cloudamqp.com:1883
mqtt.broker.username=ehegpeeg:ehegpeeg
mqtt.broker.password=BoUt3xm3z6LTDilYf1yZdCA1BRd3yjxC
mqtt.clientId=cloudapp
mqtt.topic=ehegpeeg:ehegpeeg/feeds/data
mqtt.qos=1
mqtt.completionTimeout=5000