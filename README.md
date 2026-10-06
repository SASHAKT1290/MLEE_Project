# Boost Converter Symbolic Regression & Governing Equation Discovery

Data-driven discovery of governing nonlinear equations for a DC-DC Boost Converter comparing **SINDy** (Sparse Identification of Nonlinear Dynamics) and **PySR** (Symbolic Regression via Genetic Algorithms).

---

## 🎯 Project Goals & Scope
- **Equation Discovery:** Recover governing differential equations for inductor current ($i_L$) and output capacitor voltage ($v_C$) directly from switching waveforms.
- **Method Comparison:** Benchmark SINDy (fixed function library sparse regression) against PySR (free-form genetic algorithm symbolic regression).
- **Robustness Analysis:** Perform systematic noise sweeps ($0\%$, $1\%$, $3\%$, $10\%$) and evaluate derivative estimation methods under noisy measurement conditions.

---

## ⚡ Circuit Operating Parameters
Baseline steady-state simulation settings generated via LTspice:

| Parameter | Symbol | Value |
| :--- | :--- | :--- |
| Input Voltage | $V_{in}$ | $12\text{ V}$ |
| Duty Cycle | $D$ | $0.5$ |
| Switching Frequency | $f_{sw}$ | $100\text{ kHz}$ |
| Inductance | $L$ | $100\ \mu\text{H}$ ($R_{ser} = 0.05\ \Omega$) |
| Capacitance | $C$ | $47\ \mu\text{F}$ ($R_{ser} = 0.05\ \Omega$) |
| Load Resistance | $R_{load}$ | $24\ \Omega$ |
| Sampling Rate | $f_s$ | $1\text{ MHz}$ ($1\ \mu\text{s}$ interval) |
| Steady-State Window | $t$ | $15\text{ ms} \to 20\text{ ms}$ (5,000 points) |

---

## 📊 Dataset Specification (`data/boost_clean.csv`)
Clean steady-state baseline dataset without noise or startup transient:

* `t`: Time ($0.015\text{ s} \to 0.020\text{ s}$, uniform $1\ \mu\text{s}$ spacing)
* `iL`: Inductor current in Amperes ($\text{mean} \approx 2.0\text{ A}$, ripple $\approx 1.7\text{ A} \to 2.3\text{ A}$)
* `vC`: Capacitor voltage in Volts ($\text{mean} \approx 23.0\text{ V}$, ripple $\approx 0.1\text{ V}_{p-p}$)
* `switch_state`: Switch gate state ($1 = \text{ON}$, $0 = \text{OFF}$, mean $\approx 0.5$)

---

## 📁 Repository Structure
```text
boost-sr/
├── README.md
├── .gitignore
├── sim/
│   └── boost.cir                # LTspice netlist for waveform generation
├── data/
│   └── boost_clean.csv          # Clean steady-state waveform dataset
└── notebooks/
    └── 01_export_and_sanity_check.ipynb  # Data verification & preprocessing notebook
```