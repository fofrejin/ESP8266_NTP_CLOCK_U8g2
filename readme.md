# ESP8266 NTP CLOCK U8g2
Project uses [U8g2](https://github.com/olikraus/u8g2) lib for drawing on display, so you can choose whatever display you want from a large U8g2 support list. Don't forget to change font which is best suitable for your display. [List of fonts](https://github.com/olikraus/u8g2/wiki/fntlistall) you can find on [U8g2 github wiki page](https://github.com/olikraus/u8g2/wiki).

#### To install the ESP8266 board, (using Arduino 1.6.4+):
  - Add the following 3rd party board manager under `"File -> Preferences -> Additional Boards Manager URLs"`:  
http://arduino.esp8266.com/stable/package_esp8266com_index.json
  - Open the `"Tools -> Board -> Board Manager"` and click install for the ESP8266
  - Select your ESP8266 in `"Tools -> Board"`  

#### Used libraries(can be found in Arduino library manager):
  - [U8g2](https://github.com/olikraus/u8g2)
  - [NTPClient](https://github.com/arduino-libraries/NTPClient)

#### Getting started:
By default sketch uses MAX7219 32X8 LED MATRIX DISPLAY which may be changed by commenting 
```c
U8G2_MAX7219_32X8_F_4W_SW_SPI u8g2(U8G2_R0, /* clock=*/ 14, /* data=*/ 13, /* cs=*/ 15, /* dc=*/ U8X8_PIN_NONE, /* reset=*/ U8X8_PIN_NONE);
```
and uncommenting desired line with your display name.  

Connecting to WiFi:
All you need is to specify your WiFi SSID and password in corresponding lines:
```c
const char *ssid     = "your_ssid"; //Your WiFi SSID
const char *password = "your_pass"; //Your WiFi password
```

Also you may change desired NTP server, offset(in seconds, 3600 is for +1 hour) and time sync interval(in milliseconds, 60000 is for 1 minute).
```c
NTPClient timeClient(ntpUDP, "pool.ntp.org", 3600, 60000);
```

Brightness control:
Brightness is changing depending of time of the day. In following line you may specify some parameters for this(max_bright is 100):
```c
u8g2.setContrast( getDaytimeBrightness(/*min_bright*/1, /*max_bright*/60, /*min_bright_start_hour*/18, /*min_bright_end_hour*/10) );
```
