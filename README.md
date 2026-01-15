HamHacks Dash v4
A custom ESP32‑powered touchscreen dashboard for Home Assistant
HamHacks Dash v4 is a fully custom smart‑home control panel built on the ESP32 with a 320×240 TFT display and XPT2046 touch controller. It provides instant control of Home Assistant devices via MQTT, with smooth UI updates, sleep/wake handling, and a clean, responsive interface.
This version removes the terminal page for maximum stability and includes a simplified About page showing WiFi, IP, and uptime.

⭐ Features
- 6 interactive tiles for lights, blinds, and custom devices
- Instant colour updates when Home Assistant changes state
- MQTT command + state sync
- Smooth touch handling (no double‑press, no jitter)
- Automatic sleep + wake with backlight control
- Custom SPI bus for XPT2046 touch
- About page with:
- Firmware version
- WiFi SSID
- IP address
- Uptime
- RGB LED pins included but unused (reserved for future features)

🖥 Hardware Requirements
- ESP32 (DevKit or equivalent)
- 320×240 TFT display (ILI9341 via TFT_eSPI)
- XPT2046 touch controller
- RGB LED (optional)
- Backlight pin (PWM‑controlled)




PWM Channels
CH_R  = 0  
CH_G  = 1  
CH_B  = 2  
CH_BL = 3  



📡 MQTT Setup
The firmware uses:
- Command topics (to control devices)
- State topics (to update tile colours)
Example:
homeassistant/light/media_wall/set
homeassistant/light/media_wall/state


You must edit the arrays in the code:
cmdTopic[]
stateTopic[]


to match your Home Assistant MQTT entities.

🌐 WiFi + MQTT Credentials
Set these at the top of the sketch:
const char* wifi_ssid     = "YOUR_WIFI_SSID";
const char* wifi_password = "YOUR_WIFI_PASSWORD";

const char* mqtt_server   = "YOUR_MQTT_BROKER_IP";
const int   mqtt_port     = 1883;
const char* mqtt_user     = "YOUR_MQTT_USERNAME";
const char* mqtt_pass     = "YOUR_MQTT_PASSWORD";



🖼 UI Layout
The HOME screen displays 6 tiles:
[ Media ] [ Egglamp ] [ Living ]
[ Blinds ] [ Dev5    ] [ Dev6  ]


Each tile:
- Toggles the device on touch
- Sends MQTT command
- Updates colour instantly
- Updates again when HA publishes state

😴 Sleep + Wake
- Screen sleeps after 60 seconds
- Backlight fades to 0
- First touch wakes the screen
- Second touch interacts normally

📄 About Page
Shows:
- HamHacks Dash v4
- WiFi SSID
- IP address
- Uptime
Tap the bottom area to return home.

🛠 Libraries Required
Install via Arduino Library Manager:
- TFT_eSPI
- XPT2046_Touchscreen
- PubSubClient
- WiFi.h (built‑in)
Make sure your TFT_eSPI/User_Setup.h matches your display wiring.

🚀 Flashing
- Open the .ino file in Arduino IDE
- Select your ESP32 board
- Install required libraries
- Flash at 115200 baud
- Reboot and check serial monitor

📌 Notes
- RGB LED functions are included but disabled in v4
- Terminal page removed for maximum stability
- Touch smoothing and debounce tuned for CYD hardware
- MQTT redraws only occur on HOME page

📜 License
MIT License — free to modify, fork, and improve.
