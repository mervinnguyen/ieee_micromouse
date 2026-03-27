# Micromouse : Institute of Electrical and Electronics Engineers
**Macro Rat** is an autonomous maze-solving robot implementing a FloodFill traversal algorithm on bare-metal embedded hardware. This repository documents the process undertaken by our IEEE team, covering firmware architecture, hardware bring-up, and algorithmic design.

---

# Overview
This repository captures the end-to-end development of a Micromouse platform built during Fall quarter (sophomore year) at UC Irvine under the IEEE student branch. The project involved designing a custom PCB, writing low-level firmware for an STM32 microcontroller, and implementing a real-time maze-solving algorithm. Documentation covers hardware integration, peripheral configuration, and software architecture, intended for engineers looking to understand the full system stack, not just the surface-level assembly.

---

# Hardware
- **STM32 MCU** — Core processing unit; handles sensor polling, motor control loops, and algorithm execution.
- **Custom PCB Chassis** — Rigid mounting platform with routed power and signal traces for all subsystems.
- **Mini DC Motors (×2)** — Differential drive configuration enabling forward motion and zero-radius turning.
- **7–9V Battery Pack** — Main power supply for the drive and logic subsystems.
- **7805 Linear Voltage Regulator** — Regulates battery input down to a stable 5V rail for digital logic.
- **H-Bridge Motor Driver** — Bidirectional motor control with PWM speed modulation.
- **Hall-Effect Rotary Encoders** — Quadrature feedback for closed-loop odometry and velocity estimation.
- **Infrared Distance Sensors (×2)** — Wall proximity detection used as primary inputs to the navigation state machine.

---

# Project Overview
Macro Rat is a ground-up embedded systems project targeting the core competencies of real-time control, sensor fusion, and autonomous decision-making. The robot executes a FloodFill algorithm to map and solve an unknown maze, dynamically updating its internal cell-cost representation as new wall data is acquired from the IR sensor array.

The firmware was developed in **STM32CubeIDE** and interfaces directly with hardware peripherals via HAL and low-level register access. Key engineering challenges included tuning PID loops for stable motor control, handling encoder debounce at speed, and managing real-time constraints.

The project also served as a platform for structured team collaboration, responsibilities were partitioned across firmware, hardware, and algorithm development, with integration milestones tracked across the full academic year. This mirrors real-world embedded development workflows and exposes contributors to the full V-model design cycle: from requirements through verification.

Contributions, forks, and improvements are welcome.

---

# Simulation
The FloodFill algorithm can be developed and validated in the [Micromouse Simulator](https://github.com/mackorone/mms) before deploying to hardware.

## Setup
1. Clone this repository
2. [Download the Micromouse simulator](https://github.com/mackorone/mms#download)
3. Run the simulator and click the **"+"** button to configure a new algorithm
4. Enter the following config:

| Field         | Value                        |
|---------------|-----------------------------------------|
| Name          | MacroRat                                |
| Directory     | `~ieee_micromouse\src\sourcecode`       |
| Build Command | `g++ Main.cpp API.cpp`                  |
| Run Command   | `~ieee_micromouse\src\sourcecode\a.exe` |

5. Click the **"Build"** button

6. Then, click the **"Run"** button

## Platform-Specific Notes

**Windows:**
- Download and install [MinGW](http://mingw.org/wiki/Getting_Started) if not already present
- Build command: `g++ Main.cpp API.cpp`
- Run command: `~ieee_micromouse\src\sourcecode\a.exe`

![Windows Config](https://github.com/mackorone/mms-cpp/blob/master/config-windows.png)

**Linux (Ubuntu):**
- Build command: `g++ Main.cpp API.cpp`
- Run command: `./MacroRat`

![Linux Config](https://github.com/mackorone/mms-cpp/blob/master/config-linux.png)

## Notes
- Communication with the simulator is done via **stdin/stdout** — use **stderr** for debug output
- All available API methods are documented at [mackorone/mms#mouse-api](https://github.com/mackorone/mms#mouse-api)

---

![Micromouse](docs/micromouse.jpg)
![Final Results](docs/FinalResult.png)
