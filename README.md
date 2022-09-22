# Build-your-own-P1-meter-reader
Workshop documentation on building your own ESP32 based P1 smart meter reader

## Connect hardware on breadboard

<img src="https://github.com/bokse001/Build-your-own-P1-meter-reader/blob/main/images/lilygo_p1_meter_reader.png?raw=true" alt="Connecting the hardware">
Be carefull how you connect the jumper, see colors below...

- 5V Lilygo to pin 2 jumper/P1 (yellow/RTS)
- GND Lilygo to pin 3 jumper/P1 (green/GND)
- Pin 25 Lilygo to pin 5 jumper/P1 (black/TXD)
- resistor 330Ohm between 3.3V Lilygo and pin 5 jumper/P1 (black/TXD)
- (Optional) Capacitor between pin 3 and pin 5 jumper

<img src="https://github.com/bokse001/Build-your-own-P1-meter-reader/blob/main/images/IDE.png?raw=true" alt="Arduino IDE">
 
## Prepare your laptop for ESP32 development
1. (Chess laptops) Request for administrator access on your laptop
<img src="https://github.com/bokse001/Build-your-own-P1-meter-reader/blob/main/images/RequestAdminAccess.JPG?raw=true" alt="Settings">
2. Install the Arduino.cc IDE software and launch the IDE and allow firewall access<br/>
3. File > Preferences, check the “Display line numbers option“    <br/>
4. Add the URL https://dl.espressif.com/dl/package_esp32_index.json to the “Addition Boards Manager URLs” field and press the “Ok” button 
<img src="https://github.com/bokse001/Build-your-own-P1-meter-reader/blob/main/images/settings.png?raw=true" alt="Settings">   
5. Tools > Boards > Boards Manager, install the "esp32" board package
<img src="https://github.com/bokse001/Build-your-own-P1-meter-reader/blob/main/images/boards.png?raw=true" alt="Boards manager">
6. Sketch > Include Library > Manage Libraries, install the "ArduinoOTA", "button2" and the "PubSubClient" libraries
<img src="https://github.com/bokse001/Build-your-own-P1-meter-reader/blob/main/images/libraries.png?raw=true" alt="Libraries">
7. Download the TFT_eSPI.zip from the sketch folder  (or https://github.com/Xinyuan-LilyGO/TTGO-T-Display) and unzip in your libraries folder
8. Close and re-open Arduino IDE
9. Select the proper board from Tools->Board->Board ”ESP32 Dev Module”
<img src="https://github.com/bokse001/Build-your-own-P1-meter-reader/blob/main/images/select-board.png?raw=true" alt="select board">

When Connectivity to the board does not work:
- Install the CP210x USB to UART driver and make sure you reboot your machine afterward (I suffered strange behaviors using the driver without rebooting) https://www.silabs.com/products/development-tools/software/usb-to-uart-bridge-vcp-drivers
- After rebooting open the Arduino IDE and select the proper board from Tools->Board->Board ”ESP32 Dev Module”
<img src="https://github.com/bokse001/Build-your-own-P1-meter-reader/blob/main/images/examples.png?raw=true" alt="Examples">


## Test your laptop and ESP32 setup
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
- Download the example sketch TTGO-T-Display.zip from the sketches folder and unzip into your Documents/Arduino folder.
- Load the example sketch TTGO-T-Display.ino into the Arduino IDE from File->open or by double clicking it in the folder just created.
- Try compiling it by pressing the Verify button 
- When ok:
	- 	Connect the Lilygo with the USB cable
	- 	Via Tools -> Port, check if the correct COMxx port is selected
	- 	Upload the sketch by pressing the Upload button 
	- 	Wait till the sketch is compiled and uploaded
	- 	Open the monitor
- The picture of innovatos should now be visible on the display

## Test to see if the Lilygo can read values from the P1 port
- Download the example sketch esp_p1meter_h.zip from the sketches folder and unzip into your Documents/Arduino folder.
- Load the example sketch esp32_p1meter_h.ino into the Arduino IDE from File->open or by double clicking it in the folder just created.
- Change the wifi details in settings.h with the details provided.
- Change the port from 38 to 25 in settings.h
- Try compiling it by pressing the Verify button
- When ok:
	- 	Connect the Lilygo with the USB cable
	- 	Via Tools -> Port, check if the correct COMxx port is selected
	- 	Upload the sketch by pressing the Upload button: 
	- 	Wait till the sketch is compiled and uploaded
	- 	Open the monitor Tools->Serial Monitor
- Connect your Lilygo to the P1 port simulator, ask the for help from our ioteers
- Values about energy usage should come in

## Advanced Extra: combine the print_test and p1 meter sketch to display the P1 values on the Lilygo display
- Open both the sketches “TFT_Print_Test” and “ESP_P1meter_h” and find a way to combine the necessary code from the examples.
- Do not forget to save it under a new name like “my_P1_display”

## Advanced Extra: combine the p1 meter sketch and SimpleWifiServer example sketch to display the P1 values in a webserver
- Open both the sketches “SimpleWifiServer” and “ESP_P1meter” and find a way to combine the necessary code from the examples.
- Do not forget to save it under a new name like “my_P1_webserver”

## Advanced Extra: Use the p1_meter_reader_h sketch and send values to a MQTT server
- Open “ESP_P1meter_h” and find a way to switch on the MQTT connectivity.
- Change the MQTT server detais in the seetings.h
- Do not forget to save it under a new name like “my_P1_mqtt”

Now also think about pushing the data to a cloud or home automation system like Azure, home assistant or Domoticz

Note:
- When connecting to a real live P1 meter values need to be inverted. Find the line in the sketch that contains Serial2.begin and add ",true" to invert the signal
- You can use home assistant to receive the values and create an energy dashboad. Details are in the original github: https://github.com/bartwo/esp32_p1meter. To install home assistant best use the docker version.
