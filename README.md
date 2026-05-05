# 3-Digit Random Number Generator (Digital Lottery Machine)

A microcontroller-free, hardware-based 3-digit random number generator (000–999) designed and implemented using discrete digital ICs. This project was developed for the **Digital Electronics and Logic Circuits Laboratory (ECE 2104)** at **Khulna University of Engineering & Technology (KUET)**.

## 📋 Project Overview
This project demonstrates the implementation of a "Digital Lottery Machine" without the use of microcontrollers or software programming. It utilizes a high-speed clock and cascaded decade counters to generate and display a pseudo-random number when triggered by a user.

### Key Features
- **Microcontroller-Free:** Relies entirely on CMOS and bipolar ICs.
- **Instant Response:** Real-time clock-gating mechanism with no processing latency.
- **Scalability:** The design can be easily extended to more digits by cascading additional counter stages.
- **Educational Value:** Demonstrates core digital electronics concepts: astable oscillators, carry-chain propagation, and 7-segment display driving.

## ⚙️ How It Works
1.  **Clock Generation:** An **NE555 Timer** is configured in **Astable Mode**, producing a continuous high-frequency square-wave clock pulse (in the kilohertz range).
2.  **User Trigger:** A momentary push-button acts as a gate. While pressed, the clock pulses flow to the counter stages.
3.  **Counting & Cascading:** - The clock drives the first **CD4026 Decade Counter** (Units).
    - When the Units digit completes a cycle (0-9), its *Carry Out* pin clocks the second CD4026 (Tens).
    - The second IC similarly clocks the third CD4026 (Hundreds).
4.  **Freezing the Count:** Upon releasing the button, the clock path is interrupted. The counters freeze instantly on their current state, displaying a random 3-digit number (000-999). Because the clock is faster than human reaction time, the result is effectively unpredictable.

## 🛠️ Components List
| Component | Part No. / Value | Qty | Function |
| :--- | :--- | :--- | :--- |
| Timer IC | NE555 | 1 | Generates high-frequency clock pulses |
| Decade Counter | CD4026 | 3 | Counts 0-9 and drives 7-segment displays |
| 7-Seg Display | Common Cathode | 3 | Displays the 3-digit output |
| Push-Button | SPST (NO) | 1 | Enables/Freezes the clock signal |
| Resistors | 10 kΩ, 1 kΩ | 3 | Sets timing (10k) and limits current (1k) |
| Capacitors | 0.01 µF (103) | 1 | Main timing capacitor |
| Capacitors | 0.01 µF (200) | 1 | Noise decoupling on Pin 5 |

## 💻 Simulation
The circuit design and logic were validated using **Proteus Design Suite**. Verification included:
- Stability of the NE555 square-wave output.
- Accurate carry-chain propagation across cascaded stages.
- Instant latching/freezing behavior upon button release.

## 👥 Authors
- **Md. Baized Al Nur** (Roll: 2309033)
- **Debroop Ghosh Dostider** (Roll: 2309034)

**Department of Electronics and Communication Engineering (ECE)** **Khulna University of Engineering & Technology (KUET)**

## 📚 References
- Texas Instruments, "NE555 Precision Timer Datasheet."
- Texas Instruments, "CD4026B CMOS Decade Counter Datasheet."
- M. Morris Mano, "Digital Design" (5th Edition).
- Thomas L. Floyd, "Digital Fundamentals" (11th Edition).
