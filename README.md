# 📡 Microcontroller-Based RADAR System

A simple and cost-effective RADAR system built using a microcontroller and an ultrasonic sensor to detect objects and measure their distance in real time. This project simulates the working of a real RADAR by scanning the surroundings using a rotating sensor and displaying the detected objects based on distance and angle.

## 🎯 Objectives
- Design a simple RADAR system using a microcontroller  
- Detect objects and measure their distance  
- Simulate radar scanning using a rotating sensor  
- Display object position based on angle and distance  
- Understand ultrasonic sensing and servo control  

---

## 🧰 Components Used
- Arduino Uno  
- HC-SR04 Ultrasonic Sensor  
- Servo Motor (SG90)  
- Breadboard  
- Jumper Wires  
- USB Cable  

---

## 🔌 Circuit Connections

### Ultrasonic Sensor
- VCC → 5V  
- GND → GND  
- TRIG → Pin 9  
- ECHO → Pin 10  

### Servo Motor
- VCC → 5V  
- GND → GND  
- Signal → Pin 11  

---

## ⚙️ Working Principle
The ultrasonic sensor emits sound waves and waits for the reflected signal from an object. The time taken for the echo to return is used to calculate distance.

A servo motor rotates the sensor from 0° to 180°, allowing the system to scan a wide area. At each angle, the distance is measured and sent to the serial monitor or graphical interface, creating a radar-like display.

---

## 💻 Arduino Code

```cpp
#include <Servo.h>

Servo myServo;

const int trigPin = 9;
const int echoPin = 10;
long duration;
int distance;

void setup() {
  Serial.begin(9600);
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  myServo.attach(11);
}

void loop() {
  for(int angle = 0; angle <= 180; angle++) {
    myServo.write(angle);
    delay(30);

    digitalWrite(trigPin, LOW);
    delayMicroseconds(2);
    digitalWrite(trigPin, HIGH);
    delayMicroseconds(10);
    digitalWrite(trigPin, LOW);

    duration = pulseIn(echoPin, HIGH);
    distance = duration * 0.034 / 2;

    Serial.print(angle);
    Serial.print(",");
    Serial.print(distance);
    Serial.print(".");
  }

  for(int angle = 180; angle >= 0; angle--) {
    myServo.write(angle);
    delay(30);

    digitalWrite(trigPin, LOW);
    delayMicroseconds(2);
    digitalWrite(trigPin, HIGH);
    delayMicroseconds(10);
    digitalWrite(trigPin, LOW);

    duration = pulseIn(echoPin, HIGH);
    distance = duration * 0.034 / 2;

    Serial.print(angle);
    Serial.print(",");
    Serial.print(distance);
    Serial.print(".");
  }
} 
