


# AnesthesiaAutomator: Open-Source Closed-Loop TCI Simulator

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.XXXXXXX.svg)](https://doi.org/10.5281/zenodo.XXXXXXX) **AnesthesiaAutomator** is a Python-based educational simulator designed to model Target-Controlled Infusion (TCI), pharmacokinetic/pharmacodynamic (PK/PD) curves, and closed-loop autonomic feedback systems in modern anesthesiology. 

This tool is designed for medical students, anesthesia residents, and computational neuroscience researchers to visualize how AI-driven closed-loop systems handle nociceptive stimuli, motion artifacts, and physiological decay in real-time.

> **Disclaimer:** This software is strictly an **educational and computational model**. It is not a certified medical device and must never be used for clinical decision-making or actual patient care.

---

## 🧠 Key Features

1. **Synthetic Patient Generator:** Simulates biometric drift and injects clinical events (surgical incision, motion artifacts, hemodynamic collapse, hypothermia).
2. **4-Phase Algorithmic Controller:** An automated "Brain" that processes multi-parameter sensor arrays to adjust drug delivery.
3. **PK/PD Mathematical Modeling:**
   * **Pharmacokinetics:** Utilizes a simplified 1-compartment model with an effect-site delay ($k_{e0}$) based on the Schnider model for Lean Body Mass (LBM).
   * **Pharmacodynamics:** Implements the Sigmoidal Emax (Hill) Equation to map effect-site concentration ($C_e$) to EEG depth (BIS).
4. **Autonomic Nociceptive Feedback:** Uses Heart Rate Variability (HRV/RMSSD) drops as a proxy for sympathetic pain drive to trigger algorithmic boluses.
5. **Real-Time Dashboard:** A live Matplotlib GUI displaying twin-axis plots for drug concentration, brain suppression (BIS), and automated pump output.

---

## ⚙️ The 4-Phase Logic Architecture

The `master_controller` evaluates patient state every second using the following hierarchical logic:

* **Phase 1: Critical Safety Veto:** Hard stops the infusion (0.0 mL/hr) if critical thresholds are breached (MAP < 55, SpO2 < 88%, EtCO2 < 20).
* **Phase 2: Artifact & Motion Check:** Monitors accelerometer data against the Train-of-Four (TOF) count. Distinguishes between surgical table bumps (TOF=0) and patient bucking (TOF>0), holding the infusion rate steady to prevent artifact-induced overdose.
* **Phase 3: Context Modifiers:** Adjusts baseline maintenance dosing continuously based on hypothermia (reduces dose by 7% per °C drop) and hypovolemia (CVP/PCWP).
* **Phase 4: Active Dosing Control:** Checks autonomic pain proxies (HRV) first. If stable, it maintains depth via EEG/BIS targeting (+20% for light anesthesia, -30% for deep).

---

## 🚀 Installation & Usage

### Prerequisites
You need Python 3.7+ and the following libraries:
```bash
pip install matplotlib ipython
````

### Running the Simulator

Simply clone the repository and run the Python script. The simulation is time-scaled (15x) for rapid educational visualization.

```bash
git clone [https://github.com/YourUsername/Anesthesia-TCI-Simulator.git](https://github.com/YourUsername/Anesthesia-TCI-Simulator.git)
cd Anesthesia-TCI-Simulator
python anesthesia_simulator.py
```

-----

## 📊 Visualizing the Output

When running, the simulator generates a dynamic 3-panel dashboard:

1.  **Pharmacokinetics:** Tracks Plasma ($C_p$) vs. Brain Effect-Site ($C_e$) concentrations in $\mu g/mL$.
2.  **Pharmacodynamics:** Tracks the resultant EEG suppression (BIS target 40-60).
3.  **AI Dosing Output:** Tracks the real-time adjustments made by the algorithmic controller in $mL/hr$.

-----

## 📝 Citation

If you use this code in your research or educational materials, please cite the software using the Zenodo DOI:

> [Your Name]. (2026). *AnesthesiaAutomator: A Python-Based Simulator for Target-Controlled Infusion and Closed-Loop Anesthesia Dynamics*. Zenodo. https://www.google.com/url?sa=E\&source=gmail\&q=https://doi.org/10.5281/zenodo.XXXXXXX

-----

## ⚖️ License

This project is licensed under the **MIT License** - see the [LICENSE](https://www.google.com/search?q=LICENSE) file for details. You are free to use, modify, and distribute this software for academic, commercial, or personal use, provided the original copyright is included.

