# 60W GaN-Based Synchronous Buck Converter for Avionics Systems

![Altium 3D Render]([BURAYA ALTIUM 3D RENDER GÖRSELİNİN LİNKİNİ EKLE])

## 📌 Project Overview
This project is a high-frequency, GaN (Gallium Nitride) based synchronous buck converter hardware designed for critical loads in avionics systems, such as mission computers and telemetry modules. Unlike traditional Si-MOSFET designs, it utilizes EPC2218 GaN FETs and the LTC7891 controller to minimize switching losses and achieve fanless cooling.

### ⚙️ System Specifications
* **Input Voltage (Vin):** 18V - 36V DC (Avionics Battery Standard)
* **Output Voltage (Vout):** 12V DC (Fixed)
* **Maximum Output Current (Iout):** 5A
* **Maximum Power:** 60W
* **Switching Frequency (Fsw):** 500 kHz
* **Peak Efficiency:** 95.8% (At Full Load)
* **Control Topology:** Peak Current Mode Control (LTC7891)

---

## 🔬 Hardware Design Highlights

### 1. Signal Integrity and EMI Management (4-Layer Stack-Up)
To suppress EMI radiation caused by the high $dv/dt$ switching speeds (100V/ns) of GaN FETs, an IPC-standard 4-layer PCB architecture was implemented. 
* **Layer 2 (GND Plane):** An uninterrupted Ground plane is placed directly beneath the high $di/dt$ loops on Layer 1, providing the shortest return path and mitigating electromagnetic emissions.
* **Via Shielding:** Analog signal traces are surrounded by GND via stitching to create a Faraday Cage effect.

### 2. Precision Current Sensing (Kelvin Sensing)
The $R_{SENSE}$ current feedback, critical for system stability, is achieved using a "Differential Kelvin Connection" routed from the inner side of the resistor pads. To prevent the sense traces from being affected by the power plane on Layer 3, a "Polygon Cutout" method was applied to maximize noise isolation.

### 3. Multi-Layer Avionics Protection Stage
* **Reverse Polarity Protection:** To eliminate conduction losses, a P-Channel MOSFET (Vishay SQJ459EP) with low $R_{DS(on)}$ is used instead of a traditional diode.
* **Transient Voltage (Surge) Protection:** An SMAJ40A-HT TVS diode with a 40V stand-off voltage is utilized to clamp sudden voltage spikes on the input line.

---

## 📊 Simulation and Validation (LTSpice Results)

Prior to physical manufacturing, the system was subjected to dynamic stress tests in the LTSpice environment:

1. **Start-Up Response:** Thanks to the 100nF Soft-Start capacitor, the system reaches a stable 12V within 7 ms without any overshoot.
   *(See: /Measurements/Startup_Graph.png)* ![Start-Up]([BURAYA START-UP GRAFİĞİNİ EKLE])

2. **Load Transient Response:** During sudden load steps from 0.5A to 5A (10% -> 100%), voltage fluctuation is limited to 2.2% (254mV), and the controller restores regulation within 150 µs.
   *(See: /Measurements/Transient_Graph.png)* ![Transient]([BURAYA TRANSIENT GRAFİĞİNİ EKLE])

3. **Voltage Ripple:** With 500 kHz switching and a low-ESR ceramic hybrid capacitor array, the output ripple at full load (5A) is reduced to **<10mV**.

---

## 📁 Repository Structure

* `\Hardware_Source`: Altium Designer project files (.PrjPcb, .SchDoc, .PcbDoc).
* `\Simulation`: LTSpice validation files and analysis graphs.
* `\Manufacturing`: Production-ready Gerber, NC Drill files, and Industrial BOM list.
* `\Docs`: Detailed datasheets for GaN FET and LTC7891.
