# 3-Digit Random Number Generator (Digital Lottery Machine)

## 📋 Introduction
This project was developed as part of the **2nd Year, 1st Semester Digital Electronics and Logic Circuit Laboratory (ECE 2104) Open Ended Project**[cite: 1]. 

The system is a hardware-based 3-digit random number generator (000–999) designed to function as a Digital Lottery Machine[cite: 1]. While software-based generators are common, this project focuses on the educational value of realizing such a system entirely through discrete digital ICs without any microcontroller[cite: 1]. It demonstrates core concepts of digital electronics including oscillators, counters, and display drivers in a compact, cost-effective implementation[cite: 1].

## ⚙️ How It Works
The circuit exploits the speed of digital electronics to achieve randomness through the following operation[cite: 1]:

*   **Clock Generation:** When the push-button is pressed, an **NE555 Timer** in astable mode generates a continuous square-wave clock pulse train[cite: 1].
*   **High-Frequency Oscillation:** The frequency is set by two 10 kΩ resistors and a 10 nF capacitor, producing a clock rate in the kilohertz range—far beyond human perception[cite: 1].
*   **Cascaded Counting:** 
    *   Clock pulses are fed into the first **CD4026 Decade Counter** (Units digit), which increments on each rising clock edge[cite: 1].
    *   Upon completing a cycle (0–9), the Units IC sends a carry pulse to the second CD4026 (Tens digit)[cite: 1].
    *   The second IC similarly clocks the third CD4026 (Hundreds digit)[cite: 1].
*   **Result Latching:** When the button is released, the clock signal is interrupted[cite: 1]. Each IC retains its last count, freezing the 7-segment displays on a pseudo-random number[cite: 1].

## 🛠️ Main Components
The project utilizes the following key hardware[cite: 1]:

| Component | Part No. / Value | Qty | Function in Circuit |
| :--- | :--- | :--- | :--- |
| **NE555 Timer IC** | NE555 | 1 | Astable oscillator; generates clock pulses[cite: 1] |
| **Decade Counter** | CD4026 | 3 | Counts 0-9 and directly drives 7-segment displays[cite: 1] |
| **7-Segment Display** | Common Cathode | 3 | Displays Units, Tens, and Hundreds digits[cite: 1] |
| **Push-Button** | SPST (NO) | 1 | User trigger; enables or freezes the clock[cite: 1] |
| **Resistors** | 10 kΩ, 1 kΩ | 3 | Sets timing frequency and limits current[cite: 1] |
| **Capacitors** | 0.01 µF | 2 | Main timing and noise decoupling[cite: 1] |

## 💻 Simulation & Validation
The complete circuit was designed and simulated in **Proteus Design Suite** to verify[cite: 1]:
*   Stable square-wave output from the NE555[cite: 1].
*   Correct decade counting and carry-chain propagation[cite: 1].
*   Instant latching behavior upon push-button release[cite: 1].

## 👥 Project Contributors
*   **Md. Baized Al Nur** (Roll: 2309033)[cite: 1]
*   **Debroop Ghosh Dostider** (Roll: 2309034)[cite: 1]

**Department of Electronics and Communication Engineering (ECE)**  
**Khulna University of Engineering & Technology (KUET)**[cite: 1]

## 📚 References
Refer to the file **"project proposal 33&34.pdf"** for full technical details, circuit diagrams, and datasheets[cite: 1].
