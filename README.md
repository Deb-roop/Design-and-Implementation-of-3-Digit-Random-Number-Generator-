# 3-Digit Random Number Generator (Digital Lottery Machine + Counter )

This project was developed as part of the **2nd Year, 1st Semester Digital Electronics and Logic Circuit Laboratory (ECE 2104) Open Ended Project** at Khulna University of Engineering & Technology (KUET). 

The system is a hardware-based 3-digit random number generator (000–999) designed to function as a Digital Lottery Machine. While software-based generators are common, this project focuses on the educational value of realizing such a system entirely through discrete digital ICs without any microcontroller or programmable logic device. It demonstrates core concepts of digital electronics including oscillators, counters, carry-chain propagation, and display drivers in a compact, cost-effective implementation.

## 📋 Project Overview
This project demonstrates the implementation of a "Digital Lottery Machine" using only discrete hardware. It utilizes a high-speed clock and cascaded decade counters to generate and display a pseudo-random number when triggered by a user. Additionally, a dedicated secondary logic block tracks the total number of lottery attempts.

### Key Features
- **Microcontroller-Free:** Relies entirely on standard hardware logic ICs (Bipolar and CMOS).
- **Integrated Attempt Counter:** Includes a 4th standalone display stage dedicated entirely to counting total push-button operations.
- **Winner Alignment Logic:** Features a logic gate array (AND gates) designed to monitor and detect matching digits, accompanied by an LED/Buzzer output array for event signaling.
- **Instant Response:** Real-time clock-gating mechanism with no processing latency.
- **Educational Value:** Demonstrates core digital electronics challenges such as switch debouncing, propagation delays, and parasitic capacitance mitigation.

## ⚙️ How It Works
1. **Clock Generation:** An **NE555 Timer** is configured in **Astable Mode**, utilizing an $R_1 = 10\text{ k}\Omega$, $R_2 = 2.15\text{ k}\Omega$, and $C = 0.01\ \mu\text{F}$ network to produce a continuous, high-frequency square wave at approximately **$4.8\text{ kHz}$**. At 4,800 counts per second, the sequence advances far faster than human perception.
2. **User Trigger & Gating:** A mechanically linked dual push-button switch acts as a gate. When held down, clock pulses flow into the counter stages. Because the clock speed outpaces human reaction times by several orders of magnitude, the digit frozen at the moment of button release is entirely unpredictable.
3. **Counting & Cascading (The Random Number Chain):**
   - The gated clock drives the clock pin (Pin 1) of the first **CD4026 Decade Counter** (Units).
   - Upon completing a full 0–9 cycle, its *Carry Out* (Pin 5) sends a pulse to clock the second CD4026 (Tens).
   - The Tens stage similarly propagates its carry pulse to clock the third CD4026 (Hundreds).
4. **Push-Button Press Counter:** A secondary standalone **NE555** clock stage and a 4th **CD4026** counter are dedicated entirely to tracking how many times the lottery machine has been operated. This prevents the cumulative attempt metric from interfering with the random 3-digit generation.
5. **Target Logic Matching:** A **CD74HC11** Triple 3-Input AND Gate checks the state lines of the driver chain to determine matching conditions, combining with **74HC04 (Inverter)** and **74HC08 (AND)** logic to actuate a buzzer and alert LED when specific conditions are met.

## 🛠️ Components List
| Component | Part No. / Value | Qty | Function |
| :--- | :--- | :--- | :--- |
| **Timer IC** | NE555 | 2 | 1× primary high-frequency oscillator ($4.8\text{ kHz}$); 1× slower attempt clock pulse generator |
| **Decade Counter / Driver** | CD4026 | 4 | 3× cascaded for 3-digit random number generation; 1× for the total attempt counter |
| **7-Segment Display** | Common Cathode | 4 | 3× digits for lottery output (000–999); 1× digit for total press counter display |
| **Triple 3-Input AND Gate** | CD74HC11 | 1 | Evaluates digit matching states across the counter stages |
| **Hex Inverter** | 74HC04 | 1 | Inverts push-button logic transitions for gating blocks |
| **2-Input AND Gate** | 74HC08 / 74LS08 | 1 | Combines push-button input with alignment logic to enable the indicator circuit |
| **Push-Button Switch** | SPST (NO) | 2 | Mechanically linked with a shared plate to act as a single simultaneous trigger |
| **Current-Limiting Resistors** | $220\ \Omega$ | 28 | Placed inline on *every* single segment line to protect displays from overvoltage |
| **Timing Resistors** | $10\text{ k}\Omega$ | 5 | Establishes the stable RC time constraints for the NE555 networks |
| **Main Timing Capacitors** | $0.01\ \mu\text{F}$ | 3 | Used for oscillator frequency tuning networks |
| **Decoupling Capacitor** | $47\ \mu\text{F}$ | 1 | Positioned across power rails to suppress voltage spikes and noise |
| **Output Devices** | Active Buzzer & LED | 1 ea | Provides auditory and visual alerts during logic trigger events |
| **Prototyping Platform** | Breadboards | 3 sets | Physical framework for the IC array assembly |

## 🛠️ Hardware Challenges & Troubleshooting Insights
Moving from ideal simulation to physical breadboards revealed several real-world engineering constraints that were systematically resolved:
- **Display Overcurrent Protection:** Initial testing without inline restriction led to an overvoltage failure on a 7-segment display block. The issue was fully corrected by integrating $220\ \Omega$ resistors on all 28 active segment lines, stabilizing brightness and protecting the CMOS drivers.
- **Frequency Calibration:** The initial clock configuration yielded roughly $500\text{ Hz}$, creating a visible scrolling effect that compromised pseudo-randomness. Decreasing the timing network resistances to $10\text{ k}\Omega$ escalated the frequency to **$4.8\text{ kHz}$**, rendering the sequence a blur and ensuring un-biasable results.
- **Mechanical Switch Debouncing:** Contact bouncing on the momentary switches injected spurious clock cycles, causing digit skipping on release. A hardware capacitor filter was placed across the switch terminals to smooth out mechanical transients.
- **Parasitic Capacitance & Signal Drift:** Long jumper wire arrays introduced stray capacitance not modeled in Proteus, resulting in slight rounding on the square-wave edges. Multimeter continuity verification and structured color-coding of the 28-wire segment grid ensured logic thresholds remained valid across all 3 breadboards.

## 💻 Simulation
The complete logic diagram and propagation paths were modeled and verified using **Proteus Design Suite**. This simulation validated:
- Stable $4.8\text{ kHz}$ output from the primary oscillator stage.
- Perfect sequential logic cascading through the CD4026 carry lines without missing counts.
- Zero-latency digit freezing upon simulated button open-states.

## 👥 Authors
- **Md. Baized Al Nur** (Roll: 2309033)
- **Debroop Ghosh Dostider** (Roll: 2309034)

**Department of Electronics and Communication Engineering (ECE)** **Khulna University of Engineering & Technology (KUET)**

## 📚 References
- Texas Instruments, "NE555 Precision Timer Datasheet."
- Texas Instruments, "CD4026B CMOS Decade Counter Datasheet."
- M. Morris Mano, "Digital Design" (5th Edition).
- Thomas L. Floyd, "Digital Fundamentals" (11th Edition).
