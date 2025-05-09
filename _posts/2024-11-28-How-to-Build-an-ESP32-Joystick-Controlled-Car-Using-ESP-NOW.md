---
layout: post
title:  How to Build an ESP32 Joystick-Controlled Car Using ESP-NOW
date: 2024-11-28 7:55
categories: [Robotics]

tags: [robotics, esp32, rc-car, esp-now, joystick, l298n, motor-driver, motor, car, rc, remote-control]
---

Creating a joystick-controlled car is an exciting way to learn about wireless communication, motor control, and hardware interfacing. This guide will walk you through the entire process of building one, step by step. We’ll use two ESP32 boards and ESP-NOW, a protocol designed for low-latency, peer-to-peer communication. By the end, you'll have a car that responds instantly to joystick movements without relying on Wi-Fi routers or complex networking setups.

Let’s dive in!

---

## **Project Overview**  

This project involves two ESP32 boards:  
- **Transmitter (Controller):** Reads joystick input and sends control commands wirelessly.  
- **Receiver (Car):** Interprets commands and drives motors accordingly.  

Using ESP-NOW ensures a direct and efficient connection between the two boards. This setup is great for remote-controlled cars, robots, or other wireless projects.  

---

## **What You'll Need**  

Here’s a list of components to gather:  

### **Hardware:**  
- 2 x ESP32 boards (one for the transmitter, one for the receiver)  
- USB joystick  
- Motor driver module (e.g., L298N)  
- 4 x DC motors  
- Chassis (a basic RC car or DIY frame)  
- 12V battery or power supply for motors  
- Jumper wires and breadboard  

### **Software:**  
- Arduino IDE (with ESP32 board support installed)  
- Arduino ESP32 Boards (Version 2.0.13)
- ESP32 Core Library (Version 2.0.17)

---

## **Step 1: Understand How the System Works**  

The joystick acts as the input device. Moving the joystick changes its X and Y values, which are interpreted as directional and speed commands.  

1. The **X-axis** controls left and right movement (steering).  
2. The **Y-axis** controls forward and backward movement (throttle).  

These values are sent via ESP-NOW from the transmitter ESP32 to the receiver ESP32. The receiver then translates these commands into motor speeds, driving the car.

---
![System Diagram](assets/Posts/Diagram.png)

## **Step 2: Setting Up the Transmitter (Joystick Controller)**  

The transmitter reads joystick input and sends data to the receiver.  

### **Step 2.1: Connecting the Joystick**  

For a USB joystick:  

ESP32 (Transmitter) Connections:
- GPIO 16 -> USB D+ (Green wire)
- GPIO 17 -> USB D- (White wire)
- GND -> USB GND (Black wire)
- 5V -> USB VCC (Red wire)

---

### **Step 2.2: Writing the Transmitter Code**  

Install the ESP32 libraries in the Arduino IDE if you haven’t already.  

#### **Joystick Calibration and Data Mapping**  

Most joysticks output raw values that need to be mapped into a usable range. Let’s convert them to a scale of 0 to 254, where 127 is the neutral (center) position.  

```cpp
int mapJoystickValue(int value, int minInput, int maxInput) {
    int deadZone = 20;  // Ignore minor fluctuations around the center
    int center = (maxInput + minInput) / 2;

    if (abs(value - center) < deadZone) return 127;  // Neutral position
    if (value > center) return map(value, center, maxInput, 127, 254);  // Forward/Right
    return map(value, minInput, center, 0, 127);  // Backward/Left
}
```

#### **Sending Data Using ESP-NOW**  

Define a structure to hold the joystick data and send it to the receiver:  

```cpp
#include <esp_now.h>
#include <WiFi.h>

typedef struct {
    uint8_t xAxis;
    uint8_t yAxis;
} JoystickData;

JoystickData joystickData;

void sendData() {
    esp_err_t result = esp_now_send(receiverMacAddress, (uint8_t *)&joystickData, sizeof(joystickData));
    if (result == ESP_OK) {
        Serial.println("Data sent successfully!");
    } else {
        Serial.println("Failed to send data.");
    }
}
```

*Note: Replace `receiverMacAddress` with the MAC address of the receiver ESP32.*

Here Is the Full Transmitter Code:  
Transmitter Code: **[Click here](https://github.com/ahammadnafiz/USB-Joystick-RC-Car/tree/main/Transmitter_Final)**

---

## **Step 3: Setting Up the Receiver (Car)**  

The receiver takes commands from the transmitter and drives the motors accordingly.  

### **Step 3.1: Wiring the Motor Driver**  

ESP32 (Receiver) Connections:
- GPIO 16 -> L298N IN1
- GPIO 17 -> L298N IN2
- GPIO 18 -> L298N IN3
- GPIO 19 -> L298N IN4
- GPIO  22-> L298N ENA
- GPIO 23 -> L298N ENB

L298N Motor Driver Connections:
- OUT1, OUT2 -> Right Motors
- OUT3, OUT4 -> Left Motors
- 12V -> Motor Power Supply (+)
- GND -> Motor Power Supply (-)
- 5V -> ESP32 VIN 
- GND -> ESP32 GND  

---

### **Step 3.2: Writing the Receiver Code**  

#### **Receiving ESP-NOW Data**  

Set up ESP-NOW to receive joystick data:  

```cpp
void onDataReceived(const uint8_t *macAddr, const uint8_t *incomingData, int len) {
    memcpy(&joystickData, incomingData, sizeof(joystickData));
    Serial.print("X: "); Serial.print(joystickData.xAxis);
    Serial.print(", Y: "); Serial.println(joystickData.yAxis);
}
```

#### **Controlling the Motors**  

Calculate the motor speeds based on joystick input:  

```cpp
void driveMotors(int xAxis, int yAxis) {
    int leftMotorSpeed = yAxis + (xAxis - 127);
    int rightMotorSpeed = yAxis - (xAxis - 127);

    leftMotorSpeed = constrain(leftMotorSpeed, -254, 254);
    rightMotorSpeed = constrain(rightMotorSpeed, -254, 254);

    analogWrite(leftMotorPWM, abs(leftMotorSpeed));
    digitalWrite(leftMotorDir, leftMotorSpeed > 0 ? HIGH : LOW);

    analogWrite(rightMotorPWM, abs(rightMotorSpeed));
    digitalWrite(rightMotorDir, rightMotorSpeed > 0 ? HIGH : LOW);
}
```
Here Is the Full Receiver Code:


Receiver Code : **[Click Here](https://github.com/ahammadnafiz/USB-Joystick-RC-Car/tree/main/Receiver_Final)**

---

## **Step 4: Testing and Debugging**  

1. Power both ESP32 boards and the motor driver.  
2. Open the serial monitor on the transmitter ESP32 to verify joystick input.  
3. Test the receiver by manually sending test data to the motors.  
4. Gradually test the entire system, making adjustments as needed.  

---

## **Expanding the Project**  

Once your car is up and running, you can enhance it:  
- **Add sensors:** Use ultrasonic sensors for obstacle avoidance.  
- **Add lighting:** Control LEDs for headlights or indicators.  
- **Control speed modes:** Assign joystick buttons for slow, medium, and fast modes.  

---

## **Conclusion**  

This joystick-controlled car project is a fantastic introduction to the ESP32 and ESP-NOW. You’ve learned how to integrate hardware, write code for both a transmitter and receiver, and debug a wireless system. Best of all, this project lays the foundation for more advanced robotics and IoT applications.  

Have fun driving your creation!