# Embedded Smart Home Control System

**PIC16F876A · Assembly · Custom PCBs · AC/DC Control**

---

## Overview

The **Embedded Smart Home Control System** is a modular, microcontroller-based home automation prototype designed and implemented using **PIC16F876A microcontrollers** programmed entirely in **assembly language**.

The system integrates real-world sensors, custom PCB designs, relay modules, and AC/DC power control to demonstrate **practical embedded systems engineering**.

The project is divided into **three independent control boards**, each responsible for a specific subsystem:

- Occupancy-aware lighting and daylight detection  
- Temperature-based fan and AC heater control  
- Automatic water dispensing with timed logic  

This project emphasizes **low-level firmware design**, **hardware interfacing**, and **real-world control logic**, rather than high-level frameworks.

---

## System Architecture

The system is composed of **three standalone embedded boards**, each powered by a regulated **5V adapter** and built on **single-layer custom PCBs**.

### High-level flow

Each board operates independently, allowing **modular testing, debugging, and expansion**.

---

## Hardware Design

---

### Board 1 — Occupancy & Lighting Controller

**Purpose**  
Automate indoor and outdoor lighting based on occupancy and ambient light conditions.

**Microcontroller**
- PIC16F876A  
- Firmware written in assembly language  

**Inputs**
- Reflective optical sensor (people detection / occupancy count)  
- Photoresistor (day/night detection via ADC)  
- Three indoor wall switches (one per lighting zone)  

**Outputs**
- Three indoor LED lighting zones  
- Outdoor LED lighting  

**Control Logic**
- Maintains an **occupancy counter**
- **If occupancy = 0**
  - All indoor lights forced **OFF**
  - Indoor switches **disabled**
- **If occupancy > 0**
  - Indoor switches enabled per zone
- **Outdoor lights**
  - **ON** when ambient light is below threshold (night)
  - **OFF** during daylight

**Key Embedded Concepts**
- Sensor debouncing  
- ADC threshold comparison  
- Conditional I/O gating  
- State-based logic in assembly  

---

### Board 2 — Temperature Control with AC Heater (SCR Interface)

**Purpose**  
Maintain temperature using a fan for cooling and an AC heater for warming.

**Microcontroller**
- PIC16F876A  
- Assembly language firmware  

**Inputs**
- Thermal sensor (ADC input)

**Outputs**
- DC cooling fan (via relay module)  
- AC heating element (hair dryer heater) controlled using an **SCR**

**Temperature Thresholds**
- **Fan ON:** ≥ 28°C  
- **Heater ON:** ≤ 20°C  

**AC/DC Interface**
- SCR used as a **direct gate-driven interface** between the PIC and AC heater  
- DC logic safely triggers high-power AC load  

⚠️ **Safety Note**  
This prototype used **direct SCR gate drive** for educational purposes.  
Production designs should include:
- Opto-isolation  
- Snubber circuits  
- Proper fusing and protection  

**Key Embedded Concepts**
- Analog temperature sensing  
- Threshold-based control with hysteresis  
- AC load control from a low-voltage MCU  
- Power electronics integration  

---

### Board 3 — Automatic Sink Controller

**Purpose**  
Control a water pump based on hand detection with a fixed activation time.

**Microcontroller**
- PIC16F876A  
- Assembly language firmware  

**Inputs**
- Optical hand-detection sensor  

**Outputs**
- 5V DC water pump (relay-controlled)  

**Control Logic**
- Detects hand presence (**rising edge**)  
- Activates pump for **7 seconds**  
- Pump shuts **OFF automatically**  
- Requires hands to be removed before re-triggering  

**Key Embedded Concepts**
- Edge detection  
- Timer-based control  
- Simple finite state machine  
- Deterministic timing in assembly  

---

## Firmware Design

All firmware was developed in **PIC assembly**, focusing on:

- Direct register manipulation  
- ADC configuration and polling  
- Software timers  
- State-machine logic  
- Efficient control loops  

This low-level approach provides **fine-grained control** and a strong understanding of **microcontroller internals**.

---

## PCB Design & Fabrication

- Custom **single-layer PCBs** designed using **PCB Wizard**  
- Manual etching and component soldering  
- Modular board layout for clarity and debugging  
- Separate power and signal routing where possible  

Each board was **fabricated and tested independently**.

---

## Testing & Results

- Occupancy detection reliably enabled/disabled lighting  
- Day/night lighting responded correctly to ambient conditions  
- Temperature control maintained defined thresholds  
- Automatic sink consistently delivered timed water flow  
- System demonstrated stable operation under repeated use  

---

## Challenges & Lessons Learned

- Assembly-level programming requires careful timing and structure  
- AC/DC interfacing demands strict safety considerations  
- Sensor noise and debouncing are critical in real-world systems  
- Modular hardware design greatly simplifies debugging  

---

## Future Improvements

- Replace direct SCR gate drive with **opto-isolated triac drivers**  
- Add serial communication between boards  
- Implement EEPROM logging of events  
- Upgrade lighting control to **PWM dimming**  
- Add enclosure and EMI protection  

---

## Technologies Used

- PIC16F876A  
- Assembly Language  
- Reflective optical sensors  
- Photoresistors  
- Thermal sensors  
- Relay modules  
- SCR-based AC control  
- Custom PCBs  

---

## Why This Project Matters

This project demonstrates:

- Low-level embedded firmware development  
- Real-world hardware/software integration  
- AC and DC power control  
- Custom PCB design and fabrication  

It reflects **practical skills directly applicable to embedded systems, firmware, and hardware engineering roles**.


