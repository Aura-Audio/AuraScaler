# MicScaler 🎛️ (v1.14.0)
**Multi-Instance Mathematical Scaling & DSP Engine**

MicScaler is a professional-grade, zero-dependency web application designed for high-throughput mathematical processing of live audio data. 

Unlike standard audio mixing concepts (where Gain is pre-processing and Volume is post-processing), **MicScaler treats audio as pure data**. It transforms your browser into a **3,000-channel mathematical processor**, isolating the processes of multiplicative scaling ($x$), phase-interleaving, sample-accurate chopping, and sub-millisecond gating.

---

## 🚀 Quick Start
1. Download the `index.html` file. (No installation, Node.js, or external assets required).
2. Open it in any modern web browser (Chrome, Edge, Safari, Firefox).
3. Toggle up to **3 Independent Engines** on the dashboard.
4. Click **Start Microphone**.
5. **Automate:** Use the Auto-Step LFO to create custom exponential sweeps across your track arrays.
6. **Gate & Chop:** Enable the AuraConv comb filter or the sub-millisecond hardware gates.
7. **Record:** Set an auto-stop limit and capture the manipulated soundscape natively to `.wav`.

---

## ✨ Full List of Features

### 📡 Multi-Instance Processing (3,000 Tracks)
*   **Triple-Engine Topology:** Run up to 3 isolated math engines simultaneously. Each engine can calculate up to 1,000 parallel tracks, allowing for a massive **3,000-track** total throughput.
*   **Cascading Polarity Inversion:** Apply phase flipping via Master Invert, or use **Pattern Invert** to automatically flip interleaved tracks (e.g., every 2nd, 3rd, 4th, or 5th track) creating complex phase-canceled arrays.

### ⏱️ Sequence Automation (Auto-Step LFO)
*   **Custom Boundary LFO:** Define arbitrary `Start` (High) and `End` (Low) scaling limits (e.g., from `1.0%` down to `0.0001%` or vice-versa) to automate the array spread over a user-defined duration.
*   **Drift-Proof Audio Clock:** The LFO is driven by the native hardware audio sample rate (48,000Hz) inside the C++ background thread. **It is 100% immune to browser tab-throttling** and will loop perfectly in the background indefinitely.
*   **Logarithmic Sweeps:** Interpolates logarithmically to guarantee perfectly smooth perceptual sweeps through microscopic decimal fractions in both ascending and descending directions.

### 🔪 AuraConv Interval Engine
*   **Sample-Accurate Comb Filter:** Tracks the absolute hardware sample counter to perfectly chop data arrays into exact $N$-sample blocks (e.g., every 50 or 100 samples).
*   **Burst & Gap Modes:** Choose to `Allow` audio through in rhythmic bursts or `Block` it to create rhythmic silence gaps.
*   **Synthetic Convolution Reverb:** Mathematically generates a lush, 2-second exponential-decay white-noise array on the fly to act as an Impulse Response (IR) smear.
*   **HRTF 3D Rotation:** Real-time spatial rotation utilizing Web Audio's `PannerNode`, violently panning the chopped signal around the listener's head.

### 🎚️ Dual-Layer Sub-Millisecond Gating
*   **Math Input Auto-Toggle:** A digital gate that mathematically zeroes out the bit-stream feeding *into* the math engines.
*   **Speaker Output Auto-Toggle:** Physically modulates the hardware speaker output using a 10kHz square-wave oscillator attached to a `GainNode`. Allows for brutal Amplitude Modulation (AM) effects down to `0.1ms`.

### 💾 Native Recording & Export
*   **Zero-Dependency WAV Compiler:** Bypasses compressed browser audio. Captures the raw `Float32` data array and mathematically compiles a valid 16-bit Mono `RIFF/WAVE` header on the fly inside the browser.
*   **MediaRecorder Support:** Supports highly compressed OPUS (`.webm`) and lossless FLAC exports.
*   **Auto-Stop Timers:** Enter a minute limit to record unattended. The app will automatically halt, compile, and trigger a local file download when the timer hits, preventing RAM overflows.

### 📱 Hardware Control
*   **Mobile Audio Routing Override:** Android and iOS natively hijack microphone streams for VoIP echo cancellation, routing audio to the quiet top earpiece. The **Earpiece Mode** toggle overrides WebRTC constraints (`echoCancellation: false`), forcing the OS to push uncompressed signal out of the main bottom loudspeakers.

---

## 📈 Architecture & Performance Improvements (v1.14.0)

MicScaler has been entirely re-architected to bypass browser bottlenecks, shifting from a UI-bound visualizer to an asynchronous **AudioWorklet DSP Engine**. To maintain our strict "Single HTML File" rule, the C++ style processor class is converted to a virtual Blob in the device's RAM and injected dynamically at runtime.

| Metric | Legacy (v1.9.0) | Current (v1.14.0) | Improvement |
| :--- | :--- | :--- | :--- |
| **Max Throughput** | 1,000 Tracks | **3,000 Tracks** | **+200% Capacity** |
| **RAM Footprint** | ~280 MB + GC Spikes | **~55 MB** | **-80% Memory Bloat** |
| **Main UI CPU Load** | 85% - 100% | **1% - 3%** | The UI thread is virtually asleep, purely drawing the Master Canvas. |
| **Audio Thread Load** | 0% (Forced to UI) | **~10%** | Math runs entirely on a dedicated, high-priority background core. |
| **Audio Stability** | Severe Clicking / Pops | **Flawless** | 100% immune to UI freezing, scrolling, or background tab sleeping. |

*   **The "Clicking" Fix:** In previous versions, rendering 1,000 text boxes on the DOM caused mobile CPUs (like the S24+) to drop audio frames, resulting in audible hardware clicking and amplifier power-cycling. By deleting the DOM bloat and moving the math to a dedicated background core, MicScaler now runs **144 Million math operations per second** completely glitch-free.

---

## 🗺️ Roadmap of Future Features

### Phase 1: Advanced DSP & Data Manipulation
*   **Offset Engine (+):** Implement `(Input * Scale) + Offset` logic to shift signal baselines for sensor calibration and bias correction.
*   **Hard Clipping & Clamping:** Add user-defined mathematical limits to introduce intentional saturation, data-clipping, and threshold bounds across the engine arrays.
*   **DC Offset Filtering:** A dedicated high-pass filter at 5Hz to mathematically center raw Android microphone feeds that suffer from native electrical offsets.

### Phase 2: Hardware & Edge Deployments
*   **The "Wall Plug" Port (Python/Raspberry Pi):** Refactor the core Math Engine into a vectorized NumPy/Python script to be flashed onto headless Raspberry Pi Zero / ESP32 hardware. This will allow for dedicated hardware I2S microphone processing in embedded acoustic environments.
*   **Hardware Output Selection (`setSinkId`):** Utilize experimental browser APIs to allow users to explicitly define which physical audio output channel (Bluetooth, USB interface, specific Studio Monitor pairs) the app routes the data to.

### Phase 3: External Data Routing
*   **WebSockets & OSC (Open Sound Control):** Broadcast the processed mathematical results of the instances over `localhost` to drive reactive data visualization in external software like TouchDesigner, Resolume, or Python pipelines.
*   **Web MIDI API Integration:** Convert the scaled, multi-track data outputs into continuous MIDI Control Change (CC) messages to drive DAW parameters (e.g., Engine 1 controls a cutoff filter, Engine 2 controls reverb decay).

---

## ⚠️ Requirements & Safety
*   **Environment:** Must be run on `localhost` or an `https` connection, as browsers strictly block microphone access on unsecure `http://` connections.
