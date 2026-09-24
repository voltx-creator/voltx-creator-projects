# 🚦 VoltX Creator: Project #01 - Traffic Light with LCD Countdown Timer

Welcome to the official asset folder for the **Arduino Traffic Light with LCD Countdown Timer** featured on the VoltX Creator YouTube channel! ⚡

This advanced build uses a 16x2 LCD panel to show a live, dynamic countdown clock for each street light phase. 

## 🛠️ Components Required
* Arduino Uno / Nano
* 16x2 Character LCD Display
* 1x Red LED | 1x Yellow LED | 1x Green LED
* 3x 220-ohm Resistors (for LEDs)
* 1x 10k-ohm Potentiometer (for LCD contrast adjustment)
* Jumper Wires & Breadboard

## 📐 Circuit Connection Mapping

### 🖥️ 16x2 LCD Pin Connections:
* **RS** ➡️ Digital Pin 2
* **E**  ➡️ Digital Pin 3
* **D4** ➡️ Digital Pin 4
* **D5** ➡️ Digital Pin 5
* **D6** ➡️ Digital Pin 6
* **D7** ➡️ Digital Pin 7

### 🚨 Traffic Light LED Connections:
* **Red LED**    ➡️ Digital Pin 13 (via 220Ω Resistor)
* **Yellow LED** ➡️ Digital Pin 12 (via 220Ω Resistor)
* **Green LED**  ➡️ Digital Pin 11 (via 220Ω Resistor)
* **All Ground Lines** ➡️ Arduino **GND**

## 🖼️ Wiring Visual Blueprint
*(See the uploaded `circuit_diagram.png` file inside this folder for a clear breadboard wiring layout!)*

## 📜 Arduino Source Code (`traffic_light_lcd.ino`)
```cpp
#include <LiquidCrystal.h>

LiquidCrystal lcd(2, 3, 4, 5, 6, 7);

const int GREEN_LED = 11;
const int YELLOW_LED = 12;
const int RED_LED = 13;

const int RED_TIME = 15;
const int GREEN_TIME = 12;
const int YELLOW_TIME = 3;

void setup() {
  pinMode(GREEN_LED, OUTPUT);
  pinMode(YELLOW_LED, OUTPUT);
  pinMode(RED_LED, OUTPUT);
  lcd.begin(16, 2);
}

void loop() {
  runTrafficPhase(RED_LED, RED_TIME, "STOP: RED");
  runTrafficPhase(GREEN_LED, GREEN_TIME, "GO: GREEN");
  runTrafficPhase(YELLOW_LED, YELLOW_TIME, "CAUTION: YELLOW");
}

void runTrafficPhase(int activeLed, int duration, String statusMessage) {
  digitalWrite(GREEN_LED, LOW);
  digitalWrite(YELLOW_LED, LOW);
  digitalWrite(RED_LED, LOW);
  
  digitalWrite(activeLed, HIGH);
  
  for (int timeLeft = duration; timeLeft > 0; timeLeft--) {
    lcd.clear();
    lcd.setCursor(0, 0);
    lcd.print(statusMessage);
    
    lcd.setCursor(0, 1);
    lcd.print("Time Left: ");
    lcd.print(timeLeft);
    lcd.print("s");
    
    delay(1000);
  }
}
```

---
*If you loved this build, drop a ⭐ **Star** on this repository and subscribe to **VoltX Creator** on YouTube for new projects every 2 days!*

