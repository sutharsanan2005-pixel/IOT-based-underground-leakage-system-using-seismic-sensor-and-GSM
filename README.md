# 🌐 IOT-Based Underground Leakage System Using Seismic Sensor and GSM

An IoT-powered system that detects underground water/gas pipe leakages using seismic vibration sensors and sends real-time SMS alerts via GSM module.

---

## 📌 Table of Contents
- [Overview](#overview)
- [Features](#features)
- [Components Required](#components-required)
- [System Architecture](#system-architecture)
- [Circuit Connections](#circuit-connections)
- [How It Works](#how-it-works)
- [Installation & Setup](#installation--setup)
- [Code Upload Steps](#code-upload-steps)
- [SMS Alert Format](#sms-alert-format)
- [Applications](#applications)
- [Future Improvements](#future-improvements)
- [License](#license)

---

## 🔍 Overview

Underground pipe leakages are a major cause of water and resource wastage. This project uses a **seismic/vibration sensor** to detect abnormal vibrations caused by leaks beneath the ground. When a leak is detected, the system immediately sends an **SMS alert** to the concerned authority using a **GSM module (SIM800L/SIM900A)**, enabling faster response and repair.

---

## ✨ Features

- 🔔 Real-time leakage detection using seismic/vibration sensors
- 📱 Instant SMS alert via GSM module
- ⚡ Low power consumption
- 📡 Works without internet — uses GSM cellular network
- 🔧 Easy to deploy underground or near pipelines
- 💡 LED indicator for local alert

---

## 🛒 Components Required

| Component | Quantity |
|---|---|
| Arduino UNO / Mega | 1 |
| Seismic / Vibration Sensor (SW-420 or Piezo) | 1 or more |
| GSM Module (SIM800L or SIM900A) | 1 |
| SIM Card (with SMS pack) | 1 |
| Power Supply (5V / 12V) | 1 |
| LED (Red) | 1 |
| Resistor (220Ω) | 1 |
| Jumper Wires | As needed |
| Breadboard / PCB | 1 |

---

## 🏗️ System Architecture

```
[Seismic Sensor]
       |
       v
[Arduino UNO]  ---->  [GSM Module (SIM800L)]  ---->  📱 SMS Alert
       |
       v
  [LED Indicator]
```

1. Seismic sensor continuously monitors vibrations
2. Arduino reads and analyzes sensor data
3. If vibration exceeds threshold → trigger alert
4. GSM module sends SMS to predefined number
5. LED lights up as local indicator

---

## 🔌 Circuit Connections

### Vibration Sensor (SW-420) → Arduino
| SW-420 Pin | Arduino Pin |
|---|---|
| VCC | 5V |
| GND | GND |
| DO (Digital Out) | D2 |

### GSM Module (SIM800L) → Arduino
| GSM Pin | Arduino Pin |
|---|---|
| VCC | External 4V (not Arduino 5V) |
| GND | GND |
| TX | D10 (RX of SoftwareSerial) |
| RX | D11 (TX of SoftwareSerial) |

### LED → Arduino
| LED | Arduino Pin |
|---|---|
| Anode (+) via 220Ω | D13 |
| Cathode (−) | GND |

---

## ⚙️ How It Works

1. **Sensing** — The seismic/vibration sensor detects ground vibrations near the pipeline.
2. **Processing** — Arduino reads the digital output from the sensor and checks if it crosses the threshold.
3. **Alert Trigger** — If a leakage vibration pattern is detected:
   - LED turns ON
   - GSM module sends an SMS to the authority's phone number
4. **Reset** — Once vibration stops, system returns to monitoring state.

---

## 🛠️ Installation & Setup

### 1. Clone this Repository
```bash
git clone https://github.com/sutharsanan2005-pixel/IOT-based-underground-leakage-system-using-seismic-sensor-and-GSM.git
cd IOT-based-underground-leakage-system-using-seismic-sensor-and-GSM
```

### 2. Install Arduino IDE
Download from: https://www.arduino.cc/en/software

### 3. Install Required Libraries
Open Arduino IDE → Sketch → Include Library → Manage Libraries

Search and install:
- `SoftwareSerial` (built-in)

### 4. Insert SIM Card
- Insert an active SIM card into the GSM module
- Make sure it has SMS balance

### 5. Update Phone Number in Code
Open the `.ino` file and update:
```cpp
String phoneNumber = "+91XXXXXXXXXX"; // Replace with your number
```

---

## 💻 Code Upload Steps

1. Connect Arduino to your PC via USB cable
2. Open Arduino IDE
3. Go to **Tools → Board** → Select `Arduino UNO`
4. Go to **Tools → Port** → Select the correct COM port
5. Open the project `.ino` file
6. Click **Upload** (→ arrow button)
7. Open **Serial Monitor** to view sensor readings

---

## 📩 SMS Alert Format

When a leak is detected, the following SMS is sent:

```
⚠️ ALERT: Underground Leakage Detected!
Location: Pipeline Zone A
Sensor: Seismic Sensor Triggered
Please take immediate action.
```

---

## 🌍 Applications

- Municipal water supply pipeline monitoring
- Oil & gas underground pipeline safety
- Industrial pipeline leak detection
- Smart city infrastructure management

---

## 🚀 Future Improvements

- [ ] Add GPS module for exact leak location tracking
- [ ] Integrate with IoT cloud dashboard (ThingSpeak / Blynk)
- [ ] Add multiple sensor zones for wider coverage
- [ ] Use machine learning to reduce false alerts
- [ ] Add buzzer for local audio alert

---

## 👨‍💻 Author

**Sutharsanan**
- GitHub: [@sutharsanan2005-pixel](https://github.com/sutharsanan2005-pixel)

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

⭐ **If you found this project helpful, please give it a star!** ⭐
