#Import Modules
import Adafruit_DHT
import time
import requests

#Adafruit_DHT.DHT11, Adafruit_DHT.DHT22 or Adafruit_DHT.AM2302.
sensor = Adafruit_DHT.DHT22
pin = 4
humidity, temperature = Adafruit_DHT.read_retry(sensor, pin)
 
#Display Currnt Temp / Humity for testing
#print 'Temp={0:0.1f}*C  Humidity={1:0.1f}%'.format(temperature, humidity)

#PRTG Connection
prtg_host = '192.168.#.#'
prtg_host_port = '5050'
prtg_sensor_token = '#'

def get_values():
    temp = '{0:0.1f}'.format(temperature, humidity)
    humi = '{1:0.1f}'.format(temperature, humidity)

    json_response = {
        "prtg": {
            "result": [
                {
                    "channel": "temperature",
                    "float": 1,
                    "value": temp
                },
                {
                    "channel": "ext temperature",
                    "float": 1,
                    "value": humi
                }
            ]
        }
    }
    return json_response

#Post values to PRTG
json_response = get_values()
json_string = str(json_response)
json_string = str.replace(json_string, '\'', '\"')
prtg_request_URL = 'http://' + prtg_host + ':' + prtg_host_port + '/' + prtg_sensor_token + '?content=' + json_string
request = requests.get(prtg_request_URL)
