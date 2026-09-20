# macOS Permissions Guide — J.A.R.V.I.S. Mark 54

To deliver autonomous desktop companion features on macOS, J.A.R.V.I.S. Mark 54 requests explicit user permissions under macOS Transparency, Consent, and Control (TCC) security framework.

---

## 📋 Permissions Overview

| Permission | `Info.plist` Key | Required For | Technical Purpose |
| :--- | :--- | :--- | :--- |
| 🎙️ **Microphone** | `NSMicrophoneUsageDescription` | Voice Interaction | Captures voice input for real-time duplex streaming to Google Gemini Live API. |
| 📷 **Camera** | `NSCameraUsageDescription` | Security Sentry & Vision | Enables 24/7 Security Sentry motion tracking, user presence detection, and visual recognition. |
| 🖥️ **Screen Recording** | `NSScreenCaptureUsageDescription` | Screen Perception | Captures screen frames when you ask JARVIS to debug code, analyze diagrams, or inspect documents. |
| ♿ **Accessibility** | `NSAppleEventsUsageDescription` | Desktop Automation | Automates system actions, controls application windows, and executes authorized workflows via AppleScript. |

---

## 🔍 Detailed Permission Justifications

### 1. Microphone Access
- **Why it is needed**: J.A.R.V.I.S. features natural, uninterrupted bidirectional voice conversations. You can talk freely, ask questions, and interrupt mid-sentence without holding buttons.
- **Data Flow**: Audio is captured via CoreAudio / PortAudio at 24 kHz mono and transmitted over an encrypted TLS connection directly to Google Gemini Live API.
- **Privacy Assurance**: J.A.R.V.I.S. does not save audio recordings to disk or transmit them to any third party other than Google's API.

### 2. Camera Access
- **Why it is needed**: Powering the Security Sentry mode, user facial verification, and live visual question-answering.
- **Data Flow**: Frames are captured through AVFoundation / OpenCV. In interactive vision mode, individual downsampled JPEG frames are transmitted to Gemini Live when you explicitly ask a visual question.
- **Sentry Mode**: In Security Sentry mode, motion analysis runs locally using background subtraction algorithms. No continuous video feed is uploaded to external servers.

### 3. Screen Recording Access
- **Why it is needed**: Allows JARVIS to "see" your monitor when you say *"Look at my screen"* or *"Debug this code"*.
- **Data Flow**: MSS captures the active display buffer only upon request. The frame is evaluated in memory and submitted as a multimodal prompt.
- **Security Control**: JARVIS does not silently record your screen in the background. Screen grabs occur only on direct invocation.

### 4. Accessibility & Apple Events
- **Why it is needed**: Allows JARVIS to interact with macOS applications, navigate menus, launch apps, and manipulate windows on your behalf.
- **Data Flow**: Standard AppleScript commands are executed via macOS System Events.

---

## 🛠️ How to Manage Permissions

You can view, grant, or revoke permissions at any time in **System Settings**:
1. Open **System Settings** on your Mac.
2. Navigate to **Privacy & Security**.
3. Inspect each section:
   - **Microphone** > Ensure `JARVIS` is toggled **ON**.
   - **Camera** > Ensure `JARVIS` is toggled **ON**.
   - **Screen Recording** > Ensure `JARVIS` is toggled **ON**.
   - **Accessibility** > Ensure `JARVIS` is toggled **ON**.
4. To revoke access, simply toggle the switch off.
