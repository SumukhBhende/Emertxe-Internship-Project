# 🧼 Washing Machine Simulation with PIC16F877A (Fan-Based)

This project simulates a washing machine using the **PIC16F877A microcontroller** in **PicsimLab**, replacing the motor with a **fan**. The system uses a **CLCD, keypad inputs, buzzer, and fan** to replicate washing cycles such as **program selection, water level, start/pause, door status, and completion**.

---

## 🧾 Features

* Power ON with key press
* Washing program selection
* Water level selection
* Start/Stop operation
* Fan ON for wash/spin simulation
* Door open detection (with buzzer alert)
* Completion message

---

## 🛠 Project Structure

```
├── clcd.c / clcd.h               # LCD interface code
├── digital_keypad.c / .h        # Keypad scanning (SW1-SW6)
├── timers.c / timers.h          # Timer0 config for delays/timing
├── isr.c                        # Timer0 interrupt handler
├── main.c / main.h              # Main washing logic (state machine)
├── README.md                    # This file
```

---

## 🧰 Requirements

| Tool         | Version          |
| ------------ | ---------------- |
| MPLAB X IDE  | v6.x or higher   |
| XC8 Compiler | v2.x or higher   |
| PicsimLab    | v1.3.1 or higher |

---

## 🔧 How to Build

### 1. **Setup in MPLAB X**

* Open MPLAB X IDE
* Create a new standalone **PIC16F877A project**
* Copy all `.c` and `.h` files into the project `Source` and `Header` directories
* Ensure your config bits are set correctly (or use MPLAB’s GUI)

  ```c
  #pragma config FOSC = HS      // High-Speed Oscillator
  #pragma config WDTE = OFF     // Watchdog Timer Enable (disabled)
  #pragma config PWRTE = OFF    // Power-up Timer Enable
  #pragma config BOREN = OFF    // Brown-out Reset Enable
  #pragma config LVP = OFF      // Low-Voltage Programming
  #pragma config CPD = OFF      // Data EEPROM Memory Code Protection
  #pragma config WRT = OFF      // Flash Program Memory Write Enable
  #pragma config CP = OFF       // Flash Program Memory Code Protection
  ```
* Set `__XTAL_FREQ` in `main.h` to match your clock (e.g., 20 MHz)

### 2. **Compile**

* Build the project (Shift + F11)
* Make sure no errors appear
* This will generate a `.hex` file in `dist/default/production/`

---

## 🧪 Simulation in PicsimLab

### 1. **Create Circuit**

Using **PICSimLab**, add these components:

| Component                  | Pin(s)                            | Notes               |
| -------------------------- | --------------------------------- | ------------------- |
| **CLCD**                   | PORTD (D0–D7), RC0 (RS), RC1 (EN) | LCD Display         |
| **Push Buttons (SW1–SW6)** | Connect to RB0–RB5 with pull-up   | User input          |
| **Buzzer**                 | RB0                               | Active HIGH         |
| **Fan (instead of Motor)** | RB1                               | Active HIGH for ON  |
| **Door Sensor**            | Connect to RB2                    | Pressed = door open |

⚠️ Set switches as **active low** and connect pull-up resistors.

### 2. **Load Hex**

* Click `MCU → Load Hex`
* Choose the HEX file from MPLAB build folder
* Start simulation

---

## 🖥️ Controls Mapping

| Function      | Switch           | Description                   |
| ------------- | ---------------- | ----------------------------- |
| Power ON      | SW5              | Starts simulation             |
| Scroll/Select | SW4 / long press | Navigates washing options     |
| Start         | SW5              | Starts washing                |
| Stop          | SW6              | Stops and returns             |
| Door Open     | SW1 (RB2)        | Triggers DOOR OPEN warning    |
| Fan ON        | RB1 output       | Simulates washing             |
| Buzzer        | RB0 output       | Rings if door open during run |

---

## ✅ Future Improvements

* EEPROM-based program memory
* Time estimation based on water level/program
* Real-time clock integration
* Temperature sensor for hot wash mode

---

## 📸 Screens in Simulation

* Power On screen
* Program selection
* Water level screen
* Start/Stop prompt
* Wash/Rinse/Spin with FAN ON
* Door Open alert with buzzer
* Program completion message

---

## 👨‍💻 Author

**Sumukh Bhende**
Electronics & Communication Engineering, NIT Goa
🚀 Simulation and Embedded Systems Enthusiast

