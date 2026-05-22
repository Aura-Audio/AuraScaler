# MicScaler 🎛️ (v1.24.0)

MicScaler is a professional-grade, zero-dependency web application designed for high-throughput mathematical processing of live audio data. It transforms your browser into a **20,000-channel mathematical processor**.

## 🚀 Quick Start
1. Download the `index.html` file.
2. Open it in Chrome, Edge, or Safari.
3. The app will launch with pre-configured settings (Bandpass active, 20 engines enabled, 100 tracks per engine, and staggered LFO timers). 
4. Click **Start Microphone** to engage.

## ✨ V1.24.0 Architecture Update: Mobile Stability
Previous versions suffered from a severe "hanging" bug on mobile devices (e.g., Samsung S24+) where the Auto-Step LFOs would stick at `0.0001`. 

This was identified as a **Message Queue Overflow**. The C++ `AudioWorklet` was attempting to update the UI 75 times a second, and when users clicked "Start All LFOs", the UI fired 20 simultaneous messages back to the Worklet. Mobile Chrome aggressively drops IPC (Inter-Process Communication) messages under this kind of load, causing the controls to freeze.

**The Fix:**
*   **Batch Messaging:** The UI now bundles all 20 engine configurations into a single `bulkUpdate` array payload.
*   **IPC Throttling:** The Worklet status updates are now strictly capped at `12Hz`.
*   **DOM Caching:** The 20 text-readout displays are cached in memory on boot, permanently eliminating `getElementById` layout thrashing during the 60fps render loop.

## 🎛️ Feature Overview
*   **20,000-Channel Throughput:** Run 20 isolated math engines driving 1,000 tracks each via C++ `AudioWorklet` threads.
*   **Pre & Post Metering:** Trim input volume and limit hardware output using percentage multipliers. Monitor the raw electrical DB levels at both ends of the chain.
*   **AuraConv Comb Filter:** Block or allow audio in sample-accurate intervals (5–5000), complete with dedicated FFT and Time-Domain comb filter visualizers.
*   **Dual-Layer Gating:** Separate logic for Math Input Data Chops vs Hardware Speaker Modulation.
*   **Zero-Dependency Recording:** Compiles native `WAV` or compressed `OPUS/FLAC` files directly in the browser with hardware-clocked auto-stop timers.
