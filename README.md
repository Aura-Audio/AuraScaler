# MicScaler 🎛️ (v1.21.0)
**Multi-Instance Mathematical Scaling & Spectral Engine**

MicScaler is a professional-grade, zero-dependency web application designed for high-throughput mathematical processing of live audio data. 

It transforms your browser into a **20,000-channel mathematical processor**, isolating the processes of pre-gain structuring, frequency bandpassing, multiplicative scaling, phase-interleaving, and sub-millisecond hardware gating.

---

## 🚀 Quick Start
1. Download the `index.html` file. (No installation required).
2. Open it in any modern web browser.
3. **Gain Stage:** Use the `Mic Vol (%)` to digitally trim your hardware microphone input, observing the Real-Time dB Meter to prevent clipping.
4. **Shape:** Enable the Pre-Scale Bandpass to isolate specific frequencies, and verify the shape on the FFT Spectral Graph.
5. **Architect:** Use the Master Dashboard to spawn anywhere between 1 and 20 Math Engines, dynamically assigning up to 1,000 tracks per engine.
6. **Automate:** Click the master **▶ Start All LFOs** button to globally trigger a massive, staggered array sequence across your active engines simultaneously.

---

## 📊 The Analysis Dashboard
MicScaler now features a dual-canvas real-time visualizer layout.
*   **Oscilloscope (Time Domain):** Shows the final mathematical output waveform resulting from the C++ AudioWorklet thread.
*   **FFT Spectral Distribution (Frequency Domain):** Shows a real-time Fast Fourier Transform (FFT) analysis of your raw microphone hardware. 
    *   **Gray Background:** The total acoustic energy captured by the physical microphone.
    *   **Green Outline:** The isolated frequency distribution actively passing through the Bandpass Filter and into the math engine.
*   **Throttled RMS Metering:** Shows absolute hardware decibel (dB) levels before and after your percentage-based Input Gain modifications.

---

## ✨ Full List of Features

### 📡 Spectral & Multi-Instance Processing
*   **Pre-Gain Structuring:** Trim or boost your microphone data via percentage multiplication prior to any array processing.
*   **Pre-Scale Bandpass Filter:** Isolate high or low frequencies *before* they hit the math engine via a dual-biquad (HP/LP) node cluster.
*   **Master Architect Configurator:** Dynamically manage UI and computational load by actively defining how many Math Engines (1-20) and how many tracks per engine (1-1000) your processor should allocate.
*   **Batch Phase Interleaving:** Pushes uniform phase cancellation rules across all engines (e.g., Inverting every 2nd or 4th track). 

### ⏱️ Sequence Automation (Auto-Step LFO)
*   **Master LFO Control:** One-click global start/stop synchronization for all active internal engine LFOs.
*   **Drift-Proof Audio Clock:** The LFO is driven by the native hardware audio sample rate (48,000Hz) inside the C++ background thread. **It is 100% immune to browser tab-throttling** and will loop endlessly in the background.

### 🔪 AuraConv Interval Engine & Hardware Gating
*   **Sample-Accurate Comb Filter:** Blocks or allows audio in exact $N$-sample blocks at the hardware level.
*   **Synthetic Convolution Reverb & HRTF:** Mathematically generates a 2-second white-noise exponential-decay impulse response on the fly to smear transients, and dynamically rotates the audio in 3D space around the listener's head.
*   **Dual-Layer Gating:** Separate logic for Math Input Data Chops vs Hardware Speaker Modulation (up to 10,000Hz).
*   **Zero-Dependency WAV Compiler:** Captures the raw `Float32` data array and mathematically compiles a valid 16-bit Mono `RIFF/WAVE` file inside the browser.
