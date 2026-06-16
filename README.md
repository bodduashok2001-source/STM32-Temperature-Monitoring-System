# Real-Time Internal Temperature Monitoring & Session-Based Peak Logging using STM32F407

## Overview

This project implements a real-time temperature monitoring system using the STM32F407VGT6 ARM Cortex-M4 microcontroller. The system continuously measures the internal temperature sensor using ADC with DMA, records the maximum temperature observed during each measurement session, and allows users to retrieve stored session results through UART communication.

The project demonstrates practical implementation of ADC, DMA, UART, Timers, GPIO Interrupts, and ARM Cortex-M4 interrupt handling in an embedded environment.

---

## Key Features

* Real-time internal temperature monitoring
* ADC with DMA for efficient data acquisition
* Session-based maximum temperature logging
* Push-button controlled measurement sessions
* UART communication for live monitoring and data retrieval
* Interrupt-driven architecture using NVIC
* Low CPU utilization through DMA-based transfers
* Storage of multiple session-wise peak temperature values

---

## Hardware Requirements

* STM32F407VGT6 Development Board
* USB Cable
* Push Button (PA0)
* USB-to-UART Converter (Optional)
* PC/Laptop with Serial Terminal Software

---

## Software Requirements

* STM32CubeMX
* Keil µVision / STM32CubeIDE
* STM32 HAL Drivers
* PuTTY / TeraTerm / Arduino Serial Monitor

---

## System Architecture

```text
Internal Temperature Sensor
            │
            ▼
         ADC + DMA
            │
            ▼
 Temperature Calculation
            │
            ▼
 Session Maximum Logger
            │
    ┌───────┴────────┐
    ▼                ▼
 TIM4 Timer       UART Interface
(Session Time)    (USART2)
    │                │
    ▼                ▼
 Push Button      PC Terminal
 (EXTI PA0)
```

---

## Working Principle

### Start Measurement

1. User presses the push button connected to PA0.
2. External interrupt (EXTI) is triggered.
3. A measurement session starts.
4. Timer-4 begins counting the measurement duration.

### During Measurement

* ADC continuously samples the internal temperature sensor.
* DMA transfers ADC data directly to memory.
* Temperature is calculated using factory calibration constants.
* The maximum temperature value is tracked.

### End of Session

* Timer expires after the configured duration.
* Maximum temperature is stored in memory.
* Measurement session stops automatically.

### Retrieve Logged Data

Send the following command through UART:

```text
R
```

Example Output:

```text
Session 1 Max Temperature = 34.52C
Session 2 Max Temperature = 35.11C
Session 3 Max Temperature = 35.87C
```

---

## Peripherals Used

| Peripheral | Function                             |
| ---------- | ------------------------------------ |
| ADC1       | Internal Temperature Sensor Sampling |
| DMA2       | ADC Data Transfer                    |
| TIM3       | ADC Trigger Generation               |
| TIM4       | Measurement Session Timer            |
| USART2     | UART Communication                   |
| GPIO PA0   | User Button (EXTI)                   |
| GPIO PB0   | ADC Activity Indicator               |

---

## ARM Cortex-M4 Features Utilized

* Nested Vectored Interrupt Controller (NVIC)
* Hardware Interrupt Handling
* DMA-Based Data Transfer
* Timer Interrupts
* UART Receive Interrupts
* External GPIO Interrupts

---

## Project Workflow

```text
Button Press
     │
     ▼
Start Measurement
     │
     ▼
ADC + DMA Acquisition
     │
     ▼
Calculate Temperature
     │
     ▼
Update Maximum Value
     │
     ▼
Timer Expired?
   ├── No → Continue Sampling
   └── Yes
          │
          ▼
 Store Maximum Value
          │
          ▼
 Wait for UART Command 'R'
          │
          ▼
 Display Stored Results
```

---

## Sample UART Output

```text
Measurement STARTED

Temperature = 34.21C
Temperature = 34.33C
Temperature = 34.55C
Temperature = 34.71C

Measurement STOPPED
```

Retrieve Stored Results:

```text
R

Session 1 Max Temperature = 34.71C
Session 2 Max Temperature = 35.10C
Session 3 Max Temperature = 35.45C
```

---

## Performance Highlights

| Parameter        | Value            |
| ---------------- | ---------------- |
| ADC Resolution   | 12-bit           |
| UART Baud Rate   | 115200 bps       |
| Data Acquisition | ADC + DMA        |
| CPU Utilization  | Low              |
| Response Time    | Few Milliseconds |
| Architecture     | Interrupt Driven |

---

## Learning Outcomes

Through this project, I gained hands-on experience with:

* STM32 Peripheral Configuration
* ADC with DMA
* UART Communication
* Timer-Based Event Handling
* Interrupt-Driven Embedded Design
* ARM Cortex-M4 Architecture
* Real-Time Data Acquisition
* Embedded System Debugging and Validation

---

## Future Enhancements

* External Temperature Sensor Integration
* EEPROM Data Storage
* SD Card Data Logging
* ESP32 Wi-Fi Connectivity
* IoT Cloud Dashboard
* Mobile Application Monitoring
* Long-Term Temperature Analytics

---

## Repository Contents

```text
├── Core/
├── Drivers/
├── MDK-ARM/
├── README.md
├── Internal_Temp.ioc
├── Project_Report.pdf
└── docs/
```

---

## Author

**Ashok**

Embedded Systems Engineer

### Technical Skills

* Embedded C
* STM32 Microcontrollers
* ARM Cortex-M Architecture
* UART, SPI, I2C Protocols
* ADC, DMA, Timers
* Real-Time Embedded Systems
* Automotive Embedded Systems

---

## License

This project is intended for educational and learning purposes.

If you found this project useful, feel free to star the repository.
