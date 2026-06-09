# 🛰️ Project HydroTech: Ultra-Low-Cost Inline Fluid Spectrometer
> Open-Source Bare-Metal Fluid Analytics Terminal by RikMakersHub

An ultra-low-cost (~$4.50 / ₹350), standalone optical spectrometry system engineered to detect liquid contamination, fluid density shifts, or chemical transmission profiles natively without custom laboratory hardware or cloud configurations.

---

## 💡 The Problem: High-Cost Fluid Auditing
Checking the purity of liquids or identifying structural anomalies in different fluid layers is highly restricted by economic constraints. Commercial multi-wavelength spectrometers are expensive, delicate, and often require constant cloud connectivity or enterprise software licenses to process simple metrics. 

**HydroTech** strips down the engineering to bare-metal principles: leveraging structured chromatic wavelength paths inside a light-tight pipeline enclosure to run immediate, local fluid diagnostic thresholds on a dirt-cheap microcontroller, managed by a lightweight, responsive web terminal interface.

---

## 📊 Value Engineering // BOM (~₹270 Actual)

| Component | Selection | Cost (INR) | Operational Purpose |
| :--- | :--- | :--- | :--- |
| **MCU Core** | Arduino Pro Mini 3.3V / ATmega328P | ₹180 | Runs spectrum processing matrices. |
| **Receiver** | LDR Photoresistor (5mm) | ₹30 | Measures dynamic analog voltage drops. |
| **Optics** | High-Intensity RGB LED Array | ₹15 | Flashes sequential R-G-B light vectors. |
| **Storage** | Premium Clear Glass Tube | ₹20 | Isolates target fluids without interference. |
| **Enclosure** | 1" PVC Pipeline T-Joint Coupling | ₹25 | Nullifies environmental ambient lux leaks. |

---

## 🔋 Deep-Sleep Power Optimization (SMD Hardware Hack)
Standard off-the-shelf Arduino Pro Mini development boards feature an integrated surface-mounted (SMD) power indicator LED coupled with a current-limiting resistor directly tied across the VCC and GND rails. 

### The Technical Issue
While this indicator is convenient for bench prototyping, it introduces a permanent, un-routable **3mA to 5mA constant phantom current drain**. Even if you write flawless low-power sleep firmware using internal watchdog timers, you cannot disable this trace via software because it is physically hardwired directly to the power rail. For a long-term field installation running on standard AA cells or a small Li-ion battery, this single passive LED will drain your power source in just a few days.

### The Solution (Hardware Interception)
To force the ATmega328P processor down to its true low-power limits, you must physically break this indicator circuit:
1. Locate the tiny red onboard SMD power LED (usually placed right next to the integrated voltage regulator).
2. Using a clean, fine-tipped soldering iron or a sharp precision tool, apply a localized blast of heat or careful leverage to clean-flick the component right off its PCB pads.
3. Be highly cautious during this process to avoid sliding your iron into the adjacent board reset button trace or bridging nearby data pins with stray solder blobs.

### The Payoff
By cleanly isolating the board from this single redundant indicator element, you wipe out the phantom current load. This drops your total deep-sleep baseline current floor from milliamps down to an ultra-low **under-20 microamps (µA)** spectrum. This hardware hack effectively extends your standalone field deployment lifespan from a couple of days to several months or even a year on a single cell.

---

## 🛠️ Field Assembly & Calibration Guide
1. **Chassis Modification:** Take a standard 1" PVC T-joint pipeline coupling. Coat the entire interior cavity with matte-black surface shielding to ensure external environmental lux readings remain at zero.
2. **Optical Element Alignment:** Mount the high-intensity RGB LED array directly inside one straight end of the T-joint, and the 5mm LDR photoresistor on the exact opposite side. Secure them with hot glue to form a direct, parallel light-beam axis.
3. **Fluid Path Integration:** Insert a clear glass test tube down through the top perpendicular opening of the PVC T-joint, intercepting the path between the LED and the LDR.
4. **Calibration Protocol:** Upload the production firmware, open the Serial Monitor, and log the initial raw base vectors for clean water (`rSum`, `gSum`, `bSum`). Any fluid sample tested later that skews lower than these values indicates light scattering due to contamination or adulteration particles.

---

## 🚀 Standalone Implementation Strategy
* **Inline Interception:** The dual-port configuration of the PVC chassis allows it to fit directly onto standard liquid pipelines or experimental test chambers for continuous fluid scanning.
* **Power Conservation Loop:** The firmware keeps emitter nodes asleep during deep tracking delays to minimize active current pull on battery networks.
* **Anti-Fluid Isolation:** The internal sampling path uses clear glass wall isolation layers to keep critical logic terminals dry and operating reliably in tough outdoor or lab conditions.

**Come Check It Out In:**[RikHydroTech-Pro](https://rikmakershub.github.io/RikHydroTech-Pro/)
---
*Designed for Extreme Replicability & Real-World Utility by RikMakersHub.*
