# Task-1-Read-temperature-from-LM35-Potentiometer-and-display-on-12C-LCD.
Task1
# 🌡️ Task 1: Temperature Monitoring System

### Alfido Tech - Embedded Systems Internship

This repository contains the solution for Task 1, which involves reading temperature data from an LM35 sensor and displaying it on a 16x2 I2C LCD using an Arduino UNO.

## 👤 Intern Details
* **Name:** ANISH KUMAR
* **Internship ID:** BS/REG/122708
* **Domain:** Embedded Systems

## 🛠️ Hardware Components
1. Arduino UNO
2. LM35 Temperature Sensor (Simulated)
3. 16x2 I2C LCD Display
4. Breadboard & Jumper Wires

## 📸 Circuit Diagram
[Circuit Diagram](Circuit_Diagram.jpg)

## 🎥 Working Demonstration
Below is the 60-second live demonstration of the simulation. As the sensor values are adjusted, the temperature updates in real-time on both the Serial Monitor and the I2C LCD.


<video src="https://github.com/anishkumar8318/Task-1-Read-temperature-from-LM35-Potentiometer-and-display-on-12C-LCD./raw/refs/heads/main/README.md" controls="controls" style="max-width: 100%;"></video>

## 💻 Arduino Source Code

```cpp
#include <Wire.h>
#include <LiquidCrystal_I2C.h>

// Initialize the LCD. standard I2C address is 0x27 or 0x3F for a 16x2 display
LiquidCrystal_I2C lcd(0x27, 16, 2);

const int lm35_pin = A0; // LM35 Vout connected to Analog Pin A0

void setup() {
  // Initialize LCD
  lcd.init();
  lcd.backlight();
  
  // Welcome Message
  lcd.setCursor(0, 0);
  lcd.print("Temp Monitor");
  lcd.setCursor(0, 1);
  lcd.print("System Ready...");
  delay(2000);
  lcd.clear();
}

void loop() {
  // Read raw analog value from LM35
  int raw_val = analogRead(lm35_pin);
  
  // Convert analog reading to voltage (for 5V Arduino)
  float voltage = raw_val * (5.0 / 1023.0);
  
  // LM35 outputs 10mV per degree Celsius (10mV = 0.01V)
  float temperatureC = voltage * 100.0;
  
  // Display data on 16x2 LCD
  lcd.setCursor(0, 0);
  lcd.print("Alfido Tech Task");
  
  lcd.setCursor(0, 1);
  lcd.print("Temp: ");
  lcd.print(temperatureC, 1); // Display temperature with 1 decimal place
  lcd.print((char)223);       // Degree symbol character code
  lcd.print("C   ");          // Extra spaces to clear previous digits
  
  delay(1000); // Update reading every 1 second
}
