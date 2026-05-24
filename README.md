# MicScaler 🎛️ (v1.25.0)

MicScaler is a professional-grade, zero-dependency web application designed for high-throughput mathematical processing of live audio data. It transforms your browser into a **20,000-channel mathematical processor**.

## 🚀 Quick Start
1. Download the `index.html` file.
2. Open it in Chrome, Edge, or Safari.
3. The app will launch with pre-configured settings (Bandpass active, 20 engines enabled, 100 tracks per engine, and staggered LFO timers starting at exactly 0.001s). 
4. Click **Start Microphone** to engage.

## ✨ V1.25.0 Architecture Update: True Audio-Rate LFO Modulation
Previous versions of the Auto-Step LFO suffered from aliasing and UI freezing when pushed to extreme microsecond speeds (like `0.001s`). 

This was because the LFO mathematically evaluated time *once* per audio block (every 128 samples). If the LFO was asked to cycle faster than the block rate, the math engine collapsed.

**The Fix: Per-Sample Modulation**
*   **Audio-Rate LFOs:** The internal loop counter has been completely re-architected. The LFO progress is now calculated inside the strict `for(let i = 0; i < numFrames; i++)` sample loop.
*   **0.001s Flawlessness:** The math engine can now flawlessly execute 1,000 exponential sweeps *per second* completely seamlessly. This effectively transforms the step sequencer into a high-frequency Audio-Rate Modulator. 
*   **Mobile Crash Fallbacks:** Implemented strict `isNaN` and division-by-zero safeguards to guarantee that an aggressive LFO parameter shift will never crash the mobile C++ `AudioWorklet` processor.

## 🎛️ Feature Overview
*   **20,000-Channel Throughput:** Run 20 isolated math engines driving 1,000 tracks each via C++ `AudioWorklet` threads.
*   **AuraConv Comb Filter:** Block or allow audio in sample-accurate intervals (5–5000), complete with dedicated FFT and Time-Domain comb filter visualizers.
*   **Zero-Dependency Recording:** Compiles native `WAV` or compressed `OPUS/FLAC` files directly in the browser.
