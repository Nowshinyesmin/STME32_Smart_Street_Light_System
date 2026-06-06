# STM32 Smart Street Light System

An automated street light control system developed in C using **STM32CubeIDE** and an **STM32F103C8T6 (Blue Pill)** microcontroller.

## 🛠️ Components Used
* **Microcontroller:** STM32F103C8T6 (Blue Pill)
* **Light Sensor:** LDR (Light Dependent Resistor) connected to `PA1` (ADC1_IN1)
* **Presence Sensor:** HC-SR04 Ultrasonic Sonar (Trig: `PA9`, Echo: `PA8`)
* **Street Light:** White LED connected to `PA6` (GPIO_Output)

## ⚙️ Core Logic
1. **Day/Night Detection:** The system continuously polls the LDR sensor. If the environment light value transitions to night threshold (>3000), it activates the ultrasonic logic.
2. **Presence-Aware Lighting:** During nighttime, if an object or pedestrian is detected by the sonar sensor within a **20cm range**, the external LED street light safely toggles ON. Otherwise, it remains OFF or goes back to standby to optimize energy efficiency.
   
### ⚡ High-Voltage Scaling (Real-World Implementation)
While this prototype uses a low-power test LED to simulate a street light, the core firmware is fully architecture-ready for real-world municipal deployment. 

To control a standard AC street lamp ($220\text{V}$), the digital output signal from **PA6** can be routed directly to a **Relay Module** (e.g., SRD-05VDC-SL-C) rather than an LED. 

* **Microcontroller Isolation:** The relay acts as an isolated electronic switch, allowing the STM32's 3.3V/5V logic side to safely close a high-voltage AC grid circuit without physical or electrical back-feeding.
* **Firmware Compatibility:** Because the relay triggers on standard active-high/active-low GPIO states, the current code logic requires **zero modification** to actuate commercial scale lighting systems.
