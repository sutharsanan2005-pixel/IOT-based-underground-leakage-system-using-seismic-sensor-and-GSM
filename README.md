# 🌐 IOT-Based Underground Leakage System Using Seismic Sensor and GSM

A smart, low-cost IoT system that detects underground pipeline leaks using vibration sensing and sends real-time SMS alerts via GSM — no internet required.

---

## 📄 Abstract

This project introduces an IoT-based underground leak detection system designed to monitor buried pipelines in real time. It uses an **MPU-6500 accelerometer** to capture seismic vibrations, a **DHT11 sensor** for temperature and humidity, and an **ESP32 microcontroller** for processing. When a leak is detected, the **SIM800L GSM module** sends an instant SMS alert. Power is supplied by an **18650 Li-ion battery** with TP4056 and LM317 regulation. The system operated continuously for up to **18 hours** on a single charge and was tested across dry, semi-wet, and saturated soil conditions.

**Keywords:** IoT, Leak Detection, Seismic Sensor, GSM, ESP32, Vibration Sensing

---

## ✨ Features

- Real-time leakage detection using MPU-6500 vibration sensor
- Instant SMS alert via SIM800L GSM — works without Wi-Fi
- Environmental monitoring with DHT11 (temperature & humidity)
- ESP32 dual-core MCU with deep sleep power optimization
- MicroSD card support for offline data logging
- Optional cloud integration with Firebase / ThingSpeak
- Up to 18 hours continuous operation on a single charge
- Compact and modular — suitable for urban, rural, and remote areas

---

## 🛒 Components Required

| Component | Description |
|---|---|
| ESP32 Microcontroller | Dual-core MCU with Wi-Fi & Bluetooth |
| MPU-6500 | 6-axis accelerometer + gyroscope (vibration sensor) |
| DHT11 Sensor | Temperature (0–50°C) and humidity (20–90% RH) |
| SIM800L GSM Module | Quad-band GSM — sends SMS alerts via UART |
| 18650 Li-ion Battery | 3.7V, 2200–3000mAh rechargeable power source |
| TP4056 Charging Module | Battery charge manager with protection |
| LM317 Voltage Regulator | Provides stable 4.0V output for SIM800L |
| MicroSD Card Module | Optional offline data logging via SPI |
| Logic Level Shifter | 4-channel 3.3V ↔ 5V for ESP32 ↔ SIM800L |
| Resistors & Capacitors | 220Ω, 1kΩ resistors; 10µF, 100µF capacitors |

---

## 🏗️ System Architecture

```
┌──────────────────────────────────────────────┐
│              SENSING LAYER                   │
│   MPU-6500 (Vibration) + DHT11 (Temp/Hum)   │
└─────────────────┬────────────────────────────┘
                  │ I²C / GPIO
┌─────────────────▼────────────────────────────┐
│             PROCESSING LAYER                 │
│        ESP32 Microcontroller (MCU)           │
└──────────┬───────────────────────────────────┘
           │ UART                  │ Power
┌──────────▼──────────┐  ┌────────▼──────────────┐
│  COMMUNICATION      │  │  POWER MANAGEMENT     │
│  SIM800L → SMS      │  │  18650 + TP4056       │
│  Wi-Fi → Firebase   │  │  + LM317 (4.0V)       │
│  MicroSD → Logs     │  └───────────────────────┘
└─────────────────────┘
```

---

## 🔌 Circuit Connections

### MPU-6500 → ESP32

| MPU-6500 | ESP32 |
|---|---|
| VCC | 3.3V |
| GND | GND |
| SCL | GPIO 22 |
| SDA | GPIO 21 |

### SIM800L → ESP32 (via Logic Level Shifter)

| SIM800L | Connection |
|---|---|
| VCC | External 5V supply |
| GND | Common GND |
| TX | Level Shifter → GPIO 16 (RX2) |
| RX | Level Shifter → GPIO 17 (TX2) |

### DHT11 → ESP32

| DHT11 | ESP32 |
|---|---|
| VCC | 3.3V |
| GND | GND |
| DATA | Any Digital GPIO |

### Power Chain

```
18650 → TP4056 → LM317 (4.0V) → SIM800L
18650 → ESP32 VIN → 3.3V reg → MPU-6500, DHT11
```

> ⚠️ Do NOT power SIM800L from ESP32 directly — use a dedicated 5V supply with at least 2A peak current.

---

## ⚙️ How It Works

1. MPU-6500 continuously monitors ground vibrations at **100 Hz**
2. DHT11 logs temperature and humidity every 10 seconds
3. ESP32 applies moving average filtering to reduce noise
4. If Z-axis vibration exceeds **±1.2g** → leak is detected
5. SIM800L sends SMS alert within **5 seconds**
6. All data is logged to MicroSD with timestamps

---

## 💻 Code Upload Steps

1. Download and install [Arduino IDE](https://www.arduino.cc/en/software)
2. Add ESP32 board support via Board Manager
3. Install libraries: `Wire`, `DHT`, `MPU6500`, `SD`, `SoftwareSerial`
4. Insert active SIM card into SIM800L
5. Update phone number in code: `String phoneNumber = "+91XXXXXXXXXX";`
6. Select **Tools → Board: ESP32 Dev Module**
7. Select correct **Tools → Port**
8. Click **Upload →**
9. Open **Serial Monitor** at 115200 baud to verify sensor readings

---

## 📊 Test Results

| Scenario | Z-Axis Vibration | Temp (°C) | Humidity (%) | Leak Detected |
|---|---|---|---|---|
| Normal | ±0.25g | 29.1 | 58 | No |
| Leak #1 — Slow | ±1.35g | 29.3 | 60 | Yes |
| Leak #2 — Medium | ±1.65g | 29.5 | 61 | Yes |
| Leak #3 — High Pressure | ±2.10g | 29.6 | 63 | Yes |

- SMS alert delivered in **< 5 seconds**
- Works in weak GSM signal areas (< 10 sec delivery)
- Battery life: **18 hours** continuous operation

---

## 📩 SMS Alert Format

```
ALERT: Underground Leak Detected!
Sensor: MPU-6500 Z-axis vibration exceeded threshold
Vibration: 1.35g | Temp: 29.3C | Humidity: 60%
Action: Please inspect pipeline immediately.
```

---

## 💾 Data Logging

Each MicroSD log entry contains:
- Timestamp
- Sensor ID
- X, Y, Z vibration readings
- Temperature & humidity
- Leak status (Yes / No)

Format: **CSV or JSON** — compatible with Excel, Python, MATLAB, Firebase, ThingSpeak.

---

## 🚀 Future Scope

- **GPS Geotagging** — exact leak location in SMS
- **Cloud Dashboard** — Firebase / ThingSpeak real-time monitoring
- **Solar Power** — unlimited runtime in outdoor deployments
- **Edge AI (LSTM)** — intelligent leak classification, fewer false alerts
- **Piezoelectric Harvesting** — self-powered sensor nodes
- **Multi-Node Network** — city-wide pipeline monitoring

---

## 📄 License

This project is open source and free to use for educational and research purposes.

---

⭐ If you found this project helpful, please give it a star!
