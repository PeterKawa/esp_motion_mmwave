Forked from kippesikgithub (thanks!) 
Added some links and info, and adjusted to my needs

# LD2410 mmwave Motion detection

LD2410 mmwave Motion detection + ESP8266 (Wemos d1 mini) Board in ESPHome for Home Assistant. 
Can be combined with temperature, humidity and lux sensor, but I don't use lux sensor here.
- LD2410 sensor: https://nl.aliexpress.com/item/1005004786874722.html
- cable for LD2410: https://nl.aliexpress.com/item/1005004971647691.html
- DHT11 digital Humidity & Temperature sensor https://nl.aliexpress.com/item/32840892862.html

3D Printed box used: https://www.thingiverse.com/thing:5631878
  
### Step 1
Copy the code from uart_read_line_sensor_ld2410v3.h into a new file in the esphome directory, using for example Studio Code server

### Step 2
Pin outs
![image](https://user-images.githubusercontent.com/100353268/213939599-cc16b760-055d-4786-9fc2-663132c9dd59.png)

#### Pinout ESP8266 (Wemos d1 mini) Board
esphome example code: esp-motion-toilet.yaml  
ESP8266 | LD2410  
5V <-> VCC  
GND <-> GND  
TX <-> RX  
RX <-> TX  
D7 <-> OUT  
![image](https://user-images.githubusercontent.com/100353268/213941685-f02bab19-3bf9-4c9e-8396-ed6582ae09ed.png)

ESP8266 | DHT11  
3.3V <-> VDD  
GND <-> GND   
D2 <-> DATA 
![signal-2023-03-03-023238_002](https://user-images.githubusercontent.com/74005072/222612204-518f1a7c-2aea-4dfc-9676-b5e277973766.jpeg)

  
#### Example including ESP8266 + DHT11 sensor  
esphome example code: 
![signal-2023-03-03-023401_002](https://user-images.githubusercontent.com/74005072/222612311-f6e99d1f-da2b-482f-a668-9d82682899e3.jpeg)


#### Step 3
Make sure you change all the !secret values, or create them in your esphome secrets  


#### Step 4
Add it to the yaml code of a new device in ESPhome  
Once finsihed and sensor is online, you can add it in Home assistant or visit the webpage of the device.

#### Home Assistant
![image](https://user-images.githubusercontent.com/100353268/213941863-d037745b-490f-4d33-95c3-a1122b4e0908.png)

#### Web Config
![image](https://user-images.githubusercontent.com/100353268/213941881-8a898fc7-f863-49ce-811d-e8e2b4ab90b9.png)
![image](https://user-images.githubusercontent.com/100353268/213941904-7c9577e7-99bc-47e8-b3ce-d7743633914d.png)


## other sources used  
https://community.home-assistant.io/t/mmwave-wars-one-sensor-module-to-rule-them-all/453260/2
  
https://github.com/rain931215/ESPHome-LD2410
  
