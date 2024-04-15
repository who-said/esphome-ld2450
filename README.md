About: Building an affordable presence sensor that can track 3 targets(human) including their 2D coordinates and their speed in a range of 6m*120deg and integrating into Home Assistant so it be managed centrally, used for adding automations and used to visually track people

Components needed: 
- HLK-LD2450 mmWave sensor
- ESP8266 Wemos D1 mini microcontroller
- USB mini cable of desirable length for flashing chip and powering device
- Home Assistant

Steps
1. On HA go to Settings>Add-ons>ADD-ON STORE, add the ESPHome add-on, and then start it (preferably with all options switched on)
2. Connect your microcontroller to your device using USB to mini-USB, and then go to https://esphome.github.io/esp-web-tools/ and press Connect (make sure you have the CH340 drivers installed on your device so the D1 mini is recognized by and can connect to your device through the COM ports, to download you can go here: https://www.wch-ic.com/downloads/CH341SER_ZIP.html and press download). Select your COM port and press connect. Then install the device onto your ESP and after it is flashed configure the wifi
3. Go to the ESPHome dashboard on HA and adopt the new device. Name it ld2450, and then copy the API key somewhere safe. Press skip install and then press the 3 dots on the ESPHome device and rename the hostname to ld2450. After the process finishes press close and then go to Edit and paste the LD2450 YAML example on there. Make sure to replace "API key" with the API key that you copied earlier and make sure to perform what the note at the beginning of the YAML file suggests. After this press install wirelessly, and wait for the process to start logging data
4. Connect your LD2450 sensor to the D1 mini by connecting:
    5 v -- 5 v
    GND -- GND
    TX  -- RX
    RX  -- TX
5. On HA, go to Settings>Devices and Services>Add integrations and add the ESPHome integration (this might not be needed if the device gets discovered already, in that case just adopt the integration). From the ESPHome integration, we can observe the sensor data including targets' coordinates, speed, and other characteristics. We can also customize presence regions according to our convenience, toggle the device Bluetooth, reboot the microcontroller, reset the chip, etc.
6. Now go to https://hacs.xyz/ and follow the instructions to download the HACS community store, after which we can download the Lovelace Plotly graph card. After that is installed from the HACS community store go to your dashboard and edit it, search for the plotly graph card, go to edit code, and paste the code from PlotlyLD2450F, repeat this with PlotlyLD2450C and press save. You should now be able to see a visualization of the sensor data.

  
