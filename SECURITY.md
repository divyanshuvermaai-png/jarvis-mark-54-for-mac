# Security Policy — J.A.R.V.I.S. Mark 54

## 🔒 Reporting a Vulnerability

Security is paramount. If you discover a vulnerability or security flaw in J.A.R.V.I.S. Mark 54, please report it **privately** so we can patch it before public disclosure:

📧 **Email**: `divyanshuverma.ai@gmail.com`  
**Subject**: `[SECURITY VULNERABILITY] J.A.R.V.I.S. Mark 54`

Please include:
1. Detailed description of the vulnerability.
2. Step-by-step reproduction instructions or proof-of-concept.
3. Affected macOS versions and environment.

We will acknowledge your report within 48 hours and work with you to remediate the issue promptly.

---

## 🛡️ Supported Versions

| Version | Supported | Notes |
| :--- | :---: | :--- |
| **54.0.x** | ✅ | Current stable release |
| < 54.0.0 | ❌ | Legacy experimental releases |

---

## 🔐 Security Principles & Boundaries

J.A.R.V.I.S. Mark 54 adheres to strict security standards:

- **Explicit macOS TCC Authorization**: J.A.R.V.I.S. operates strictly within the macOS security model. It cannot capture audio, access the camera, record the screen, or automate applications without explicit permission granted in **System Settings > Privacy & Security**.
- **No Remote Execution Backdoors**: J.A.R.V.I.S. does not expose open network ports to the public internet. Local HTTP servers (such as the local web dashboard) bind exclusively to `127.0.0.1`.
- **API Key Protection**: API keys are read strictly by the application and stored in `~/.config/jarvis/api_keys.json`. Users should restrict file permissions to prevent other local accounts from reading the file:
  ```bash
  chmod 600 ~/.config/jarvis/api_keys.json
  ```
  *(Migration to native macOS Keychain storage is planned for the v54.1.0 release).*
- **Ad-Hoc Signing & Entitlements**: The binary is signed with hardened runtime entitlements allowing only necessary system hardware interfaces (`com.apple.security.device.audio-input`, `com.apple.security.device.camera`, `com.apple.security.cs.allow-jit`).
