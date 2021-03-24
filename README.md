# ** ESP8266 & VS1053 Wifi WebRadio ** #

### Ka-Radio, a WiFi shoutcast player based on ESP8266 and VS1053b chips</br>
See also the esp32 version at https://github.com/karawin/Ka-Radio32</br>

## Basic informations<BR/>
### New
A new android application is born
  
- KaRadio Remote Control by Vassilis Serasidis on google Play.

It is an easy and fast WiFi remote control for your KaRadio or KaRadio32 hardware.  
With this android app you can select the WebRadio station you want to play, set the volume and get the station information such as Station name, Genre, Bit rate, Meta data and more.   
Found it at
https://play.google.com/store/apps/details?id=com.serasidis.karadio.rc

Thanks Vassilis.  
###  
### Release 1.9 R8 - Built on 2021/01/01

#### Add On: add a lcd, a remote control, and other goodies: see https://github.com/karawin/Karadio-addons 

#### Attention:
The optional led is now on GPIO2. The blue led on the ESP8266 is blinking at the same rate.  
GPIO16 is now the Chip select for the external ram if any.<BR/>
The external ram is detected at boot time if present.    
To load this release, please flash   
boot_v1.6.bin at 0x0000,  
user1.4096.new.4.bin at 0x1000 ,  
user2.4096.new.4.bin at 0X81000,  
esp_init_data_default.bin at 0x3FC000   
and blank.bin at	0x3fe000   
After that, all next updates are done with the On The Air (OTA) feature.  
<BR/>  
See also https://hackaday.io/project/11570-wifi-webradio-with-esp8266-and-vs1053   


#### Loading the esp8266
The binaries are on ESP8266-Firmware/bin/upgrade/

#### First use
- If the access point of your router is not known, the webradio inits itself as an AP. Connect the wifi of your computer to the ssid "WifiWebRadio",  
- Browse to 192.168.4.1 to display the page, got to "setting" "Wifi" and configure your ssid ap, the password if any, the wanted IP or use dhcp if you know how to retrieve the dhcp given ip (terminal or scan of the network).
- In the gateway field, enter the ip address of your router.
- Validate. The equipment restart to the new configuration. Connect your wifi to your AP and browse to the ip given in configuration.
- Congratulation, you can edit your own station list. Dont forget to save your stations list in case of problem or for new equipments.
- if the AP is already know by the esp8266, the default ip is given by dhcp.
- a sample of stations list is on https://github.com/karawin/Ka-Radio/blob/master/ESP8266-Firmware/WebStations.txt . Can be uploaded via the web page.   
- Karadio can be controlled by the web interface or by the uart interface or by telnet. List of commands: type help  
- See the list of command at http://karadio.karawin.fr/Interface.txt  
<img src="https://github.com/karawin/ESP8266-WebRadio/blob/master/Images/webradio3mini.jpg" alt="screenshot" border=0> 

### Generate Ka-Radio
see the http://karadio.karawin.fr/readme.txt file.

### History:
- Based on https://github.com/PiotrSperka/ESP8266-WebRadio<br />
- New development based on the new https://github.com/espressif/ESP8266_RTOS_SDK<br />
- Compiled with [esp-open-sdk](https://github.com/pfalcon/esp-open-sdk)<br />
- Compatible with mobile<br />
- Stable<br />
- tools to save and restore the stations database<br /><br />
- prototype made with:<br />
-- http://fr.aliexpress.com/item/MB102-Breadboard-Power-Supply-Module-3-3V-5V-For-Solderless-Breadboard/2027279953.html (0.74 euros)<br />
-- http://www.ebay.fr/itm/121775761053?_trksid=p2057872.m2749.l2649&ssPageName=STRK%3AMEBIDX%3AIT  (3,09 euros)<br />
-- http://www.ebay.fr/itm/401046111343?_trksid=p2060353.m2749.l2649&ssPageName=STRK%3AMEBIDX%3AIT  (6 euros)<br />
-- http://www.ebay.fr/itm/131683794035?_trksid=p2060353.m2749.l2649&ssPageName=STRK%3AMEBIDX%3AIT  (1.05 euros)<br />
-- http://fr.aliexpress.com/item/USB-to-TTL-converter-UART-module-CH340G-CH340-3-3V-5V-switch/32392228218.html?detailNewVersion=2 (0.59 euro)<br />
-- some wires ...<br /><br />
- Wiring: <br />
From ESP8266_ESP12( 3.3 v) to VS1053 (5 v)<br />
REST<br />
ADC   if control panel is not used, this input must be grounded.<br />
CH_PD to 3.3v<br />
GPIO16 (a 1Hz output)<br />
GPIO14 to VS1053 SCK<br />
GPIO12 to VS1053 MISO<br />
GPIO13 to VS1053 MOSI<br />
<br />
TXD to   CH340G UART rx<br />
RXD from CH340G UART tx<br />
GPIO05 to VS1053 XDCS<br />
GPIO04 to VS1053 DREQ<br />
GPIO00 to VS1053 XRST<br />
GPIO02<br />
GPIO15 to VS1053 XCS<br />
<br/>
Optional external ram (23LCV1024) support (1:CS/=GPIO16 2:MISO=GPIO12 3:NC 4:GND 5:MOSI=GPIO13 6:SCK=GPIO14 7:GND 8:3.3v)<br/>
If your chip has a /Vhold in place of /VBAT, the pin 7 must be wired to VCC (pin8)<br/>
Attention:<br>
	The optional led is now on GPIO2. The blue led on the ESP8266 is blinking at the same rate.<br/>
	GPIO16 is now the Chip select for the external ram if any.<br/>
	The external ram is detected at boot time if present.<br/>

## Used hardware
WiFi : ESP8266 (ESP-12 with 32Mbits flash)<br />
Additional MCU (as a bridge UART<=>UI): AVR<br />
Audio decoder: VS1053<br />


