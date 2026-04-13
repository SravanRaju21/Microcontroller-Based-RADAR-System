# Microcontroller-Based-RADAR-System
A simple and cost-effective RADAR system built using a microcontroller and an ultrasonic sensor to detect objects and measure their distance in real time. This project simulates the working of a real RADAR by scanning the surroundings using a rotating sensor and displaying the detected objects based on distance and angle.
📡 Microcontroller-Based RADAR System
🎯 Objectives
To design a simple RADAR system using a microcontroller
To detect objects and measure their distance in real time
To simulate RADAR scanning using a rotating sensor
To visualize object position based on angle and distance
To understand the working of ultrasonic sensors and servo motors
🧰 Components Used
Arduino Uno
HC-SR04 Ultrasonic Sensor
Servo Motor (SG90)
Breadboard
Jumper Wires
USB Cable
🔌 Circuit Connections
📡 Ultrasonic Sensor (HC-SR04)
VCC → 5V (Arduino)
GND → GND (Arduino)
TRIG → Pin 9 (Arduino)
ECHO → Pin 10 (Arduino)
🔄 Servo Motor
VCC → 5V (Arduino)
GND → GND (Arduino)
Signal → Pin 11 (Arduino)
⚙️ Working Principle
The ultrasonic sensor sends sound waves toward an object
The waves reflect back after hitting the object
The time taken for the echo is measured
Distance is calculated using:
𝑑
=
𝑣
×
𝑡
2
d=
2
v×t
	​

The servo motor rotates from 0° to 180°
At each angle, distance is measured
Data is sent to the serial monitor / GUI
This creates a radar-like scanning effect
💻 Arduino Code
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

    // Send ultrasonic pulse
    digitalWrite(trigPin, LOW);
    delayMicroseconds(2);
    digitalWrite(trigPin, HIGH);
    delayMicroseconds(10);
    digitalWrite(trigPin, LOW);

    // Receive echo
    duration = pulseIn(echoPin, HIGH);

    // Calculate distance
    distance = duration * 0.034 / 2;

    // Print data (angle, distance)
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
⚡ Advantages
Simple and easy to implement
Low cost and widely available components
Low power consumption
Real-time object detection
Useful for learning embedded systems and sensors
Can be extended for robotics and automation
