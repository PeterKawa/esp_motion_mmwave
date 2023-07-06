<i>Forked from kippesikgithub (thanks!)</i>
Added some links and info, and adjusted to my needs

### LD2410B mmwave Motion detection with temperature, humidity, (lux) sensors for ~€9,-  (housing: ~€6,-)

LD2410B mmwave Motion detection + ESP8266 (Wemos d1 mini) / ESP32-S2 mini Board in ESPHome for Home Assistant. 
Can be combined with temperature, humidity and lux sensor, but I don't use lux sensor here. The LD2410B can be updated to measure luminance as well (I've read somewhere)

#### Shopping list
##### Boards
- ESP8266 (Wemos d1 mini)(€ 2.00): https://nl.aliexpress.com/item/4001157391459.html<br/>
OR
- ESP32-S2 mini (€ 2.20): https://nl.aliexpress.com/item/1005004344359250.html
##### Sensors
- LD2410B (with Bluetooth) sensor (€ 3.50): 
https://a.aliexpress.com/_mqyYb5S
- - cable for LD2410B (€ 1.50): https://nl.aliexpress.com/item/1005004971647691.html
- DHT11 digital Humidity & Temperature sensor (€ 1.00) https://nl.aliexpress.com/item/32840892862.html

###### Only for ESP32-S2:
- Luminance sensor KY-018 3pin (€ 0.80): https://nl.aliexpress.com/item/32820189174.html

##### Housing
- 3D-printed housing: https://www.thingiverse.com/thing:5631878
Price example:
6x housing+lid, white, € 35 all-in, (printics.nl)

![signal-2023-04-07-165048_002](https://user-images.githubusercontent.com/74005072/230629117-bf4672eb-1cd2-47e3-a572-2170de3b5f0c.jpeg)

  
### Step 1
Download this repository: https://github.com/PeterKawa/esp_motion_mmwave/archive/refs/heads/main.zip

### Step 2
##### A. 
copy the code from the downloaded file `uart_read_line_sensor_ld2410v3.h` 
into a new file in the /config/esphome directory, using for example 'Studio Code server'; 

Do the same with the downloaded file `esp8266-template.yaml` and/or `esp32-S2-template.yaml`
##### Or B.
use the 'File editor' and upload those 2 files to /config/esphome

### Step 3 
In HA, install the ESPhome add-on; 

Extended ESPhome how-to:
https://esphome.io/guides/getting_started_hassio.html

### Pin outs
How to connect the stuff

##### Pinout ESP8266 (Wemos d1 mini) Board
![image](https://github.com/PeterKawa/esp_motion_mmwave/assets/74005072/42f1f7d2-fb61-491c-b4b7-2984aa8e8133)

##### ESP8266 | LD2410B  
5V <-> VCC  
GND <-> GND  
TX <-> RX  
RX <-> TX  
D7 <-> OUT  
(ESPHome example code: esp8266-template.yaml)

##### Pinout ESP32-S2 mini Board
![ESP32_S2_mini pinout](https://github.com/PeterKawa/esp_motion_mmwave/assets/74005072/e8d03e0a-b853-443a-b7e0-6c9bee976555)


##### ESP32-S2 | LD2410B<br/>
5V <-> VCC<br/>
GND <-> GND<br/>
GPIO18 <-> RX<br/>
GPIO33 <-> TX<br/>
GPIO5 <-> OUT<br/>
(ESPHome example code: esp32-S2-template.yaml)

### Step 4
Connect the LD2410B cable:

![image](https://user-images.githubusercontent.com/100353268/213939599-cc16b760-055d-4786-9fc2-663132c9dd59.png)

### Step 5
Solder three wires to the DHT11:

![signal-2023-03-03-023238_002](https://user-images.githubusercontent.com/74005072/222615325-db56ee88-5517-4e04-a8bb-0634b4329030.jpeg)

##### ESP8266 | DHT11  
3.3V <-> VDD  
GND <-> GND   
D2 <-> DATA 

##### ESP32-S2 | DHT11  
3V3 <-> VDD  
GND <-> GND   
GPIO9 <-> DATA 

##### LUMI sensor KY-018 3pin
![Screenshot from 2023-06-28 17-03-35](https://github.com/PeterKawa/esp_motion_mmwave/assets/74005072/6807c286-8ba2-4509-bcae-18f55125ff2a)

##### ESP32-S2 | LUMI sensor KY-018 3pin
3V3 <-> Middle pin  
GND <-> - (minus sign)   
GPIO3 <-> S 

Something like this:
![signal-2023-03-03-023401_002](https://user-images.githubusercontent.com/74005072/222612311-f6e99d1f-da2b-482f-a668-9d82682899e3.jpeg)

### Step 6
Make sure you change all the !secret values, or create them in your /config/esphome/secrets.yaml  

### Step 7
_Merge_ (do NOT overwrite), so MERGE the example yaml code (`presence-woonkamer_git.yaml`) to the yaml code of a new device in ESPhome. You should keep the unique device keys and password stuff;
In the end, the new device yaml should look the same as the example yaml, except from these details:
```
# Enable Home Assistant API
api:
  encryption:
    key: "KeepTheGeneratedKey"

```
```
ota:
  password: "KeepOtaPassword"
```
```
  # Enable fallback hotspot (captive portal) in case wifi connection fails
  ap:
    ssid: "KeepDeviceNameAsSsid"
    password: "KeepGeneratedPassword"
```

Once finsihed and sensor is online, you can add it in Home assistant


#### Home Assistant
![Screenshot from 2023-07-06 11-58-56](https://github.com/PeterKawa/esp_motion_mmwave/assets/74005072/af91eb73-e287-4580-9cb6-e78535b3ba1a)


#### Web Config
You can monitor the distance & sensitivity by temporary enabling `show_target_stats`
![Screenshot from 2023-03-03 03-30-41](https://user-images.githubusercontent.com/74005072/222616576-55c012a3-9f28-40b0-b670-20131b6e72cc.png)

#### Impression
Still quite small:
![20230530_200249~01](https://github.com/PeterKawa/esp_motion_mmwave/assets/74005072/c054a4e8-73b5-4284-9585-6a25a5985751)

And hidden from view inside a (fake) flower pot ;-)
![20230601_235500](https://github.com/PeterKawa/esp_motion_mmwave/assets/74005072/02c19245-f45f-44e9-b6d7-53d5c66e8882)


## HLKRadarTool app for configuring LD2410B sensor via Ble
- iphone: https://apps.apple.com/ae/app/hlkradartool/id1638651152
- android: https://www.pgyer.com/Lq8p
- The app is in Mandarin, but it switches to English when you set your phone's language to English

### Other sources used  
https://community.home-assistant.io/t/mmwave-wars-one-sensor-module-to-rule-them-all/453260/2
  
https://github.com/rain931215/ESPHome-LD2410
  
