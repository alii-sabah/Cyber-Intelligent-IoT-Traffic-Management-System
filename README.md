# Cyber-Intelligent IoT Traffic Management System

A secure, autonomous, and adaptive traffic control framework powered by **Ant Colony Optimization (ACO)** and secured with robust cryptographic protocols. This project integrates an **ESP32 IoT hardware layer**, a **Flask backend server**, and a **live web dashboard** to dynamically optimize traffic flow while mitigating cyber threats.

---

## 🛠️ System Architecture

The system operates as a closed-loop cyber-physical framework split into three distinct layers:
1. **Edge Hardware Layer (ESP32):** Reads high-density IR sensor matrices across 4 lanes (North, East, South, West), compiles raw system states into JSON payloads, encrypts them, and transmits secure HTTP POST requests to the central node.
2. **Central Logic & Optimization Layer (Flask Server):** Decrypts data packets, runs a real-time ACO decision engine, maintains a strict State Machine to manage transitions, and dynamically evaluates safe traffic light timings.
3. **Monitoring Layer (Web Dashboard):** A dark-themed web panel rendering live lane states, heuristic distributions, pheromone configurations, and security system logs.

---

## 🐜 Intelligent Optimization (ACO Logic)

Instead of rigid static timers, traffic lane activation probability is determined dynamically using an algorithmic model derived from natural ant foraging behavior. The probability ($Prob_i$) for each lane $i$ is calculated using the following mathematical logic:

$$Prob_i = \frac{(\tau_i^{\alpha}) \times (\eta_i^{\beta})}{\sum_{j=1}^{4} (\tau_j^{\alpha}) \times (\eta_j^{\beta})}$$

Where:
*   $\tau_i$: **Pheromone Level** (Cumulated historic demand/congestion data on Lane $i$).
*   $\eta_i$: **Heuristic Value** (Immediate current vision: Calculated from real-time vehicle density + lane waiting timers).
*   $\alpha = 1.0$: Weight parameter prioritizing historical traffic memory.
*   $\beta = 2.0$: Weight parameter prioritizing active, immediate congestion patterns.

### Safety-First State Machine
To guarantee smooth transitions and absolute physical safety:
*   **Verification Consistency Counter:** The system enforces a verification window; an alternative lane must consistently demonstrate priority for several cycles before triggering a phase change.
*   **Intermediate Yellow/Clearance Phases:** Includes specialized transitions to clear intersection zones, mitigating erratic lane switching or sudden collisions.

---

## 🔐 Cyber Security Framework

Designed with an emphasis on defensive computing to protect critical city infrastructure against data injection and spoofing:
*   **End-to-End Encryption:** All operational payloads transmitted from edge nodes are encrypted using **AES-128-CBC** with explicit padding validation routines.
*   **API Authentication:** Strict validation of proprietary server-side API tokens via custom headers prior to processing requests.
*   **Active HoneyPot Trap:** Includes an integrated deceptive gateway route (`/admin_login`). Any unauthorized bot scanning or traversing this route triggers an immediate system alert, automatically blacklisting the source IP address from server interactions.

---

## 💻 Tech Stack & Hardware Specifications

### Software & Algorithms
*   **Backend Framework:** Python / Flask
*   **Security & Encryption:** PyCryptodome (AES-128), Custom HoneyPot Architecture
*   **Algorithms:** Meta-Heuristic Ant Colony Optimization (ACO), Hysteresis Logic, Deterministic State Machines
*   **Frontend Interface:** HTML5, CSS3 (Modern Glossy Dark UI), Vanilla JavaScript (Asynchronous Pollers)

### Hardware Implementation
*   **Microcontroller:** ESP32 NodeMCU Development Module
*   **Sensors:** Infrared (IR) Obstacle Sensor Matrix mapping three logical positions per lane: *Entry, Mid, and Stop*.
*   **Actuators:** High-Visibility LED Traffic Signal Array managed via optimized GPIO configurations.
*   **System Integrity:** Hardware Watchdog Timer (WDT) loops configured to self-recover and restart edge logic automatically if communication drops.

---

## 📜 Repository Status
> **Notice:** The full source code for this proprietary framework (including core `aco_logic.py`, `app.py`, firmware binaries, and UI packages) is maintained in a **private enterprise repository** to protect proprietary logic and prevent structural system vulnerabilities. This documentation serves as a conceptual and architectural portfolio display.
