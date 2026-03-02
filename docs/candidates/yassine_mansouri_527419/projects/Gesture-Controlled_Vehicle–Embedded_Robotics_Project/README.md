# 🎮 Gesture-Controlled Vehicle — Embedded Robotics Project

A wireless mobile robot controlled in real time via a **PS4 DualShock controller** over Bluetooth. The system maps controller buttons and triggers to a full set of motion commands, including variable speed, differential steering, and pivot turns — all managed by an Arduino-based embedded architecture.

---

## ✨ Features

- **Wireless PS4 Bluetooth control** — no wires, real-time response
- **6 motion modes** — Forward, Reverse, Left, Right, and two special pivot turns per side
- **3-level speed control** — Low (120), Default (195), High (255) via L1/L2 triggers
- **2-level turn radius control** — tighter rotation via R1/R2 triggers
- **Differential motor logic** — independent PWM + direction control for each motor
- **Auto-reconnect** — automatically retries Bluetooth pairing if the controller disconnects

---

## 🗂️ Project Structure

```
├── version_with_ps4.ino   # Full Arduino source (Bluetooth + motor control)
└── README.md
```

---

## 🛠️ Technologies

| Layer | Stack |
|---|---|
| Embedded Controller | Arduino (C/C++) |
| Wireless Input | PS4 DualShock via Bluetooth (PS4Controller library) |
| Motor Control | PWM + DIR signals to dual motor driver |
| Communication | Serial (115200 baud, debug output) |

---

## ⚙️ Hardware Requirements

- ESP32-based Arduino board (required for Bluetooth PS4 pairing)
- PS4 DualShock 4 controller
- 2× DC motors + motor driver board (L298N or similar)
- Power supply for motors
- USB cable (for flashing)

---

## 🚀 Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/your-username/your-repo-name.git
cd your-repo-name
```

### 2. Install the PS4Controller library

In the Arduino IDE, go to **Sketch → Include Library → Manage Libraries** and search for `PS4Controller` by bluepad32 / Juan Neyra, then install it.

> ⚠️ This library requires an **ESP32** board. Make sure you have the ESP32 board package installed via the Boards Manager.

### 3. Pair your PS4 controller

Update the MAC address in the sketch to match your ESP32's Bluetooth address:

```cpp
PS4.begin("d4:8a:fc:cf:9c:72");  // Replace with your board's BT MAC address
```

You can find your ESP32's Bluetooth MAC using a small sketch that prints `ESP.getEfuseMac()`.

To pair the PS4 controller, hold **PS + Share** until the light bar flashes rapidly, then reset the ESP32.

### 4. Flash the Arduino

Open `version_with_ps4.ino` in the Arduino IDE, select your ESP32 board and port, and upload.

### 5. Power up and drive

Open the Serial Monitor at **115200 baud** to confirm connection, then use the controller.

---

## 🎮 Controls Reference

| Button / Combo | Action |
|---|---|
| **↑ (Up)** | Forward |
| **↓ (Down)** | Reverse |
| **← (Left)** | Turn Left |
| **→ (Right)** | Turn Right |
| **↑ + □ (Square)** | Gentle curve left (reduced inner wheel speed) |
| **↑ + ○ (Circle)** | Gentle curve right (reduced inner wheel speed) |
| **△ (Triangle)** | Pivot left (outer wheel only) |
| **✕ (Cross)** | Pivot right (outer wheel only) |
| **L1** | Low speed (120) |
| **L2** | High speed (255) |
| **R1** | Tighter turn ratio |
| **R2** | Even tighter turn ratio |
| *(no input)* | Stop |

---

## 🔧 Key Configuration Parameters

| Parameter | Default | Description |
|---|---|---|
| `defaultSpeed` | 195 | Normal driving PWM |
| `Speed1` | 120 | Slow speed (L1) |
| `Speed2` | 255 | Max speed (L2) |
| `defaultrot` | 2 | Default turn ratio divisor |
| `PWM` / `DIR` | Pins 2, 4 | Motor 1 control pins |
| `PWM1` / `DIR1` | Pins 19, 21 | Motor 2 control pins |

---

## 📄 License

This project is open-source. Feel free to use, modify, and distribute it with attribution.

---

## 🙋 Author

> *Yassine Mansouri
> https://y-mansouri.github.io/portfolio/*
