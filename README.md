Forked from kippesikgithub (thanks!) 
Added some links and info, and adjusted to my needs

### LD2410B mmwave Motion detection with temperature and humidity sensor for ~€8,-  (housing: ~€6,-)

LD2410B mmwave Motion detection + ESP8266 (Wemos d1 mini) Board in ESPHome for Home Assistant. 
Can be combined with temperature, humidity and lux sensor, but I don't use lux sensor here. The LD2410B can be updated to measure luminance as well (I've read somewhere)

Shopping list
- ESP8266 (Wemos d1 mini)(E 2.00): https://nl.aliexpress.com/item/4001157391459.html
- LD2410B (with Bluetooth) sensor (E 3.50): 
https://a.aliexpress.com/_mqyYb5S
- cable for LD2410B (E 1.50): https://nl.aliexpress.com/item/1005004971647691.html
- DHT11 digital Humidity & Temperature sensor (E 1.00) https://nl.aliexpress.com/item/32840892862.html

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

Do the same with the downloaded file `esp8266-template.yaml`
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

### Step 4
Connect the LD2410 cable:
![image](https://user-images.githubusercontent.com/100353268/213939599-cc16b760-055d-4786-9fc2-663132c9dd59.png)

##### ESP8266 | LD2410B  
5V <-> VCC  
GND <-> GND  
TX <-> RX  
RX <-> TX  
D7 <-> OUT  

### Step 5
Solder three wires to the DHT11:
![signal-2023-03-03-023238_002](https://user-images.githubusercontent.com/74005072/222615325-db56ee88-5517-4e04-a8bb-0634b4329030.jpeg)

##### ESP8266 | DHT11  
3.3V <-> VDD  
GND <-> GND   
D2 <-> DATA 

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
![Screenshot from 2023-03-03 03-26-59](https://user-images.githubusercontent.com/74005072/222616032-f306ec58-261c-4068-8ed8-fb3bc4e97893.png)


#### Web Config
You can monitor the distance & sensitivity by temporary enabling `show_target_stats`
![Screenshot from 2023-03-03 03-30-41](https://user-images.githubusercontent.com/74005072/222616576-55c012a3-9f28-40b0-b670-20131b6e72cc.png)

#### Impression
Still quite small:
![20230530_200249~01](https://github.com/PeterKawa/esp_motion_mmwave/assets/74005072/c054a4e8-73b5-4284-9585-6a25a5985751)

And hidden from view inside a (fake) flower pot ;-)
![20230601_235500](https://github.com/PeterKawa/esp_motion_mmwave/assets/74005072/02c19245-f45f-44e9-b6d7-53d5c66e8882)

### Other sources used  
https://community.home-assistant.io/t/mmwave-wars-one-sensor-module-to-rule-them-all/453260/2
  
https://github.com/rain931215/ESPHome-LD2410
  
