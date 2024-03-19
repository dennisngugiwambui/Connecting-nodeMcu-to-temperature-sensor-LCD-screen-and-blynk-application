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


# THE CODE


```
//Viral science www.youtube.com/c/viralscience
//Temperature sensor
/**************************************************************
 * Blynk is a platform with iOS and Android apps to control
 * Arduino, Raspberry Pi and the likes over the Internet.
 * You can easily build graphic interfaces for all your
 * projects by simply dragging and dropping widgets.
 *
 *   Downloads, docs, tutorials: http://www.blynk.cc
 *   Blynk community:            http://community.blynk.cc
 *   Social networks:            http://www.fb.com/blynkapp
 *                               http://twitter.com/blynk_app
 *
 * Blynk library is licensed under MIT license
 * This example code is in public domain.
 *
 **************************************************************
 * This example shows how value can be pushed from Arduino to
 * the Blynk App.
 *
 * WARNING :
 * For this example you'll need SimpleTimer library:
 *   https://github.com/jfturcot/SimpleTimer
 * and Adafruit DHT sensor library:
 *   https://github.com/adafruit/DHT-sensor-library
 *
 * App project setup:
 *   Value Display widget attached to V5
 *   Value Display widget attached to V6
 *
 **************************************************************/

#define BLYNK_PRINT Serial    // Comment this out to disable prints and save space


#define BLYNK_TEMPLATE_ID "TMPL2xsAOcjWb"
#define BLYNK_TEMPLATE_NAME "smart health"
#define BLYNK_AUTH_TOKEN "m43LgpgorJJyiy6mg05WPWo9dnv04e--"



#include <SPI.h>
#include <ESP8266WiFi.h>
#include <BlynkSimpleEsp8266.h>
#include "Simpletimer.h"
#include <DHT.h>


#define DHTPIN 2          // Digital pin 4

// GPIO pins for LED bulbs
const int LED_PIN_1 = 5;  // D1
const int LED_PIN_2 = 4;  // D2
const int LED_PIN_3 = 0;  // D3


// Uncomment whatever type you're using!
#define DHTTYPE DHT11     // DHT 11
//#define DHTTYPE DHT22   // DHT 22, AM2302, AM2321
//#define DHTTYPE DHT21   // DHT 21, AM2301


// Instances of WidgetLED for LED bulbs
WidgetLED led1(V7);
WidgetLED led2(V8);
WidgetLED led3(V9);



// You should get Auth Token in the Blynk App.
// Go to the Project Settings (nut icon).
char auth[] = "m43LgpgorJJyiy6mg05WPWo9dnv04e--"; //Enter the Auth code which was send by Blink


// Your WiFi credentials.
// Set password to "" for open networks.
char ssid[] = "Delly IT";  //Enter your WIFI Name
char pass[] = "0758024400";  //Enter your WIFI Password


DHT dht(DHTPIN, DHTTYPE);
BlynkTimer timer;

// This function sends Arduino's up time every second to Virtual Pin (5).
// In the app, Widget's reading frequency should be set to PUSH. This means
// that you define how often to send data to Blynk App.
void sendSensor()
{
  float h = dht.readHumidity();
  float t = dht.readTemperature(); // or dht.readTemperature(true) for Fahrenheit

  if (isnan(h) || isnan(t)) {
    Serial.println("Failed to read from DHT sensor!");
    return;
  }
  // You can send any value at any time.
  // Please don't send more that 10 values per second.
  Blynk.virtualWrite(V5, h);  //V5 is for Humidity
  Blynk.virtualWrite(V6, t);  //V6 is for Temperature
}
BLYNK_WRITE(V7) {
  int pinValue = param.asInt();
  digitalWrite(LED_PIN_1, pinValue);
}

BLYNK_WRITE(V8) {
  int pinValue = param.asInt();
  digitalWrite(LED_PIN_2, pinValue);
}

BLYNK_WRITE(V9) {
  int pinValue = param.asInt();
  digitalWrite(LED_PIN_3, pinValue);
}



void setup()
{
  Serial.begin(9600); // See the connection status in Serial Monitor
  Blynk.begin(auth, ssid, pass);

  dht.begin();

  // Setup LED pins
  pinMode(LED_PIN_1, OUTPUT);
  pinMode(LED_PIN_2, OUTPUT);
  pinMode(LED_PIN_3, OUTPUT);

  // Setup a function to be called every second
  // timer.register_callback(sendSensor);
  timer.setInterval(1000L,sendSensor);
}

void loop()
{
  Blynk.run(); // Initiates Blynk
  timer.run(); // Initiates SimpleTimer
}

```



