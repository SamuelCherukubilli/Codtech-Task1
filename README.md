# Codtech-Task1
To design a system to control an LED light using a microcontroller (such as an Arduino) and a mobile app, we need to break the project down into hardware and software components. Here's a step-by-step guide to designing and building the system:

Hardware Requirements:
Arduino Board:

An Arduino Uno or similar microcontroller.
LED:

A standard LED (preferably with a current-limiting resistor).
Bluetooth Module:

HC-05 or HC-06 Bluetooth module to establish communication between the mobile app and the Arduino.
Power Supply:

A power source for the Arduino and LED (e.g., USB, battery, or DC adapter).
Resistor:

A current-limiting resistor (typically 220Ω to 330Ω) for the LED.
Software Requirements:
Arduino IDE:

For programming the Arduino board.
Mobile App:

A mobile app, which could be developed using tools like MIT App Inventor, Flutter, or React Native to interface with the Bluetooth module and control the LED.
Bluetooth Library:

SoftwareSerial library for Bluetooth communication (or use the hardware serial port for Arduino boards with multiple serial ports).
System Design:
Step 1: Arduino Hardware Setup
Connect the LED to the Arduino:
Connect the positive leg (longer one) of the LED to a digital pin (e.g., pin 13) on the Arduino.
Connect the negative leg (shorter one) of the LED to the ground (GND) pin on the Arduino through a 220Ω resistor.
Connect Bluetooth Module (HC-05/HC-06) to Arduino:
VCC of HC-05 → 5V (Arduino)
GND of HC-05 → GND (Arduino)
TX of HC-05 → RX (pin 0 on Arduino)
RX of HC-05 → TX (pin 1 on Arduino)
Step 2: Arduino Code
Here’s a simple Arduino sketch to receive commands from the mobile app over Bluetooth and turn the LED on/off:
#include <SoftwareSerial.h>

// Define Bluetooth Serial pins
SoftwareSerial BTSerial(2, 3);  // RX, TX

const int ledPin = 13;  // Pin where the LED is connected

void setup() {
  // Start Bluetooth communication
  BTSerial.begin(9600);  
  // Start Serial Monitor communication
  Serial.begin(9600);  

  // Set LED pin as output
  pinMode(ledPin, OUTPUT);  
}

void loop() {
  if (BTSerial.available()) {
    char command = BTSerial.read();  // Read command from mobile app
    
    if (command == '1') {
      digitalWrite(ledPin, HIGH);  // Turn LED ON
    } else if (command == '0') {
      digitalWrite(ledPin, LOW);   // Turn LED OFF
    }
  }
}
Step 3: Mobile App Development
Using MIT App Inventor:

MIT App Inventor is a user-friendly, drag-and-drop platform for creating mobile apps. You can create an app to communicate with the Bluetooth module.
Here are the steps:

Design the App Interface:

Create two buttons: one labeled "ON" and the other "OFF."
Bluetooth Connection:

Use the BluetoothClient component to manage Bluetooth communication between the phone and the Arduino.
Add event handlers for when the "ON" and "OFF" buttons are pressed.
Code Blocks for Bluetooth Communication:

When the "ON" button is pressed, send the character '1' to the Arduino via Bluetooth.
When the "OFF" button is pressed, send the character '0' to the Arduino via Bluetooth.
Example MIT App Inventor Blocks:

For the "ON" button:
BluetoothClient.SendText("1")
For the "OFF" button:
BluetoothClient.SendText("0")
Using Flutter or React Native:

Alternatively, you can use Flutter or React Native to build a more customizable app with Bluetooth support. You will need libraries like flutter_blue (for Flutter) or react-native-ble-plx (for React Native) to handle Bluetooth communication.
Step 4: Testing and Debugging
Upload the Arduino Code:

Use the Arduino IDE to upload the code to your Arduino board.
Install and Set Up the Mobile App:

Install the MIT App Inventor app on your mobile device or create an APK if you're using a custom app built with Flutter or React Native.
Pair your mobile device with the HC-05 Bluetooth module (the default PIN is usually 1234 or 0000).
Test the System:

Open the mobile app, connect to the Bluetooth module, and press the "ON" and "OFF" buttons to see the LED turn on and off based on your commands.
Conclusion:
This system allows you to control an LED light using a mobile app via Bluetooth. The Arduino listens for commands from the app, and depending on whether you send '1' or '0', it will turn the LED on or off.

Potential Enhancements:

Add dimming control by adjusting PWM (Pulse Width Modulation) on the LED pin.
Use Wi-Fi (e.g., ESP8266 or ESP32) instead of Bluetooth for a more advanced smart lighting system that can be controlled over the internet.
Add more lights and control them independently via the app.
