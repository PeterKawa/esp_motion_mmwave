Forked from kippesikgithub (thanks!) 
Added some links and info, and adjusted to my needs

# LD2410 mmwave Motion detection

LD2410 mmwave Motion detection + ESP8266 (Wemos d1 mini) Board in ESPHome for Home Assistant. 
Can be combined with temperature, humidity and lux sensor, but I don't use lux sensor here.

Shopping list
- ESP8266 (Wemos d1 mini): https://nl.aliexpress.com/item/4001157391459.html
- LD2410 sensor: https://nl.aliexpress.com/item/1005004786874722.html
- cable for LD2410: https://nl.aliexpress.com/item/1005004971647691.html
- DHT11 digital Humidity & Temperature sensor https://nl.aliexpress.com/item/32840892862.html

- 3D Printed box: https://www.thingiverse.com/thing:5631878
  
### Step 1
Install the ESPhome add-on;

Then copy the code from uart_read_line_sensor_ld2410v3.h into a new file in the /config/esphome directory, using for example Studio Code server

### Step 2
### Pin outs

![image](https://user-images.githubusercontent.com/100353268/213939599-cc16b760-055d-4786-9fc2-663132c9dd59.png)

#### Pinout ESP8266 (Wemos d1 mini) Board

##### ESP8266 | LD2410  
5V <-> VCC  
GND <-> GND  
TX <-> RX  
RX <-> TX  
D7 <-> OUT  

##### ESP8266 | DHT11  
3.3V <-> VDD  
GND <-> GND   
D2 <-> DATA 

![signal-2023-03-03-023238_002](https://user-images.githubusercontent.com/74005072/222615325-db56ee88-5517-4e04-a8bb-0634b4329030.jpeg)


#### Example including ESP8266 + DHT11 sensor  
esphome example code: `presence-woonkamer_git.yaml`

![signal-2023-03-03-023401_002](https://user-images.githubusercontent.com/74005072/222612311-f6e99d1f-da2b-482f-a668-9d82682899e3.jpeg)

#### Step 3
Make sure you change all the !secret values, or create them in your esphome secrets  

#### Step 4
Add example code to the yaml code of a new device in ESPhome  
Once finsihed and sensor is online, you can add it in Home assistant or visit the webpage of the device.

#### Home Assistant
![Screenshot from 2023-03-03 03-26-59](https://user-images.githubusercontent.com/74005072/222616032-f306ec58-261c-4068-8ed8-fb3bc4e97893.png)


#### Web Config
You can monitor the distance & sensitivity by temporary enabling `show_target_stats`
![Screenshot from 2023-03-03 03-30-41](https://user-images.githubusercontent.com/74005072/222616576-55c012a3-9f28-40b0-b670-20131b6e72cc.png)


## other sources used  
https://community.home-assistant.io/t/mmwave-wars-one-sensor-module-to-rule-them-all/453260/2
  
https://github.com/rain931215/ESPHome-LD2410
  
