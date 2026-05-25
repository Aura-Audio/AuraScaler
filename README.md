# MicScaler 🎛️ (v1.27.0)

MicScaler is a professional-grade, zero-dependency web application designed for high-throughput mathematical processing of live audio data. It transforms your browser into a **20,000-channel mathematical processor**.

## 🚀 Quick Start
1. Download the `index.html` file.
2. Open it in Chrome, Edge, or Safari.
3. The app will launch with pre-configured settings (Bandpass active, 20 engines enabled, 100 tracks per engine, and staggered LFO timers). 
4. Click **Start Microphone**. 
5. A **Pre-Flight BIOS Overlay** will appear to securely handshake with the C++ Audio Thread before fading out and starting the audio stream.

## ✨ V1.27.0 Architecture Update: Pre-Flight Handshake
Previous versions occasionally suffered from a "silent freeze" when running on high-end mobile devices under heavy load. This was diagnosed as an **IPC Race Condition**: the browser's UI thread would attempt to blast the 20-Engine configuration payload into the background C++ `AudioWorklet` before the mobile CPU had finished compiling it, causing the messages to drop into the void.

**The Fix: Automated BIOS Boot Sequence**
*   **The Ping/Pong Handshake:** MicScaler no longer assumes the audio thread is ready. When you click start, it halts the Javascript UI and sends a microscopic `{ type: 'ping' }` packet to the C++ core. It waits in a suspended promise state until the core replies with `{ type: 'pong' }`. Only then does it release the massive 20,000-track payload.
*   **Visual Diagnostic Console:** Users are now presented with a dark, terminal-style overlay tracking the exact status of the boot sequence (Microphone Request, Worklet Compilation, IPC Handshake). If the mobile processor ever fails to boot, the sequence will halt and highlight the exact point of failure in Red, ending the era of silent freezing.
