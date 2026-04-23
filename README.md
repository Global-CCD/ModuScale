# ModuScale: Live Mic LFO Scaler

![HTML5](https://img.shields.io/badge/html5-%23E34F26.svg?style=for-the-badge&logo=html5&logoColor=white)
![JavaScript](https://img.shields.io/badge/javascript-%23323330.svg?style=for-the-badge&logo=javascript&logoColor=%23F7DF1E)
![Web Audio API](https://img.shields.io/badge/Web_Audio_API-000000?style=for-the-badge)

**ModuScale** is a zero-dependency, single-page web application that applies real-time LFO (Low-Frequency Oscillator) modulation to your live microphone input. 

Unlike standard tremolo effects that blindly adjust output volume, ModuScale is built on strict audio-mathematics. It utilizes Web Audio API routing to apply precise **Multiplicative (x)** scaling and **Constant Addition (+)** offset to the control data, ensuring accurate expansion and shrinking of the audio signal ranges across multiple concurrent tracks.

## 🧠 The Math Logic

This application strictly separates audio processing into specific mathematical domains:

| Feature | Stage | Primary Use | Math Logic |
| :--- | :--- | :--- | :--- |
| **Gain** | Pre-Processing | Signal strength/Saturation | Additive/Subtractive (dB) |
| **Volume** | Post-Processing | Mixing and Balancing | Additive/Subtractive (dB) |
| **Scale** | Data/Control | Shrinking/Expanding ranges | Multiplicative (x) |
| **Offset**| Data/Control | Shifting the baseline | Constant Addition (+) |

## ✨ Features

* **Strict Scaling Engine:** Utilizes isolated `ConstantSourceNode` (Offset) and `GainNode` (Multiplier/Scale) architecture to process the LFO control data before it touches the audio signal.
* **Concurrent Multi-Tracking:** Run up to 5 individual LFO tracks simultaneously against the same live mic input.
* **Global BPM & QN Sync:** Precise mathematical speed mapping. Frequency is calculated via `BPM / (60 * QuarterNotes)`.
* **Reaper-Matched Waveforms:** Supports Sine, Square, Triangle, Saw R (Falling), and dynamically phase-inverted Saw L (Rising).
* **Live Visualizers:** Real-time visual feedback of the currently calculated LFO multiplier.
* **Zero Dependencies:** 100% Vanilla HTML, CSS, and JS. Just open the file and go.

---

## 📖 How to Use the UI

### 1. Setup & Audio Initialization
* **⚠️ IMPORTANT:** Plug in headphones before starting to prevent destructive audio feedback loops between your speakers and microphone.
* Click **"Enable Microphone"**. Your browser will prompt you for microphone permissions. 
* To cut the audio at any time, click **"Stop Audio"**.

### 2. Global Settings
* **Global BPM:** Sets the master tempo for the application (e.g., 120).
* **Number of Tracks:** Choose between 1 and 5 concurrent scaling tracks. The app automatically balances the master volume to prevent digital clipping when combining multiple tracks.

### 3. Track Settings
Each track operates completely independently:
* **LFO Waveform:** Choose the shape of the LFO. 
* **Speed (QN):** Set how fast the LFO cycles based on Quarter Notes. For example, at 120 BPM, a `4` QN speed will complete one full cycle exactly every 2 seconds.
* **LFO Amount %:** Determines the mathematical scale factor. At `100%`, the signal scales entirely from `0.0` to `1.0`. At `50%`, it scales from `0.25` to `0.75`.
* **Visualizer:** Watch the yellow bar expand and shrink to represent the real-time Multiplier value being applied to the audio.

---

## 🚀 Roadmap of Future Features

We are constantly looking to expand ModuScale's mathematical audio capabilities. Here is what is planned for future releases:

* [ ] **Phase Offset Control:** Add the ability to shift the phase (0° to 360°) of individual LFOs so multiple tracks running at the same QN can interweave rhythmically.
* [ ] **Stereo Panning Integration:** Route the output of individual scaled tracks to hard-Left or hard-Right channels.
* [ ] **Hardware Input Selection:** A dropdown to select which audio interface/microphone to use, rather than defaulting to the OS primary device.
* [ ] **Web MIDI Sync:** Allow the Global BPM to be controlled by an external MIDI clock signal via the Web MIDI API.
* [ ] **Recording / WAV Export:** Add a `MediaRecorder` node to capture the modulated performance and download it directly as a `.wav` file.
* [ ] **Custom Waveforms:** A canvas-based wave drawer to create custom LFO shapes to feed into the multiplier node.

---

## 🛠 Installation

Because ModuScale is a static, zero-dependency app, installation is instant:

1. Clone or download this repository.
2. Open `index.html` (or `mic-scaler.html`) in any modern web browser (Chrome, Firefox, Safari, Edge).
3. Ensure you have a microphone connected.

## License
MIT License. Feel free to use, modify, and distribute this code as you see fit!
