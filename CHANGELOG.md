# Changelog

All notable changes to **J.A.R.V.I.S. (Mark 54) for macOS** will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [54.0.0] — 2026-09-20

### Added
- **Initial Release of J.A.R.V.I.S. Mark 54 for macOS**.
- **Real-Time Voice Duplex**: Bidirectional conversational voice streaming powered by Google Gemini Live 2.0 WebSockets API at 24 kHz.
- **Multimodal Vision Sentry**: 24/7 camera monitoring with background motion detection and live face tracking.
- **Deep Screen Perception**: High-speed display capture and visual debugging via MSS and Gemini multimodal models.
- **macOS System Automation**: Native AppleScript / System Events control for launching apps, searching Safari, managing files, and window control.
- **Hardware-Accelerated UI**: Floating, draggable Arc Reactor HUD rendered in PyQt6 (Qt 6.8).
- **Standalone Distribution**: Self-contained mountable `jarvis.dmg` (169 MB) for Apple Silicon (M1/M2/M3/M4) with embedded Python 3.11 runtime.

### Security
- Embedded macOS security entitlements for Microphone, Camera, Screen Recording, and JIT dynamic memory allocation.
- Localized API key storage at `~/.config/jarvis/api_keys.json` with zero external developer telemetry.
- Cryptographic SHA-256 release checksum verification (`SHA256SUMS`).

### Documentation
- Comprehensive 16-section README with click-by-click Google Gemini API key generation guide.
- System architecture specifications (`docs/ARCHITECTURE.md`).
- macOS Transparency, Consent, and Control (TCC) permissions breakdown (`docs/PERMISSIONS.md`).
- Responsible automation & human-in-the-loop policy (`docs/RESPONSIBLE_AUTOMATION.md`).
- Security vulnerability disclosure policy (`SECURITY.md`).
- Third-party dependency notices (`THIRD_PARTY_NOTICES.md`).

---

## [54.1.0] — Planned / Upcoming

### Added
- **macOS Keychain Integration**: Native storage of Gemini API keys directly within the Apple Keychain Services API rather than plaintext JSON.
- **Multi-Monitor DPI Auto-Detection**: Dynamic high-DPI scaling when dragging the floating Arc Reactor HUD between built-in Retina displays and external 4K/5K monitors.
- **Custom Wake-Word Engine**: Choose between *"Hey Jarvis"*, *"Friday"*, or train your own local wake word.
- **Plugin Store**: Easy modular installation of action plugins for VS Code, Slack, and Spotify.

### Improved
- Low-power efficiency profile to minimize MacBook battery drain during extended background sentry monitoring.
- Enhanced screen perception token efficiency with intelligent region-of-interest cropping.
