# Responsible Automation & Safety Policy — J.A.R.V.I.S. Mark 54

J.A.R.V.I.S. Mark 54 possesses the capability to automate desktop workflows, manipulate files, control applications, and interact with the macOS operating system. With great autonomy comes the responsibility to safeguard user assets, personal data, and system integrity.

---

## 🛡️ The 5-Step Safety Guardrail Flow

For all sensitive or high-impact desktop automations, J.A.R.V.I.S. follows a **Human-in-the-Loop** safety architecture:

```text
┌──────────────┐     ┌───────────────────┐     ┌────────────────┐     ┌───────────────────┐     ┌──────────────┐
│  AI Decides  │ ──> │ Action Identified │ ──> │   Risk Check   │ ──> │ User Confirmation │ ──> │   Execute    │
└──────────────┘     └───────────────────┘     └────────────────┘     └───────────────────┘     └──────────────┘
```

1. **AI Decides**: The conversational reasoning engine interprets user intent and plans the necessary operations.
2. **Action Identified**: The action planner categorizes the operations (Read-only, State modification, or Destructive).
3. **Risk Check**: If an operation involves destructive changes, sensitive data, or financial transactions, it is flagged as **High Risk**.
4. **User Confirmation**: J.A.R.V.I.S. pauses execution and asks the user for explicit verbal or interactive UI confirmation before proceeding.
5. **Execute**: Only after explicit approval is granted is the system command dispatched.

---

## 🚫 Restricted & High-Risk Operations

The following operations strictly require human approval:

| Category | Action | Guardrail Policy |
| :--- | :--- | :--- |
| **File Deletion** | Deleting files or emptying Trash (`rm`, `trash`) | **Always Confirmation Required**: Files must be moved to Trash rather than permanently unlinked. |
| **Outbound Messaging** | Sending emails, Slack/Discord messages, SMS | **Draft First**: JARVIS prepares the draft and presents it for review before sending. |
| **Financial / Purchases** | Online shopping, credit card submission, payments | **Blocked by Policy**: JARVIS is not authorized to submit payment forms or make purchases. |
| **System Modification** | Modifying `sudo`, editing `/System` or `/Library` | **Strictly Forbidden**: JARVIS operates only within the user's unprivileged user space. |
| **Credential Access** | Reading keychain, passwords, or private SSH keys | **Strictly Forbidden**: JARVIS will refuse any instruction to read or exfiltrate private credentials. |
| **Background Automation** | Autonomous camera or microphone monitoring | **Visual HUD Indicator**: Arc Reactor pulses with a visual status light whenever active. |

---

## 🛑 Emergency Stop

You can interrupt or cancel any ongoing action immediately at any moment by:
- Saying: *"Jarvis, stop"* or *"Cancel"*
- Pressing `Esc` or clicking the Arc Reactor HUD icon.
