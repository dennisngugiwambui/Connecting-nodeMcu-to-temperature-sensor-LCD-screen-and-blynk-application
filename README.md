# this is my connection

![Nodemcu-Dht-11_bb1](https://github.com/dennisngugiwambui/Connecting-nodeMcu-to-temperature-sensor-LCD-screen-and-blynk-application/assets/112067611/f6758142-aa0c-488a-b4a5-2382f9509f4b)

# The code for LCD screen connection

The Sketch:

#include <LiquidCrystal_I2C.h>

#include <Wire.h>

LiquidCrystal_I2C lcd(0x27, 16, 2);

void setup() {

Serial.begin(115200);

//Use predefined PINS consts

Wire.begin(D2, D1);

lcd.begin();

lcd.home();

lcd.print("Hello, NodeMCU");

}

void loop() { // do nothing here }

![image](https://github.com/dennisngugiwambui/Connecting-nodeMcu-to-temperature-sensor-LCD-screen-and-blynk-application/assets/112067611/7068e72b-c78d-476c-b1f9-6b6d5c70d882)

LCD library


2. LiquidCrystal_I2C library - ```https://github.com/fdebrabander/Arduino-LiquidCrystal-I2C-library```




