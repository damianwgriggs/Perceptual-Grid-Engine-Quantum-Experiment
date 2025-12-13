# Perceptual Grid Engine (PGE): Quantum Teleportation Protocol

> **Status:** Validated on IBM Quantum Hardware (`ibm_fez`)  
> **Fidelity:** 74.5% (Single Hop) | 71.9% (Round Trip)  
> **Stack:** Python, Qiskit SDK v1.0+, Qiskit Runtime (SamplerV2)

## 1. Overview
This repository contains the source code and experimental data for the **Perceptual Grid Engine (PGE)** adaptation for Quantum Hardware. The project demonstrates a robust "Grid Handoff" mechanism—technically known as Quantum Teleportation—that allows a quantum state to be transferred between qubits without traversing the physical space between them.

The core objective was to validate that data persistence can be maintained using **Dynamic Circuits** (real-time hardware feedback) on utility-scale quantum processors.

## 2. Architecture
The engine uses a "Bridge" qubit to entangle a "Dying" memory unit with a "Fresh" grid unit. It employs the following advanced primitives:

* **Dynamic Logic (`if_test`):** Uses real-time mid-circuit measurement to trigger hardware-level logic gates ($X$ and $Z$ corrections) within the coherence window.
* **Mid-Circuit Reset:** Wipes qubits clean during execution to allow for iterative reuse (demonstrated in the Round-Trip stress test).
* **Sampler V2:** Utilizes IBM's latest execution primitive for optimized probability distribution readout.

### The Protocols
1.  **Standard Grid Handoff:** Teleports state $q_0 \rightarrow q_2$.
2.  **Ping-Pong (Round Trip):** Teleports $q_0 \rightarrow q_2$, resets $q_0$, and teleports $q_2 \rightarrow q_0$ back.

## 3. Experimental Results
Experiments were conducted on **December 13, 2025**, targeting the **IBM Eagle Processor (`ibm_fez`)**, a 127-qubit superconducting quantum computer.

The target state was an "NBA Predictor" kernel initialized via $R_x(\frac{\pi}{3})$, creating a theoretical probability distribution of **75% $|0\rangle$ / 25% $|1\rangle$**.

| Test Protocol | Hardware Target | Circuit Depth | Measured Fidelity | Theoretical Max | Note |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Single Hop** | `ibm_fez` | 9 | **74.5%** | 75.0% | Near-perfect transmission. |
| **Round Trip** | `ibm_fez` | 15 | **71.9%** | 75.0% | Only 2.6% signal loss after 2 hops + reset. |

*Data validated via Qiskit Runtime Service Job IDs: `d4usfuuaec6c738rnb6g`, `d4usjvcgk3fc73auamsg`*

## 4. Repository Structure
* `PGE_Teleport_Engine.ipynb`: The main Jupyter Notebook containing the circuit logic, simulation setup, and IBM execution blocks.
* `requirements.txt`: List of dependencies (Qiskit, Qiskit-IBM-Runtime, etc.).

## 5. Quick Start
To run this code, you will need an IBM Quantum API Token.

1.  **Clone the Repo:**
    ```bash
    git clone [https://github.com/YOUR_USERNAME/perceptual-grid-engine.git](https://github.com/YOUR_USERNAME/perceptual-grid-engine.git)
    ```

2.  **Install Dependencies:**
    ```bash
    pip install qiskit qiskit-ibm-runtime qiskit-aer pylatexenc
    ```

3.  **Configure Credentials:**
    Open the notebook and locate the execution cell. Replace the placeholder with your key:
    ```python
    MY_IBM_KEY = "YOUR_IBM_API_KEY_HERE"
    ```
    *Note: Never commit your API key to GitHub.*

## 6. License
This project is open-source. Please attribute the "Perceptual Grid" architecture if adapting this logic for further persistence models.
