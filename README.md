# MicScaler 🎛️ (v1.20.0)
**Multi-Instance Mathematical Scaling & Spectral Engine**

MicScaler is a professional-grade, zero-dependency web application designed for high-throughput mathematical processing of live audio data. 

It transforms your browser into a **20,000-channel mathematical processor**, isolating the processes of frequency bandpassing, multiplicative scaling, phase-interleaving, sample-accurate chopping, sub-millisecond gating, and background-proof data recording.

---

## 🚀 Quick Start
1. Download the `index.html` file. (No installation required).
2. Open it in any modern web browser.
3. **Shape:** Enable the Pre-Scale Bandpass to isolate specific frequencies, and verify the shape on the FFT Spectral Graph.
4. **Scale:** The app boots pre-configured with 20 parallel engines enabled (20,000 tracks). Hit **Start Microphone**.
5. **Phase Patterning:** Select a pattern from the "Master Pattern" dropdown and click "Set All" to instantly push a uniform phase-inversion rule to all 20,000 tracks.
6. **Automate:** Click the master **▶ Start All LFOs** button to globally trigger a massive, staggered array sequence across all 20 engines simultaneously.

---

## ✨ Key Features

### 📡 Spectral & Multi-Instance Processing
*   **Pre-Scale Bandpass Filter:** Isolate high or low frequencies *before* they hit the math engine via a dual-biquad (HP/LP) node cluster.
*   **Massive Engine Topology:** Run up to **20 isolated math engines** simultaneously, driving up to **20,000 parallel tracks**.
*   **Batch Phase Interleaving:** The "Master Pattern" tool pushes uniform phase cancellation rules across all engines (e.g., Inverting every 2nd or 4th track). Because it acts as a batch command rather than a global lock, users can re-apply a baseline state and then manually tweak individual engine patterns safely.

### ⏱️ Sequence Automation (Auto-Step LFO)
*   **Master LFO Control:** One-click global start/stop synchronization for all 20 internal engine LFOs.
*   **Custom Boundary LFO:** Define arbitrary `Start` (High) and `End` (Low) scaling limits to automate the array spread.
*   **Drift-Proof Audio Clock:** The LFO is driven by the native hardware audio sample rate (48,000Hz) inside the C++ background thread. **It is 100% immune to browser tab-throttling** and will loop endlessly in the background.

### 🔪 AuraConv Interval Engine
*   **Sample-Accurate Comb Filter:** Blocks or allows audio in exact $N$-sample blocks (e.g., every 50 or 100 samples) at the hardware level.
*   **Synthetic Convolution Reverb & HRTF:** Mathematically generates a 2-second white-noise exponential-decay impulse response on the fly to smear transients, and dynamically rotates the audio in 3D space around the listener's head.

### 🎚️ Sub-Millisecond Gating & Native Recording
*   **Dual-Layer Gating:** Separate logic for Math Input Data Chops vs Hardware Speaker Modulation (up to 10,000Hz).
*   **Zero-Dependency WAV Compiler:** Captures the raw `Float32` data array and mathematically compiles a valid 16-bit Mono `RIFF/WAVE` file inside the browser. Hardware-clocked to auto-stop recordings even if the screen locks.
