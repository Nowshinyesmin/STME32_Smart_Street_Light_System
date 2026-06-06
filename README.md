# STM32 Smart Street Light System

An automated street light control system developed in C using **STM32CubeIDE** and an **STM32F103C8T6 (Blue Pill)** microcontroller.

## 🛠️ Components Used
* **Microcontroller:** STM32F103C8T6 (Blue Pill)
* **Light Sensor:** LDR (Light Dependent Resistor) connected to `PA1` (ADC1_IN1)
* **Presence Sensor:** HC-SR04 Ultrasonic Sonar (Trig: `PA9`, Echo: `PA8`)
* **Street Light:** Yellow LED connected to `PA6` (GPIO_Output)

## ⚙️ Core Logic
1. **Day/Night Detection:** The system continuously polls the LDR sensor. If the environment light value transitions to night threshold (>3000), it activates the ultrasonic logic.
2. **Presence-Aware Lighting:** During nighttime, if an object or pedestrian is detected by the sonar sensor within a **20cm range**, the external LED street light safely toggles ON. Otherwise, it remains OFF or goes back to standby to optimize energy efficiency.
