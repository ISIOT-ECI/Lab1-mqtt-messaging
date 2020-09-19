
### Software Engineering for IoT and BigData

### Lab 2 - IoT devices communication (

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

- The manifacturing process should be ON by default.
- The microcontroller must publish, every 2 seconds, the light and temperature readings in a topic on the MQTT broker.
- The requests for stopping the manufacturing process will be posted as a message on another topic on the MQTT broker. Therefore, the microcontroller should be subscribed to such topic, and continiously check for new messages.






Simultaneously, the microcontoller should be able to identify a request to stop the process. These requests wi



- publisher that submits light/temperature readings
- subscriber that get requests from other's side button and performs an action (in this case, turn on the LED)
- 



- 
- A publisher that publishes an action request when a button is pressed
- A subscriber that get data from light/temperature from the remote side, and turns on the leds when values are above certain value, and turn them off when said values are below.




- 
- A LED that will turn on once a certain value on light and temperature are reported, to alert a human operator
- A Button for the human operator to take action

#### Software
- A publisher that publishes an action request when a button is pressed
- A subscriber that get data from light/temperature from the remote side, and turns on the leds when values are above certain value, and turn them off when said values are below.


### Device B - In place controller:
#### In-place sensors
- A photoresistor
- A LED that represents an in-place action

#### Software
- publisher that submits light/temperature readings
- subscriber that get requests from other's side button and performs an action (in this case, turn on the LED)
- 







El laboratorio que estoy armando y que terminaría mañana consiste, en principio, en el siguiente ejercicio:

En grupos de dos personas, van a armar dos circuitos simulando un escenario con dos dispositivos en el que el Dispositivo #1 está dentro de una fábrica controlando un proceso de manufactura (en este caso simulado con mantener un LED encendido) y midiendo parámetros del entorno de dicho proceso (en este caso, la cantidad de luz, y la temperatura ambiente) y transmitiéndolos contínuamente. 
A su vez, el Dispositivo #2 (que estaría ubicado en un sitio remoto) evalúa contínuamente los valores del Dispositivo #1, activando o desactivando alarmas visuales o auditivas (en este caso, serían unos LEDs) deacuerdo con unos intervalos de valores de temperatura y luz determinados. A partir de dichas alarmas visuales, una persona puede decidir detener el proceso del Dispositivo #1 oprimiendo un botón  en Dispositivo #2. Es decir, al oprimir el botón del Dispositivo #2, se generará un evento que debe ser detectado por el Dispositivo #1, a partir del cual debe detener su proceso (en este caso, apagar su LED).



### Device A - Remote monitoring:
#### Hardware configuration
- A LED (optional a buzzer) that will turn on once a certain value on light and temperature are reported, to alert a human operator
- A Button for the human operator to take action

#### Software
- A publisher that publishes an action request when a button is pressed
- A subscriber that get data from light/temperature from the remote side, and turns on the leds when values are above certain value, and turn them off when said values are below.


### Device B - In place controller:
#### In-place sensors
- A photoresistor
- A LED that represents an in-place action

#### Software
- publisher that submits light/temperature readings
- subscriber that get requests from other's side button and performs an action (in this case, turn on the LED)
- 



## Elements

- Install umqtt library packages [through upip (micro-pip)](https://docs.micropython.org/en/latest/reference/packages.html)

	import upip
	upip.install('micropython-umqtt.robust')

- Setup a MQTT broker. It is suggested CloudAMQP (supports MQTT)
- To setup a subscriber

	- s = MQTTClient('pub-52dc166c-2de7-43c1-88ff-f8021142432','hawk.rmq.cloudamqp.com',1883,'ehegpeeg:ehegpeeg','BoUt3xm3z6LTDilYf1yZdCA1BRd3yjxC')

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