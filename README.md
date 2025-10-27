# Capston-Project

# 🚗 Sensor-Based Parking Assistance System  
### Intelligent Hardware + Real-Time Alerts + Bluetooth Integration

This project is a prototype of an intelligent parking assistance system designed to help drivers safely maneuver vehicles in tight spaces. It uses ultrasonic sensors for obstacle detection and gives visual + audio feedback. Sensor data is also transmitted to a mobile app via Bluetooth.

---

## 🎯 Features

✅ 4-Directional Obstacle Detection  
✅ Real-Time Distance Monitoring  
✅ Buzzer & LED Alerts Based on Danger Level  
✅ Bluetooth HC-05 Communication  
✅ Low-Cost & Beginner Friendly  
✅ Expandable for Autonomous Parking

---

## 🧠 Working Principle

The sensors measure the distance from obstacles and the Arduino processes the data. Depending on the proximity:

| Distance Range | Alert Type | Safety Level |
|----------------|-----------|--------------|
| 0 – 15 cm | Continuous buzzer + LED ON | 🚨 High Danger |
| 15 – 30 cm | Fast beeps + LED ON | ⚠ Warning |
| 30 – 60 cm | Slow beeps + LED ON | 🙂 Safe Zone |
| Above 60 cm | No alerts | ✅ Clear |

Sensor data is also sent to the mobile app for live monitoring.

---

## 🔌 Hardware Components

| Component | Quantity |
|----------|----------|
| Arduino Uno | 1 |
| Ultrasonic Sensors HC-SR04 | 4 |
| Buzzer | 1 |
| LEDs | 3 |
| Bluetooth Module HC-05 | 1 |
| Motor Driver + Motors (optional) | Used for robot movement |
| Chassis / Model Car | 1 |
| Jumper Wires, Breadboard, Power Supply | As required |

---

## 🧩 System Architecture

Ultrasonic Sensors → Arduino Uno → Buzzer / LEDs → Driver Alerts
↓
Bluetooth HC-05
↓
Mobile App Display


---

## 📟 Arduino Source Code

```cpp
// ✅ Sensor-Based Parking Assistance System
// Ultrasonic Sensors + LEDs + Buzzer + Bluetooth HC-05

const int trigFront = 2, echoFront = 3;
const int trigBack  = 4, echoBack  = 5;
const int trigLeft  = 6, echoLeft  = 7;
const int trigRight = 8, echoRight = 9;

const int buzzerPin = 10;
const int ledFront = 11;
const int ledBack  = 12;
const int ledSide  = 13;

int getDistance(int trigPin, int echoPin) {
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  long duration = pulseIn(echoPin, HIGH, 30000);
  if (duration == 0) return 999;

  return duration * 0.034 / 2;
}

void setup() {
  Serial.begin(9600);

  pinMode(trigFront, OUTPUT); pinMode(echoFront, INPUT);
  pinMode(trigBack,  OUTPUT); pinMode(echoBack, INPUT);
  pinMode(trigLeft,  OUTPUT); pinMode(echoLeft, INPUT);
  pinMode(trigRight, OUTPUT); pinMode(echoRight, INPUT);

  pinMode(buzzerPin, OUTPUT);
  pinMode(ledFront, OUTPUT);
  pinMode(ledBack,  OUTPUT);
  pinMode(ledSide,  OUTPUT);

  Serial.println("✅ Parking Assist System Ready");
}

void loop() {
  int distFront = getDistance(trigFront, echoFront);
  int distBack  = getDistance(trigBack, echoBack);
  int distLeft  = getDistance(trigLeft, echoLeft);
  int distRight = getDistance(trigRight, echoRight);

  Serial.print("Front:"); Serial.print(distFront); Serial.print("cm ");
  Serial.print("Back:");  Serial.print(distBack);  Serial.print("cm ");
  Serial.print("Left:");  Serial.print(distLeft);  Serial.print("cm ");
  Serial.print("Right:"); Serial.print(distRight); Serial.println("cm");

  digitalWrite(buzzerPin, LOW);
  digitalWrite(ledFront, LOW);
  digitalWrite(ledBack, LOW);
  digitalWrite(ledSide, LOW);

  processSensor(distFront, ledFront, "Front");
  processSensor(distBack,  ledBack,  "Back");
  processSensor(distLeft,  ledSide,  "Left");
  processSensor(distRight, ledSide,  "Right");

  delay(200);
}

void processSensor(int distance, int ledPin, String direction) {
  if (distance > 0 && distance <= 15) {
    digitalWrite(buzzerPin, HIGH);
    digitalWrite(ledPin, HIGH);
    Serial.println("⚠ DANGER " + direction + "!");
  }
  else if (distance > 15 && distance <= 30) {
    digitalWrite(ledPin, HIGH);
    digitalWrite(buzzerPin, HIGH);
    delay(100);
    digitalWrite(buzzerPin, LOW);
    delay(100);
  }
  else if (distance > 30 && distance <= 60) {
    digitalWrite(ledPin, HIGH);
    digitalWrite(buzzerPin, HIGH);
    delay(300);
    digitalWrite(buzzerPin, LOW);
    delay(300);
  }
}

📱 Mobile App Support

Receives real-time distance values via Bluetooth

Alerts based on proximity

Can be extended into remote control in future updates

🚀 Future Enhancements

🔹 Camera + OpenCV for parking line detection
🔹 Auto-parking algorithms
🔹 Voice command support
🔹 App UI for vehicle control

👨‍💻 Team Members

Bollu Nagaraju Kumar

(Add your teammates names here)

📌 License

Open-source — free for educational use 👨‍🎓

🌟 If you like this project, please ⭐ the repository!

---

If you want, I can also create:  
✅ A **project banner image** for GitHub  
✅ A **schematic diagram** section  
✅ Badges (Arduino, C++, License, Releases, etc.)  

Would you like me to design a **professional repository logo/banner** next?
