# ESPurna change log

The format is based on [Keep a Changelog](http://keepachangelog.com/)
and this project adheres to [Semantic Versioning](http://semver.org/).

## [1.12.1] 2018-01-14
### Added
- Option to perform a WiFi network scan from web UI
- Added hostname to web UI side menu (#404)
- Option to flash multiple devices with ESPurna OTA Manager

### Fixed
- Fix web UI layout so signature does not overlay buttons (#396)
- Option to disable network scan and allow connecting to hidden SSID (#392, #399)
- Fix crash caused by a delay in UDP debugging code (#397)
- Fix memory leak in influxDB module (#410)
- Fix typos in web UI (#394, #421)

### Changed
- Updated to fauxmoESP 2.4.2
- Changed default I2C GPIO for Wemos D1 (#420)
- Some terminal commands have changed. See docs or type "help".

## [1.12.0] 2018-01-11
### Added
- Scheduler (contributed by Stefano Cotterli, thank you!, #131)
- Added "wifi.scan" command to terminal
- Added ESPurna Switch board support
- Added support for python3 in memanalyzer and ota scripts (thanks to Ryan Jarvis)
- Added BSSID, RSSI, channels and distance to web UI status tab
- Added mDNS name resolving to MQTT, InfluxDB and NoFUSS modules (#129, disabled by default)

### Fixed
- Update FauxmoESP library to 2.4.1, solves dependency issue (#388)
- Fixed hardware definition in Sonoff Basic and Dual R2 causing wrong relay state on boot (#365)

### Changed
- Removed auto-recursion check in Domoticz module (#379)
- Rename terminal commands: reset.wifi to wifi.reset, reset.mqtt to mqtt.reset.
- Update JustWifi library to 1.1.6 (support for multiple SSIDs with the same name)
- Changed the way Home Assistant module handles disabling auto-discovery (#383)

## [1.11.4] 2018-01-09
### Fixed
- Fix bug in RF Bridge when RF code contains the stop byte. Check overflow (#357)
- Fixed typos in code and wiki (Thanks to Ryan Jarvis)
- Fix bug in magnitude topic and units (#355)

### Added
- Small core build to allow two-step flashing method for big binaries
- Thingspeak support (#371, disabled by default)
- Color synchronization between lights using MQTT (#362)
- Support for Arilux AL-LC02 (#347)
- Support for Tarpuna Shield for Wemos D1
- Build option to disable password checking (#373)
- Option to report sensor address via MQTT (#377, I2C address, GPIO, Dallas address,...)
- Added binary size to memanalyzer script
- Option to specify custom client ID for MQTT connection (#368)
- Cross-platform ESPurna OTA Manager implemented in python (untested)
- Terminal command to get or set digital GPIO

### Changed
- Using 2.3.0 for prebuilt binaries
- Fix delay in DHT sensor
- Allow MQTT keep alive value of up to 3600s
- Changed Sonoff 4CH Pro definitions to support built-in interlock mode (#333)

## [1.11.3] 2018-01-02
### Fixed
- Fix uninitialized PWM channels bug (#356)

### Added
- Added memory analyzer

## [1.11.2] 2017-12-30
### Fixed
- Fix my92xx and pwm references for Arduino IDE (#346)
- Fix SHT3X I2C sensor magnitude count (#337)
- Fix timing for DHT11 sensors (#294)
- Fix overflow in relayParsePayload with long MQTT messages (#344)
- Fix loading of Dallas and DHT sensors for Sonoff TH images (#352)
- Subscribe to Domoticz MQTT topics only if Domotic< is enabled

### Added
- Added option to change MQTT retain flag, QoS and keepalive time from webUI (#321)
- Added LED modes "always off" and "always on" (#348)
- Defined new ESPurna switch (no HLW8012 support & touch button ready)

### Changed
- Stop requiring definition of boards in migrate module

## [1.11.1] 2017-12-29
### Fixed
- Fixed relay status on reboot

### Added
- Added support for Arilux AL-LC01 and AL-LC11
- Added support for BH1750 luminosity sensor
- Added automatic memory size identification in ota_flash script

## [1.11.0] 2017-12-28
### Fixed
- Fixed Arduino IDE compilation issues (#330)
- Fixed issues with IE
- Fixed websocket auth issue with Safari (temporary)
- Fixed MQTT group sync when different switches share same group
- Fixed casting issue in buttonStore (#327)
- Fixed crash in InfluxDB initial heartbeat (#318)
- Fixed LED logic for ESPurna H08 board

### Added
- New sensors module (major change)
  + Existing sensor have been migrated: EMON*, ECH1560, V9261F, HLW8012, DHT, DALLAS, ANALOG, DIGITAL and EVENTS
  + New sensor have bee added: BMP280/BME280, EMON over ADS1115, MHZ19, PMSX003 (thanks to Òscar Rovira), SHT3X over I2C and SI7021
- Option to change boot and pulse modes per relay from the web UI
- Option to select sensor read interval and report interval from web UI
- Itead RF Bridge
  + Match MQTT RFOUT codes to relays
  + Force RFBridge to send messages even if switch is already in requested state (#324)
  + Implemented RFbridge message queue asynchronously
- Added option to load config via HTTP POST & reset (#335)
- Added option to define behaviour of the first LED between WIFI, MQTT, FIND-ME (#317)
- Added HTML linter to gulp builder
- Added Help command on terminal (#338)
- Added preliminary support for SSDP (untested, disabled by default) (#282)
- Reporting NTP datetime on MQTT heartbeat (thanks to Eldon R. Brown)
- Added version tracking and migration code
- I2C and GPIO locking features
- Changed default button action for touch button devices (TOUCH and T1) (#327)
- Generic 8 channel board (#336)

### Changed
- Added more sensor data filters (Max, MobileAverage)
- Changed max pulse time to 1h (#316)
- Renamed "reset" to "reboot" for clarity (#315)
- UI refactor
- Change apiRegister signature

## [1.10.1] 2017-12-05
### Fixed
- Fix Sonoff RFBridge learn message from web UI (#287)
- Fix unstability in "one and just one" sync mode (#290)
- Fix unnecessary inclusion of my92xx library (#293)
- Limit the MQTT queue to 10 messages when "Use JSON payload" enabled (#296)
- Fix Sonoff RFBridge OFF button toggling switch (#303)
- Allow defining only ON or OFF codes in Sonoff RFBridge (#304)
- Disabled terminal support for Sonoff Dual (#310)

### Added
- Support for SI7021-based sensor by Itead Studio compatible with Sonoff TH (#216)
- Support for Sonoff Dual R2 (#286)
- MQTT group topics (sync two or more switches from different devices, #300)
- Color transitions (enabled by default, can be disabled from web UI)
- Option to disable MQTT support at build time

### Changed
- Decreased PWM frequency for dimmer lights
- Changed password policy (#297)

## [1.10.0] 2017-11-26
### Fixed
- Temperatures with 1 decimal resolution
- Issues with Sonoff B1 due to bad driver management (using my92xx library now)
- Avoid recursive messages on Domoticz (#272)
- Fixed Sonoff T1 configuration
- Simplify and fix web auth (#284)
- Fix Embedis custom parser

### Added
- Added option to define a temperature correction factor (thanks to Pawel Raszewski)
- Option to disable system check on build time
- Power saving features (loopDelay and wifi sleep)
- Added Sonoff TH build environment
- Send Home Assistant auto discover messages on connect (#279)
- Implemented Home Assistant availability topic (#280)
- Update time, uptime and heap on webUI every heartbeat
- Support for LLMNR and NetBIOS (#282)
- Added I2C clean bus code
- Added realm to auth challenge

### Changed
- Changed default hostname to "ESPURNA_XXXXXX"
- Binaries built against stable core (~40Kb less, #274)
- Enabled TERMINAL_SUPPORT for Sonoff Dual (only available via TELNET)
- Dinamically resize debug strings (now messages are not cropped)
- MQTT: unsubscribe to '#' before subscribing
- Updated ESPAsyncWebServer and ESPAsyncTCP libraries
- Removed InfluxDB support by default
- Using stock slider in webUI to reduce size
- Unify DHT and DS18B20 code, show NOT CONNECTED on webUI

## [1.9.9] 2017-11-09
### Fixed
- Fixed bug in MY9291-based light bulbs at full brightness

### Added
- RFBridge: toggle when RF codes for ON and OFF are the same (#270)
- Support for HSV color schema (MQTT, API and webUI via a selector)

### Changed
- "COLOR" entry point deprecated, use "RGB" instead (MQTT and API, ex. topic "light/rgb/set" instead of "light/color/set")

## [1.9.8] 2017-11-08
### Fixed
- Removed dimmer lights flicker when saving to EEPROM (#191)
- Fixed low brightness in dimmer lights (#157)
- Fixed blank fields in energy (#258, #259)
- Fixed support for Arilux AL-LC06
- Updated fauxmoESP library with support for GetBinaryState actions

### Added
- Support for IR remotes
- Option to select power read and report interval from webUI
- Option to report real-time values in API, configurable via webUI
- Support for ESPurna-H Board v0.8
- Support for Arilux E27 light bulb (untested)
- Support for YJZK 2-gang switch

### Changed
- PWM using ESP8266_new_pwm by Stephan Bruens (https://github.com/StefanBruens/ESP8266_new_pwm)
- Using own DHT implementation (removed dependency on Adafruit libraries)
- Disabled serial debug for Sonoff RFBridge

## [1.9.7] 2017-10-25
### Fixed
- Fix Alexa interface switching on all lights (#256)

## [1.9.6] 2017-10-23
### Fixed
- Fix power report in Domoticz (#236)
- Fix Sonoff POW in AP mode (#241)
- Fix Home Automation auto-discovery (support for single relay switches and RGB lights, #235)
- Check WS authentication only on start event

### Added
- Support for 2.4.0 RC2 Arduino Core that fixes KRACK vulnerablity (pre-built images are compiled against this, #242)
- Support for ManCaveMade ESPLive board (thanks to Michael A. Cox)
- Support for InterMIT Tech QuinLED 2.6 (thanks to Colin Shorts)
- Support for Magic Home LED Controller 2.0 (thanks to users @gimi87 and @soif, #231)
- Support for Arilux AL-LC06 (thanks to Martijn Kruissen)
- Support for Xenon SM-PW702U Wifi boards (thanks to Joshua Harden, #212)
- Support for Authometion LYT8266 (testing, thanks to Joe Blellik, #213)
- Support for an external button for D1 Mini boards (thanks to user @PieBru, #239)
- Option to query relay status via MQTT or WS (thanks to Wesley Tuzza)
- Automatically install dependencies for web interface builder (thanks to Hermann Kraus)
- Support for HSV and IR for Magic Home LED Controller (optional, disabled by default, thanks to Wesley Tuzza)
- Added option to report DS18B20 temperatures based on changes (thanks to Michael A. Cox)
- Safer buffer handling for websocket data (thanks to Hermann Kraus & Björn Bergman)
- Updates HL8012 library with energy counting support (thanks to Hermann Kraus)
- Added option to disable light color persistence to avoid flickering (#191)
- Option to enable TELNET in STA mode from web UI (#203)

### Changed
- Changed default MQTT base topic to "{identifier}" (no leading slashes, #208)
- Prevent reconnecting when in AP mode if a web session or a telnet session is active (#244)
- Web UI checks for pending changes before reset/reconnect options (#226)
- Increase WIFI connect timeout and reconnect interval

## [1.9.5] 2017-09-28
### Fixed
- Revert to JustWifi 1.1.4 (#228)

## [1.9.4] 2017-09-22
### Added
- Added ESPurna specific mDNS text registers (app_name, app_version, device_name)
- Crash dump info is stored in EEPROM and retrieved via terminal ("crash" command)
- Support for Huacanxing H802
- Support for powermeters based on V9261F IC
- Support for powermeters based on ECH1560 IC (beta, untested)

### Changed
- Changed behaviour on MQTT connection failure (#215)
- Removed boot delay
- Refactor power modules
- Updated JustWifi library

### Fixed
- Set all esp8285 devices to use esp01_1m (#210, #225)
- Removed wifi gain option since it prevents some devices to connect (#204)

## [1.9.3] 2017-09-04
### Added
- New "erase.config" option in terminal to delete SDK settings
- Added error code to error message when updating from web UI
- Fixed Web UI to be behind a proxy (http://tinkerman.cat/secure-remote-access-to-your-iot-devices/)
- Support "ON", "OFF" and "TOGGLE" (also lowercase) as payload in relay MQTT, API and WS (http://tinkerman.cat/using-google-assistant-control-your-esp8266-devices/)

### Changed
- Updated fauxmoESP library to 2.2.0

### Fixed
- Fix HLW8012 calibration (#194)
- Fix telnet dropping connection
- Fix WiFiSecureClient connection with PubSubClient (#64)

## [1.9.2] 2017-08-31
### Added
- System stability check (turns off everything except WIFI AP, OTA and telnet if there is a boot crash loop) (#196)
- Telnet support (enabled by default only on AP interface)
- Option to set WiFi gain from web UI
- Option to disable MQTT from web UI
- MQTT autodiscover, with the option to autoconnect if no broker defined
- Home Assistant MQTT autodiscover feature
- List enabled modules in INIT debug info
- Counter module (counts and reports transitions in a digital pin)

### Changed
- Updated NoFUSS support
- Web UI documentation changes
- Changes in terminal commands ("reconnect" is now "reset.wifi", also new commands added)

### Fixed
- Crash in settings saving (#190) and fixed UDP debug conditional build clauses

## [1.9.1] 2017-08-27
### Added
- Support to build without NTP support
- Added current time, uptime, free heap, firmware size and free space to web interface

### Changed
- Changed settings keys for Itead Sonoff RF Bridge
- Disable Domoticz by default

### Fixed
- Fixed build flags for DHT and DS18B20 in platformio.ini file
- Fixed Itead Sonoff B1 by updating the my9291 library
- Fixed light status on boot (#157)
- Fixed CSS bug cause by a bad merge

## [1.9.0] 2017-08-25
### Added
- Support for IteadStudio BN-SZ01 Ceiling Light (#132)
- Support for IteadStudio Sonoff RF Bridge (#173)
- Support for IteadStudio Sonoff 4CH Pro (#174)
- Support for IteadStudio Sonoff B1
- Support for IteadStudio Sonoff LED
- Support for IteadStudio Sonoff T1 wall switches (1, 2 and 4 channels)
- Support for WiOn 50055 WiFi Wall Outlet & Tap
- Support for EXS WiFi Relay v3.1 (and other future latching relay boards) (#152)
- TLS/SSL support for MQTT (caution: eats a lot of memory, do not use with web interface) (#64)
- Add support for delayed ON/OFF switches (#123, #161, #188)
- Added ON and OFF actions for button events (previously only TOGGLE available) (#182)
- Sliders in web interface to control dimmer channels independently (also for brightness)
- Debug info about MQTT disconnect reason

### Changed
- MQTT setters ending with "/set" by default
- Using DOUT flash mode on all devices (#167)
- Longer timeout for WiFi connection (better chances for Sonoff Basic to connect)
- Changed MQTT topics for light devices (COLOR, BRIGHTNESS, MIRED, KELVIN, CHANNEL) (#144)
- Changed the way light devices are defined (see LIGHT_PROVIDER_DIMMER)
- Allow to disable color picker in web interface
- API returns processed values for HLW8012 sensor (not raw values anymore) (#176)
- Major refactoring of settings

### Fixed
- Discard MQTT messages with empty payload (#185)
- Wifi connection issue (https://github.com/esp8266/Arduino/issues/2186)
- Alexa connection issue

## [1.8.3] 2017-07-23
### Added
- Issue #85 and #90. Option to report MQTT messages with JSON payloads
- Issue #170. Updated DebouceEvent library to allow disabling double click and get faster click responses
- Using memory layout with no SPIFFS for 1Mb devices

### Changed
- Rename settings s/POW/HLW8012/
- Return times in ISO8601 format

### Fixed
- Issue #168. Added H801 to arduino.h file
- Issue #171. Fix corrupted will message

## [1.8.2] 2017-07-16
### Added
- InfluxDB support via HTTP API
- Added custom reset reason to debug log
- Enable WIFI debug on hardware reset (button long click)

### Changed
- Issue #159. Allow decimals in relay pulse interval
- Updated HLW8012 library

### Fixed
- Issue #148. Fix bug in conditional compilation check
- Issue #149. Using different pulse counters for each relay (thanks to Lauris Ieviņš)
- Issue #141. Limit relay pulse interval to 60s
- Fixed units for apparent & reactive power (thanks to Lauris Ieviņš)
- Fixed mDNS setup when using custom HTTP port for web interface

## [1.8.1] 2017-05-22
### Fixed
- Issue #140. Fix no relay control bug in Sonoff Dual

## [1.8.0] 2017-05-21
### Added
- Added gamma correction to RGB strips. Thanks to Chris Ward.
- Added support for Huacanxing H801 WiFi LED Controller. Thanks to Minh Phuong Ly.
- Issue #138. Added NTP configuration from web interface
- Issue #128. Report color when booting and in heartbeat stream.
- Issue #126. Show NTP status in web interface.
- Added filter limits on POW readings.
- Added color temperature to RGB calculation. Thanks to Sacha Telgenhof.
- Issue #120. Added relay flood protection. Thanks to Izik Dubnov.
- Support for "#RRGGBB", "RRR,GGG,BBB" and "WWW" color formats.
- Issue #117. Added build date & time to web interface.

### Fixed
- Fix MQTT_RELAY board conifugration. Thanks to Denis French.
- Issue #125. Fix bug in relay status reading from EEPROM
- Issue #127. Fix button action in DUAL.
- Fix bug in Sonoff POW current reading. Thanks to Emmanuel Tatto.
- Minimizing my9291 flickering when booting.
- Fix conditional flags in hardware.ino to support Arduino IDE.

## [1.7.1] 2017-03-28
### Fixed
- Issue #113. Fix restoring color from EEPROM upon reboot
- Issue #113. Fix bug in API handlers

## [1.7.0] 2017-03-27
### Added
- Web interface embedded in firmware image by default
- Upload firmware image from web interface
- Added API entry point to change light color
- Added generic analog sensor. Thanks to Francesco Boscarino
- Report RSSI value in debug console and MQTT status messages
- Added support for Magic Home LED Controller
- Added support for ESPurna-H Board (based on HLW8012)
- Added forward compatible code for v2.0

### Changed
- Added ellipsis (...) in debug messages longer than 80 characters
- Changed topic constants in code
- Prevent the SDK from saving WiFi configuration to flash

### Fixed
- Issue #113. Fix light bulb state to OFF in library prevented the bulb from turning on
- Issue #58. Added code to handle spurious readings
- Fix bug in HLW8012 calibration current parameter casting to int instead of float
- Issue #115. Removed local declaration of _mqttForward variable. Thanks to Paweł Fiedor
- Fix MQTT will topic. Thanks to Asbjorn Tronhus

## [1.6.9] 2017-03-12
### Added
- Two stage read for DS18B20 devices. Thanks to Izik Dubnov.
- Option to report the relay status via MQTT periodically
- Terminal commands to change relay status an light color
- Added debug via UDP (disabled by default)
- Moved debug strings to PROGMEM. ~1.5KByes memory freed
- Avoid broadcasting websocket messages if no clients connected

### Fixed
- Fixing use after free bug that leads to corrupted auth credentials. Thanks to David Guillen

## [1.6.8] 2017-03-01
### Added
- Issue #85. Heartbeat reports now free heap, uptime and VCC every 5 minutes

### Changed
- Wait two minutes instead of one in AP mode before trying to reconnect to the router
- Issue #92. Debug log enabled by default in Arduino IDE
- Issue #91. Using AsyncMqttClient as default MQTT client again

### Fixed
- Report data from all sensors via websocket even if no MQTT connection
- Issue #92. Fix unknown reference in Arduino IDE
- Split data.h contents into 1k lines, otherwise Arduino IDE chokes on them
- Discard empty MQTT topic while subscribing

## [1.6.7] 2017-02-25
### Added
- Support for OpenLight / AI-Light by AI-Thinker based on MY9291 LED driver
- Issue #87. Factory reset when physical button pressed for >10 seconds

## [1.6.6] 2017-02-23
### Fixed
- Issue #82. Fix critical bug on Sonoff Dual

## [1.6.5] 2017-02-22
### Added
- Option to backup and restore settings from the web interface
- Footer in the web interface

### Changed
- Using PubSubClient as MQTT client by default (please read the documentation)
- Double & long clicks do nothing except for the first defined button

### Fixed
- Issue #79. Fix bug in WiFi led notification & MQTT connectivity (using PubSubClient)
- Issue #73. Fix bug when building without Domoticz support
- Fix Gulp tasks dependencies

## [1.6.4] 2017-02-20
### Added
- Option to embed the web interface in the firmware, disabled by default
- Change relay status with a GET request (browser friendly)
- Support for PROGMEM debug messages (only wifi module has been changed)
- Option to disable mDNS, enabled by default
- Show current web server port in debug log
- Issue #75. Link relays to LEDs
- Issue #76. Using http://espurna.local when in AP mode

### Changed
- Images and favicon is now embedded in the HTML
- Authentication challenge only in /auth request. All static contents are un-authenticated
- HTTP response code when out of websocket slots changed from 423 to 429

### Fixed
- Memory leak in MQTT connection method
- Wait 60 seconds before retrying to connect when in AP mode
- Issue #24 & #74. Update ESPAsyncTCP and ESPAsyncWebServer to latest GIT version that supports MSS defragmenting
- Issue #73. Fixes for windows machines

### Removed
- Captive portal removed, mDNS resolution for AP mode too

## [1.6.3] 2017-02-15
### Added
- Issue #69. Temperature unit configuration from the web interface
- Issue #55. WebServer port configurable from the web interface, defaults to 80
- Expand network configuration when adding a new network

### Changed
- Merged web contents except images in a single compressed file for reliability
- Update support for Itead Motor Clockwise/Anticlockwise board
- Scan for strongest network only if more than 1 network configured

### Fixed
- Issue #71. Added default values for netmask and DNS in web configuration
- Fixed Itead 1CH self-locking/inching board definition
- Fixed PlatformIO environments for ESP8285 boards (4CH and Touch)

## [1.6.2] 2017-02-10
### Fixed
- Check if there is an MQTT broker defined before the MQTT_MAX_TRIES check

## [1.6.1] 2017-02-10
### Added
- Added support for [Jorge Garcia's Wifi+Relay Board Kit](https://www.tindie.com/products/jorgegarciadev/wifi--relays-board-kit/)
- Reporting current and energy incrementals to a separate counters in Domoticz (thanks to Toni Arte)
- Force WiFi reconnect after MQTT_MAX_TRIES fails trying to connect to MQTT broker

## [1.6.0] 2017-02-05
### Added
- Added support for toggle switches
- Allow reset the board via an MQTT message
- Allow reset the board via an RPC (HTTP) message
- Added support for ADC121 I2C for current monitoring (Check [http://tinkerman.cat/power-monitoring-sonoff-th-adc121/](http://tinkerman.cat/power-monitoring-sonoff-th-adc121/))
- Reporting voltage to Domoticz (only HLW8012)
- Map button events to actions (toggle relay, AP mode, reset, pulse mode)

### Changed
- Reporting energy incrementals (Domoticz, MQTT)

### Removed
- Removed current monitor bypass when relay is OFF
- Removed energy API entry point

## [1.5.4] 2017-02-03
### Fixed
- Issue #50. Fix type bug in window variable when calculating energy for HLW8012 devices (Sonoff POW)

## [1.5.3] 2017-02-02
### Fixed
- Issue #50 and #54. Fixed domoticz MQTT message format

### Added
- Energy calculation and aggregation. API entry points and MQTT messages.

## [1.5.2] 2017-01-29
### Fixed
- Fix bug in emon topic payload

## [1.5.1] 2017-01-28
### Added
- OpenEnergyMonitor WiFi MQTT Relay / Thermostat support (thanks to Denis French)

### Fixed
- NTP connection refresh upon wifi connection
- Filesystem image build using local gulp installation

## [1.5.0] 2017-01-21
### Added
- Pulse mode. Allows to define a pulse time after which the relay will switch back
- API entry points for sensor data (power, current, voltage, temperature and humidity)
- Export sensor data to Domoticz (power, current, voltage, temperature and humidity)
- Configurable (in code) mapping between buttons and relays
- MQTT messages for button events
- Added support for Itead Studio 1CH inching/self locking smart switch board
- Added support for Jan Goedeke Wifi Relay boards (both NC and NO versions)
- Notify OTA updates to websocket clients, automatically reload page
- Support for pulse mode notification LED and button
- Revert relay state mode on boot (thanks to Minh Phuong Ly)

### Fixed
- MQTT will topic
- Crash with HLW812 interrupts while trying to create a WIFI connection
- Issue #20 Better inline documentation for Alexa and Domoticz default settings
- Issue #39 Fixed autoconnect issue with static IP (fixed in JustWifi library)
- Issue #41 Added password requirements to initial password change page

### Changed
- Changed LED pattern for WIFI notifications (shorter pulses)

## [1.4.4] 2017-01-13
### Added
- Adding current, voltage, apparent and reactive power reports to Sonoff POW (Web & MQTT)

### Fixed
- Issue #35 Fixed frequent MQTT connection drops after WIFI reconnect
- Defer wifi disconnection from web interface to allow request to return

### Changed
- Move all Arduino IDE configuration values to their own file
- Using latest HLW8012 library in interrupt mode

## [1.4.3] 2017-01-11
### Fixed
- Issue #6 Using forked Time library to prevent conflict with Arduino Core for ESP8266 time.h file in windows machines

## [1.4.2] 2017-01-09
### Added
- Support for inverse logic relays

### Fixed
- Issue #31. Fixed error in relay identification from MQTT messages

## [1.4.1] 2017-01-05
### Added
- Alexa support by default on all devices
- Added support for Wemos D1 Mini board with official Relay Shield

### Fixed
- Multi-packet websocket frames

## [1.4.0] 2016-12-31
### Added
- Domoticz support via MQTT (https://www.domoticz.com/wiki/MQTT)
- Support for static IP connections

### Fixed
- Issue #16. Enforce minimum password strength in web interface

### Changed
- Using default client_id provided by AsyncMqttClient
- Allow up to 5 different WIFI networks

### Removed
- File system version file

## [1.3.1] 2016-12-31
### Fixed
- data_dir fix for PlatformIO

## [1.3.0] 2016-12-30
### Changed
- Arduino IDE support (changes in the folder structure and documentation)

## [1.2.0] 2016-12-27
### Added
- Force password changing if it's the default one
- Added Last-Modified header to static contents
- Added DNS captive portal for AP mode
- Added support for Sonoff 4CH
- Added support for WorkChoice ecoPlug (ECOPLUG). Thanks to David Myers
- Added support for Sonoff SV
- Added support for Sonoff Touch
- Comment out hardware selection in hardware.h if using Arduino IDE
- Added support for MQTT get/set suffixes (/status, /set, ...)
- Added support for LED notifications via MQTT
- Added EEPROM check commands to terminal interface

### Changed
- Using unreleased AsyncMqttClient with stability improvements
- Better decoupling between MQTT and relays/websockets
- Skipping retained MQTT messages (configurable)

### Fixed
- Issue #11 Compile error when building sonoff-dual-debug
- Issue #14 MQTT Connection with Username an Password not working
- Issue #17 Moved static variable 'pending' to class variable

## [1.1.0] 2016-12-06
### Added
- Added support for DS18B20 temperature sensor. Thanks to Francesco Boscarino
- Added reset command from console
- Added support for multirelay boards like Sonoff DUAL or Electrodragon ESP Relay Board

### Changed
- Not using espressif8266_stage in default environment
- Relay MQTT topics
- API entry points

### Removed
- Old non protected API

## [1.0.3] 2016-11-29

### Added
- WeMo emulation through the fauxmoESP library (control your switch from Alexa!)
- REST API for relay management
- Better dependency definitions in platformio.ini
- Option to define inverse logic to on-board LED
- Built data folder included in repo

### Changed
- Using non-interrupt driven mode for HLW8012
- Better documentation
- Small changes to web interface
- Same admin password for web, OTA and WIFI AP mode

### Fixed
- Prevent fauxmoESP to be compiled by default

### Removed
- Removed ESPurna board to its own repo

## [1.0.1] 2016-11-13

### Added
- Basic authentication and CSRF to websocket requests

## [1.0.0] 2016-11-13

### Added
- Using ESPAsyncWebServer (for web & websockets) and AsyncMqttClient

## [0.9.9] 2016-11-12

### Added
- Preliminary support for Sonoff POW
- Replace AJAX requests with websockets
- Using sprites for images
- Hostname can be changed
- Added initial relay state mode
- Reconnect and reset buttons on web interface

### Changed
- Changed long click to reset and double click to AP mode
- Using officially supported platformio.ini file by default

### Fixed
- Removed unnecessary memory inefficient code
- Temprary fix for Adafruit DHT library (see https://github.com/adafruit/DHT-sensor-library/issues/62)

## [0.9.8] 2016-10-06

### Added
- Using PureCMS for the web interface
- Using gulp to build the filesystem files
- Using Embedis for configuration

### Changed
- Updated JustWifi library
- Web interface changes
- Using custom platformio.ini file
- Loads of changes in modules
- Added DEBUG_MSG

### Fixed
- Clean gulp builder script

## [0.9.7] 2016-08-28

### Changed
- Moving wifi management to library (JustWifi)
- Split code into modules

## [0.9.6] 2016-08-12

### Added
- Added heartbeat, version and fsversion MQTT messages

### Changed
- GZip 3rd party contents

## [0.9.5] 2016-07-31
- Initial stable version
