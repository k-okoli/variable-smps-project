# ⚡ Variable Benchtop Power Supply (SMPS + Wireless Control)

A collaborative electronics project to design and build a **mains-powered variable benchtop power supply** using a **flyback switch-mode power supply (SMPS) topology**. Unlike traditional linear supplies, this design emphasizes efficiency, compactness, and the learning opportunities of modern power electronics.  

We’re also integrating **Bluetooth (and possibly Wi-Fi)** for wireless monitoring and control, making this supply not just a lab tool but a connected device.

---

## ✨ Key Features
- **Output Power**: Up to **45 W** (15 V, 3 A max)  
- **Modes**: Constant Voltage (CV) and Constant Current (CC).
- **Protecton**: Over Voltage Protection (OVP), Over Current Protection (OCP), Thermal Protection
- **Outputs**:  
  - Main: Standard 4 mm banana plug terminals  
  - Auxiliary: USB-A and USB-C ports (independent of main supply)  
  - **USB-C PD support** (if feasible, via dedicated PD controller IC)  
- **Wireless Control**:  
  - Bluetooth (baseline) for remote monitoring and adjustment  
  - Possible Wi-Fi integration for extended features (logging, web UI)  
- **User Interface**:  
  - Display for voltage/current readouts  
  - Rotary encoders for intuitive control  
  - Wireless app/PC interface (future scope)  
- **Enclosure**: TBD (custom 3D-printed front panel or off-the-shelf instrument case)

---

## 🛠️ Tools & Components
- **Circuit Design**: [KiCad](https://www.kicad.org/) (open-source EDA)  
- **Topology**: Flyback SMPS (isolated, compact, efficient)  
- **Controller MCU**: STM32 (primary candidate)  
  - Alternatives: ESP32 (if Wi-Fi is prioritized)  
- **USB-C PD**: Dedicated PD controller IC (e.g., STUSB4500)  
- **Firmware**: C/C++ with STM32 HAL or FreeRTOS (depending on complexity)  

---

## 📅 Project Roadmap
**Month 1**  
- Research + schematic design (flyback topology, USB PD feasibility, wireless module selection)  
- Set up GitHub repo, task board, and documentation workflow  

**Month 2**  
- First PCB prototype (SMPS core + CV/CC control)  
- Firmware skeleton (basic UI + wireless comms)  

**Month 3**  
- Refined prototype with USB outputs + enclosure design  
- Wireless integration (Bluetooth baseline, Wi-Fi optional)  

**Month 4**  
- Testing, debugging, and validation (CV/CC transitions, load testing)  
- Final enclosure + polish  
- Documentation + public release  

---

## 🔬 Development Practices
- **Version Control**: GitHub for schematics, firmware, and docs  
- **Task Management**: GitHub Projects / Notion for milestones  
- **Simulation**: SPICE models for SMPS stability before prototyping  
- **Testing**:  
  - Low-voltage isolated tests first  
  - Load testing with electronic loads/resistors  
  - Oscilloscope validation of CV/CC transitions  

---

## 📲 Wireless Control
- **Bluetooth**:  
  - Mobile/desktop app for setting voltage/current limits  
  - Real-time monitoring of output values  
- **Wi-Fi (optional)**:  
  - Web dashboard for remote access  
  - Data logging to cloud/local server  

---

## 🎥 Content & Documentation
We’re documenting the journey for **students, hobbyists, and professionals**

---

## 👥 Team & Collaboration
This is a **two-person collaborative build**, with roles split between:  
- **Power electronics & hardware design**  
- **Firmware, UI, and wireless integration**  

We overlap on integration, testing, and content creation.

---

## 🚧 Status
Currently in **early design phase**:  
- Flyback topology under evaluation  
- Controller MCU selection (STM32 vs ESP32)  
- Wireless module feasibility study  

---

## 📢 Get Involved
We welcome feedback, suggestions, and collaboration ideas!  
Follow our progress on social media, or contribute via GitHub issues and discussions.  