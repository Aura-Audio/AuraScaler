# MicScaler 🎛️ (v1.19.0)
**Multi-Instance Mathematical Scaling & Spectral Engine**

MicScaler is a professional-grade, zero-dependency web application designed for high-throughput mathematical processing of live audio data. 

It transforms your browser into a **20,000-channel mathematical processor**, isolating the processes of frequency bandpassing, multiplicative scaling, phase-interleaving, sample-accurate chopping, sub-millisecond gating, and background-proof data recording.

---

## 🚀 Quick Start
1. Download the `index.html` file. (No installation required).
2. Open it in any modern web browser.
3. **Shape:** Enable the Pre-Scale Bandpass to isolate specific frequencies, and verify the shape on the FFT Spectral Graph.
4. **Scale:** The app boots pre-configured with 20 parallel engines enabled (20,000 tracks). Hit **Start Microphone**.
5. **Automate:** Click the master **▶ Start All LFOs** button to globally trigger a massive, staggered array sequence across all 20 engines simultaneously.
6. **Record:** Set an auto-stop limit and capture the manipulated soundscape natively to `.wav`.

---

## 📊 The Analysis Dashboard
MicScaler now features a dual-canvas real-time visualizer layout.
*   **Oscilloscope (Time Domain):** Shows the final mathematical output waveform resulting from the C++ AudioWorklet thread.
*   **FFT Spectral Distribution (Frequency Domain):** Shows a real-time Fast Fourier Transform (FFT) analysis of your raw microphone hardware. 
    *   **Gray Background:** The total acoustic energy captured by the physical microphone.
    *   **Green Outline:** The isolated frequency distribution actively passing through the Bandpass Filter and into the math engine.

---

## ✨ Full List of Features

### 📡 Spectral & Multi-Instance Processing
*   **Pre-Scale Bandpass Filter:** Isolate high or low frequencies *before* they hit the math engine via a dual-biquad (HP/LP) node cluster.
*   **Massive Engine Topology:** Run up to **20 isolated math engines** simultaneously, driving up to **20,000 parallel tracks**.
*   **Cascading Polarity Inversion:** Apply phase flipping via Master Invert, or use **Pattern Invert** to automatically flip interleaved tracks (e.g., every 2nd, 3rd, 4th, or 5th track).

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
*   **Mobile Audio Routing Override:** Bypasses Android and iOS VoIP echo cancellation constraints (`echoCancellation: false`), forcing the OS to push uncompressed signal out of the main bottom loudspeakers.
