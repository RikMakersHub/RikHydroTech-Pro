# 🛰️ Project HydroTech: Ultra-Low-Cost Inline Fluid Spectrometer
> Open-Source Bare-Metal Fluid Analytics Terminal by RikMakersHub

An ultra-low-cost (~$4.50 / ₹350), standalone optical spectrometry system engineered to detect liquid contamination, fluid density shifts, or chemical transmission profiles natively without custom laboratory hardware or cloud configurations.

---

## 💡 The Problem: High-Cost Fluid Auditing
Checking the purity of liquids or identifying structural anomalies in different fluid layers is highly restricted by economic constraints. Commercial multi-wavelength spectrometers are expensive, delicate, and often require constant cloud connectivity or enterprise software licenses to process simple metrics. 

**HydroTech** strips down the engineering to bare-metal principles: leveraging structured chromatic wavelength paths inside a light-tight pipeline enclosure to run immediate, local fluid diagnostic thresholds on a dirt-cheap microcontroller, managed by a lightweight, responsive web terminal interface.

---

## 📊 Value Engineering & Hardware Strategy
To keep the system scalable and highly replicable, all electronic sub-assemblies avoid specialized modular chips. Instead, the design forces elementary components to perform complex physical telemetry over basic analog buses:

* **Chassis Conduit (1" PVC T-Joint):** Rather than relying on fragile 3D-printed filaments, a common industrial PVC joint serves as a robust, weatherproof housing. Treating the internal chamber with a matte-black surface layer effectively nullifies environmental ambient lux interference.
* **Optical Array (High-Intensity RGB LED):** Operates as a sequential, multi-wavelength light emitter. By flashing isolated spectrum vectors across the sampling fluid channel, the system measures targeted transmission behaviors across different color bands.
* **Telemetry Core (5mm LDR + Pi Pico / Pro Mini):** The photoresistor functions as a dynamic analog receiver, transforming light scattering into precise voltage variations read straight via the controller's internal ADC.

---

## 💻 The Bare-Metal Firmware Logic
The core firmware runs on local synchronous state logic. Instead of measuring continuous light—which drops accuracy over time due to thermal drift—the micro executes a high-speed pulsed matrix loop:

1. **Ambient Baseline Initialization:** Isolates the current zero-lux dark value inside the PVC tube.
2. **Sequential Pulse Stream:** Activates individual GPIO emitter gates for Red, Green, and Blue light pathways, adding an 85ms stabilization cooldown window per pulse.
3. **Vector Capture & Serialization:** Aggregates individual channel analog drops (`rSum`, `gSum`, `bSum`) and immediately pipes raw data strings (`VEC:R,G,B`) over a 115200 baud UART bus.

Any drop in light transmission value against a baseline calibration profile (like pure water) immediately signals contamination or fluid density shifts due to foreign particles.

---

## 🚀 Standalone Implementation Strategy
* **Inline Interception:** The dual-port configuration of the PVC chassis allows it to fit directly onto standard liquid pipelines or experimental test chambers for continuous fluid scanning.
* **Power Conservation Loop:** The firmware keeps emitter nodes asleep during deep tracking delays to minimize active current pull on battery networks.
* **Anti-Fluid Isolation:** The internal sampling path uses clear glass wall isolation layers to keep critical logic terminals dry and operating reliably in tough outdoor or lab conditions.
