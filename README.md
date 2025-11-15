# Smart Water Tank Monitoring & Leak Detection System – Arduino

This Arduino project implements a **smart water management and safety system** by combining multiple sensors and solenoid valves. It monitors **pH level**, **water flow**, **tank water level**, and detects **leaks** using intelligent logic. All data is transmitted in real time using an **HC-05 Bluetooth module**.

---

## 🚀 Features

### 🔹 Water Quality Monitoring (pH Sensor)
- Reads and averages analog pH sensor values
- Acceptable water range: **6 – 8**
- Marks water as **Unusable** when pH is out of range
- Automatically closes solenoid valves when unsafe

### 🔹 Flow Monitoring (Two YF-S201 Sensors)
- Measures inflow and outflow
- Detects:
  - No water entering
  - Flow stoppage
  - Flow differences that indicate leakage
- Uses hardware interrupts for accurate pulse counting

### 🔹 Ultrasonic Tank Level Monitoring (HC-SR04)
- Measures tank water height
- Detects:
  - Tank full
  - Tank filling
  - Sudden drops in water level (leak detection)

### 🔹 Advanced Leak Detection
Leak is triggered when:
- Flow rate is **zero**  
- But water level drops **> 1 cm** in 2 seconds  
- OR flow difference between sensors exceeds threshold

Leak mode:
- Activates safety valves
- Sends continuous Bluetooth warnings
- Requires manual reset through switch

### 🔹 Bluetooth Monitoring (HC-05)
Sends real-time data:
- pH value  
- Flow rates  
- Water level  
- Tank status  
- Leak alerts  

Compatible with mobile apps such as **Serial Bluetooth Terminal**.

### 🔹 Automatic Solenoid Valve Control
- Opens/closes IN and OUT valves based on sensor data
- Ensures safety during leak or bad water conditions

---

## 🛠 Hardware Components

| Component | Quantity | Purpose |
|----------|----------|---------|
| Arduino UNO/Mega | 1 | Main controller |
| YF-S201 Flow Sensor | 2 | Measure inflow/outflow |
| HC-SR04 Ultrasonic Sensor | 1 | Tank water level |
| Solenoid Valves | 2 | Control water IN/OUT |
| Analog pH Sensor | 1 | Water quality |
| HC-05 Bluetooth Module | 1 | Wireless monitoring |
| Push Button | 1 | Leakage reset |
| Jumper Wires | — | Connections |

---

## 📌 Pin Configuration

### Flow Sensors
| Sensor | Pin |
|--------|-----|
| Flow Sensor 1 | D2 (interrupt) |
| Flow Sensor 2 | D3 (interrupt) |

### Ultrasonic Sensor (HC-SR04)
| Pin | Arduino |
|-----|---------|
| Trig | 5 |
| Echo | 6 |

### Solenoid Valves
| Solenoid | Pin |
|----------|------|
| solenoid_in | 11 |
| solenoid_out | 12 |

### Bluetooth Module (HC-05)
| Module Pin | Arduino |
|------------|----------|
| RX | D8 |
| TX | D9 |

### Other Sensors / Inputs
| Device | Pin |
|--------|------|
| pH Sensor | A0 |
| Switch (reset) | D13 |

---

## 📂 Project Overview

The system continuously performs:

1. **pH Reading**
   - Reads 10 samples
   - Sorts and averages middle values
   - Converts to calibrated pH value

2. **Flow Rate Calculation**
   - Based on pulse count from YF-S201 sensors
   - Uses interrupts for accuracy

3. **Distance Measurement**
   - Ultrasonic sensor measures water level
   - Lower values = tank full

4. **Leak Detection Logic**
   - Compares flow rates
   - Checks for unexpected water level drop
   - Raises warnings and locks valves

5. **Valve Control**
   - Opens water input when tank is not full
   - Closes when full
   - Locks into safety mode during leaks

6. **Bluetooth Data Transmission**
   - Sends sensor values and alerts every 1.5 seconds

---

## 🧪 Leak Detection Rules

A leak is detected if:

### Rule 1 — Level Drop Leak
- flowRate == 0  
- AND (distance1 - distance2) > 1 cm  
- → **Leak detected**

### Rule 2 — Flow Difference Leak


### Rule 3 — Manual Reset
Leakage stops 
---

## 🔧 How to Run the System

1. Upload the code to Arduino  
2. Power sensors and valves properly  
3. Open Bluetooth app and pair with **HC-05**  
4. Monitor live readings  
5. Press reset switch if leak mode activates  

---

