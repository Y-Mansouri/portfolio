# 🤖 Autonomous Mobile Robot — Computer Vision + LiDAR Navigation

An autonomous mobile robot that integrates real-time computer vision and LiDAR-based obstacle avoidance. A Python AI module communicates over serial with an Arduino embedded controller to drive four independently actuated wheels and navigate dynamic environments.

---

## ✨ Features

- **Color-based object tracking** using OpenCV HSV filtering and contour detection
- **LiDAR obstacle avoidance** with configurable distance threshold and avoidance angle
- **4-wheel actuation** — each wheel driven by a DC motor + stepper motor pair controlled via Arduino
- **Real-time dashboard** built with Tkinter + Matplotlib showing live camera feed and LiDAR scan
- **Serial communication** between Python (host) and Arduino (embedded controller) at 9600 baud
- **Multi-threaded architecture** — video processing, LiDAR scanning, and GUI run in parallel

---

## 🗂️ Project Structure

```
├── main_combine_lidar_camera.py   # Python AI module (vision + LiDAR + GUI)
├── code_for_4_wheels.ino          # Arduino embedded controller (motor actuation)
└── README.md
```

---

## 🛠️ Technologies

| Layer | Stack |
|---|---|
| AI / Vision | Python, OpenCV, NumPy |
| LiDAR | RPLidar library |
| GUI | Tkinter, Matplotlib |
| Embedded | Arduino (C/C++) |
| Communication | Serial (PySerial) |

---

## ⚙️ Hardware Requirements

- Arduino Mega (or compatible board with enough digital pins)
- RPLidar A-series sensor
- USB camera / webcam
- 4× DC motors + 4× stepper motors (with DRV8825 or A4988 drivers)
- Motor driver boards (PWM-capable)
- Power supply suitable for motors

---

## 🚀 Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/your-username/your-repo-name.git
cd your-repo-name
```

### 2. Install Python dependencies

```bash
pip install opencv-python numpy pyserial rplidar-roboticia matplotlib
```

### 3. Flash the Arduino

Open `code_for_4_wheels.ino` in the Arduino IDE and upload it to your board.

### 4. Configure serial port

In `main_combine_lidar_camera.py`, update the serial port to match your system:

```python
serialInst.port = "COM6"   # Windows example
# serialInst.port = "/dev/ttyUSB0"  # Linux example
```

Also verify the LiDAR port if needed.

### 5. Run the Python module

```bash
python main_combine_lidar_camera.py
```

---

## 🎮 How It Works

1. The camera captures frames and converts them to HSV color space to detect a target object by color.
2. The centroid of the detected contour is mapped to a steering angle (`-40°` to `+40°`).
3. The RPLidar continuously scans for obstacles. If an object is detected within `OBSTACLE_DISTANCE_THRESHOLD` (default: 850 mm), the robot triggers an avoidance maneuver.
4. Navigation commands (angle + PWM) are sent over serial to the Arduino, which translates them into individual motor signals for each of the four wheels.
5. A Tkinter GUI displays the live camera feed, mask overlay, and a polar LiDAR map in real time.

---

## 🔧 Key Configuration Parameters

| Parameter | Default | Description |
|---|---|---|
| `OBSTACLE_DISTANCE_THRESHOLD` | 850 mm | Minimum safe distance from obstacle |
| `AVOIDANCE_ANGLE` | 35° | Steering angle applied during avoidance |
| `PWM` | 190 | Base motor speed |
| `AVOIDANCE_PWM` | 190 | Motor speed during avoidance |
| `low` / `high` | HSV (32,50,61) – (90,255,255) | Target color range (green) |

---

## 📡 Serial Communication Protocol

Commands are sent as ASCII strings from Python to Arduino:

```
<angle>,<pwm>,<state>,<elevate>
```

The Arduino parses these values and drives the four motor pairs accordingly.

---

## 📄 License

This project is open-source. Feel free to use, modify, and distribute it with attribution.

---

## 🙋 Author

> *Yassine Mansouri
> https://y-mansouri.github.io/portfolio/*
