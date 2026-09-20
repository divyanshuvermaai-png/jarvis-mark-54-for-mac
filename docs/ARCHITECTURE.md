# J.A.R.V.I.S. Mark 54 — System Architecture

This document outlines the internal architecture, technical design, and operational pipeline of **J.A.R.V.I.S. (Mark 54) for macOS**.

---

## 🏛️ High-Level System Architecture

J.A.R.V.I.S. operates on a 3-tier modular architecture designed for ultra-low latency, real-time multimodal perception, and safe system execution:

```text
                               ┌────────────────────────┐
                               │   User Interaction     │
                               │ (Voice / Camera / HUD) │
                               └───────────┬────────────┘
                                           │
                                           ▼
┌────────────────────────────────────────────────────────────────────────────────────────┐
│                                 PERCEPTION LAYER                                       │
│                                                                                        │
│  ┌──────────────────────┐    ┌──────────────────────┐    ┌──────────────────────────┐  │
│  │   Microphone Audio   │    │    Webcam Capture    │    │      Screen Perception   │  │
│  │ (PortAudio / 24kHz)  │    │  (OpenCV VideoStream)│    │      (MSS Fast Buffer)   │  │
│  └──────────┬───────────┘    └──────────┬───────────┘    └────────────┬─────────────┘  │
└─────────────┼───────────────────────────┼─────────────────────────────┼────────────────┘
              │                           │                             │
              ▼                           ▼                             ▼
┌────────────────────────────────────────────────────────────────────────────────────────┐
│                              REASONING & COGNITION LAYER                               │
│                                                                                        │
│  ┌──────────────────────────────────────────────────────────────────────────────────┐  │
│  │                  Bidirectional Streaming Duplex Engine                           │  │
│  │             (Google Gemini Live 2.0 Multimodal WebSockets API)                   │  │
│  └──────────────────────────────────────┬───────────────────────────────────────────┘  │
│                                         │                                              │
│                        ┌────────────────┴────────────────┐                             │
│                        │ Function Call & Tool Dispatcher │                             │
│                        └────────────────┬────────────────┘                             │
└─────────────────────────────────────────┼──────────────────────────────────────────────┘
                                          │
                                          ▼
┌────────────────────────────────────────────────────────────────────────────────────────┐
│                               ACTION & AUTOMATION LAYER                                │
│                                                                                        │
│  ┌──────────────────────┐    ┌──────────────────────┐    ┌──────────────────────────┐  │
│  │  macOS Automation    │    │    PyQt6 UI HUD      │    │     Files & Settings     │  │
│  │   (NSAppleEvents)    │    │ (Floating Arc Reactor│    │   (~/.config/jarvis)     │  │
│  └──────────────────────┘    └──────────────────────┘    └──────────────────────────┘  │
└────────────────────────────────────────────────────────────────────────────────────────┘
```

---

## 📦 Binary & Packaging Architecture

From the verified DMG bundle inspection:

- **Mach-O Architecture**: Native `arm64` 64-bit executable, optimized for Apple Silicon (M1, M2, M3, M4).
- **Executable Engine**: PyInstaller standalone runtime bundle freezing Python 3.11 (`libpython3.11.dylib`).
- **UI Framework**: PyQt6 (Qt 6.8 backend) featuring hardware-accelerated OpenGL/Metal rendering for the floating Arc Reactor HUD.
- **Audio Subsystem**: PortAudio v19 with native CoreAudio backend via `sounddevice`, operating at 24 kHz mono PCM for bidirectional Gemini Live audio duplexing.
- **Vision Subsystem**: OpenCV (libavcodec, libavformat, libswscale) with native AVFoundation camera capture.
- **Display Perception**: MSS high-speed frame grabber with Retina display support.

---

## 🔄 Lifecycle & Execution Pipeline

1. **Initialization**:
   - Application launches via `JARVIS.app/Contents/MacOS/JARVIS`.
   - Checks for existing configuration at `~/.config/jarvis/api_keys.json`.
   - Initializes PyQt6 application loop and registers global Hotkey monitors.
2. **Duplex Session Connection**:
   - Establishes a secure TLS WebSocket connection to Google's Gemini Live API endpoint.
   - Negotiates audio input format (16-bit PCM, 24,000 Hz) and audio output stream.
3. **Continuous Perception**:
   - Microphone input is buffered through a RingBuffer and streamed in real-time chunks.
   - When requested by user prompt or automated sentry mode, video frames or screen snapshots are downsampled and submitted as multimodal inline image parts.
4. **Tool / Action Dispatch**:
   - When Gemini returns a `functionCall`, the dispatcher maps it to native action handlers (e.g., launching Safari, checking system load, retrieving weather, organizing directories).
   - Results are sent back via `functionResponse` for immediate conversational acknowledgment.
