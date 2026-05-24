# MicScaler 🎛️ (v1.26.0)

MicScaler is a professional-grade, zero-dependency web application designed for high-throughput mathematical processing of live audio data. It transforms your browser into a **20,000-channel mathematical processor**.

## 🚀 Quick Start
1. Download the `index.html` file.
2. Open it in Chrome, Edge, or Safari.
3. The app will launch with pre-configured settings (Bandpass active, 20 engines enabled, 100 tracks per engine, and staggered LFO timers starting at exactly 0.001s). 
4. Click **Start Microphone** to engage.

## ✨ V1.26.0 Version Tagging & Title Update
Ensuring clarity for researchers and developers, Version 1.26.0 introduces explicit version tagging in the primary UI header and document title. Users no longer need to check the console or the file properties to verify they are running the latest Audio-Rate Modulated LFO build.

## 🎛️ Feature Overview
*   **True Audio-Rate LFOs:** Calculates exponential scaling arrays 48,000 times a second, allowing for flawless sub-millisecond sweeps (down to `0.001s`) across thousands of tracks without aliasing or dropping frames.
*   **20,000-Channel Throughput:** Run 20 isolated math engines driving 1,000 tracks each via C++ `AudioWorklet` threads.
*   **AuraConv Comb Filter:** Block or allow audio in sample-accurate intervals (5–5000), complete with dedicated FFT and Time-Domain comb filter visualizers.
*   **Zero-Dependency Recording:** Compiles native `WAV` or compressed `OPUS/FLAC` files directly in the browser.
