# Build-your-own-P1-meter-reader
Workshop documentation on building your own ESP32 based P1 smart meter reader

## Connect hardware on breadboard

<img src="https://github.com/bokse001/Build-your-own-P1-meter-reader/blob/main/images/lilygo_p1_meter_reader.png?raw=true" alt="Connecting the hardware">

- 5V Lilygo to pin 2 jumper/P1 (yellow/RTS)
- GND Lilygo to pin 3 jumper/P1 (green/GND)
- Pin 25 Lilygo to pin 5 jumper/P1 (black/TXD)
- resistor 330Ohm between 3.3V Lilygo and pin 5 jumper/P1 (black/TXD)
- (Optional) Capacitor between pin 3 and pin 5 jumper

<img src="https://github.com/bokse001/Build-your-own-P1-meter-reader/blob/main/images/IDE.png?raw=true" alt="Arduino IDE">
 
## Prepare your laptop for ESP development
1. (Chess laptops) Request for administrator acces on your laptop
1. Install the Arduino.cc IDE software and launch the IDE and allow firewall access
1. File > Preferences, check the “Display line numbers option“
1. Add the URL https://dl.espressif.com/dl/package_esp32_index.json to the “Addition Boards Manager URLs” field and press the “Ok” button
<img src="https://github.com/bokse001/Build-your-own-P1-meter-reader/blob/main/images/settings.png?raw=true" alt="Settings">
1. Tools > Boards > Boards Manager, install the "esp8266" board package
<img src="https://github.com/bokse001/Build-your-own-P1-meter-reader/blob/main/images/boards.png?raw=true" alt="Boards manager">
1. Sketch > Include Library > Manage Libraries, install the "ArduinoOTA" and the "PubSubClient" libraries
<img src="https://github.com/bokse001/Build-your-own-P1-meter-reader/blob/main/images/libraries.png?raw=true" alt="Libraries">
1. Close and re-open Arduino IDE
1. Select the proper board from Tools->Board->Board ”ESP32 Dev Module”
<img src="https://github.com/bokse001/Build-your-own-P1-meter-reader/blob/main/images/select-board.png?raw=true" alt="select board">

When Connectivity to the board does not work:
- Install the CP210x USB to UART driver and make sure you reboot your machine afterward (I suffered strange behaviors using the driver without rebooting) https://www.silabs.com/products/development-tools/software/usb-to-uart-bridge-vcp-drivers
- After rebooting open the Arduino IDE and select the proper board from Tools->Board->Board ”ESP32 Dev Module”
<img src="https://github.com/bokse001/Build-your-own-P1-meter-reader/blob/main/images/examples.png?raw=true" alt="Examples">


## Test your laptop and nodeMCU setup
- Load the example sketch “TFT_Clock” into the Arduino IDE from File->Examples->TFT_eSPI->160x128->
<img src="https://github.com/bokse001/Build-your-own-P1-meter-reader/blob/main/images/blink.png?raw=true" alt="Blink">
- Try compiling it by pressing the Verify button: 
<img src="https://github.com/bokse001/Build-your-own-P1-meter-reader/blob/main/images/verify.png?raw=true" alt="Verify">
- When ok, connect the Liligo to your laptop:
	- 	Connect the Lilygo with the USB cable
	- 	Via Tools -> Port, check if the correct COMxx port is selected
	- 	Upload the sketch by pressing the Upload button:
	<img src="https://github.com/bokse001/Build-your-own-P1-meter-reader/blob/main/images/upload.png?raw=true" alt="Upload">
	- 	Wait till the sketch is compiled and uploaded
- A clock should now be visible on the display

## Test to see if the Lilygo can Display a picture
- Load the example sketch “????” into the Arduino IDE from File->open...
????-Change .....????
- Try compiling it by pressing the Verify button 
- When ok:
	- 	Connect the Lilygo with the USB cable
	- 	Via Tools -> Port, check if the correct COMxx port is selected
	- 	Upload the sketch by pressing the Upload button 
	- 	Wait till the sketch is compiled and uploaded
	- 	Open the monitor
- The picture should now be visible on the display

## Test to see if the Lilygo can read values from the P1 port
- Load the example sketch “ESP_P1meter” into the Arduino IDE from File->...
- Try compiling it by pressing the Verify button
- When ok:
	- 	Connect the nodeMCU with the USB cable
	- 	Via Tools -> Port, check if the correct COMxx port is selected
	- 	Upload the sketch by pressing the Upload button: 
	- 	Wait till the sketch is compiled and uploaded
	- 	Open the monitor Tools->Serial Monitor
- Connect the RJ12??? to the P1 port simulator
- Values about energy usage should come in

## Advanced Extra: combine the display and p1 meter sketch to display the P1 values on the Lilygo display
- Open both the sketches “????” and “ESP_P1meter” and find a way to combine the necessary code from the examples.
- Do not forget to save it under a new name like “my_P1_meter”

## Advanced Extra: combine the p1 meter sketch and SimpleWifiServer example sketch to display the P1 values in a webserver
- Open both the sketches “????” and “ESP_P1meter” and find a way to combine the necessary code from the examples.
- Do not forget to save it under a new name like “my_P1_webserver”

Now also think about pushing the data to a cloud or home automation system like Azure, home assistant or Domoticz
