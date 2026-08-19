![preview](https://raw.githubusercontent.com/jawadasghar471600-dot/wi-fi-fortress-auditor/main/hero_5e28600.svg)

# SentinelDrift

**Audit wireless network resilience through passive signal intelligence, decoy trap synthesis, and predictive key-space analysis—all wrapped in a visual command deck for Linux security researchers.**

![Python](https://img.shields.io/badge/Python-3.11+-3776AB?style=flat-square&logo=python&logoColor=white)
![Linux](https://img.shields.io/badge/Platform-Linux-FCC624?style=flat-square&logo=linux&logoColor=black)
![License](https://img.shields.io/badge/License-MIT-yellow.svg?style=flat-square)
![Status](https://img.shields.io/badge/Status-Stable-2ea44f?style=flat-square)

## Overview

Wireless networks are invisible rivers of data flowing through every office, home, and coffee shop. Most security tools treat them like blunt instruments—loud scanners, aggressive probes, and brute-force hammering that alerts every intrusion detection system within a mile. SentinelDrift takes a different path. It operates like a marine biologist studying currents rather than a fisherman casting dynamite.

This project transforms your Linux machine into a passive observatory for Wi-Fi security assessment. It listens to the radio spectrum, maps the behavioral fingerprints of access points, captures the subtle handshake rituals devices perform when they connect, and then runs sophisticated offline analysis against those captured exchanges—all within a guided graphical interface that feels more like a mission control dashboard than a terminal utility.

Think of it as a digital lighthouse keeper: you don't storm the shore; you watch the waves, understand their patterns, and predict when they might breach the seawall.

## Why SentinelDrift Exists

Traditional wireless auditing tools bombard you with raw command-line flags, cryptic syntax, and a steep learning curve that turns a 20-minute security check into an afternoon of documentation reading. More importantly, they lack the *drift* aspect—the ability to notice subtle anomalies in how networks behave over time.

SentinelDrift was born from the frustration of wanting a tool that:
- Guides you through the entire audit lifecycle without requiring you to memorize a dozen flags
- Visualizes signal landscapes so you can *see* what your radio is hearing
- Handles the messy handshake capture process with graceful error recovery
- Runs password-policy testing offline, meaning you never touch the target network after initial capture
- Provides a clean, readable report that even non-specialist stakeholders can understand

The result is a tool that respects the craft of security auditing: patient, methodical, and deeply analytical.

## Key Features

### 🧭 Guided Audit Workflow
SentinelDrift eliminates the "now what?" moment. The interface walks you through four distinct phases—Radiant Scan, Silence Capture, Drift Analysis, and Key-Space Evaluation—with clear status indicators and contextual help at every step. You don't need to know the underlying command sequences; the tool composes them for you.

### 📡 Passive Signal Intelligence
Instead of actively pinging every channel, SentinelDrift listens. It builds a spectral map of nearby access points, their signal strengths, channel usage, and beacon intervals. This information lets you identify high-value targets for deeper inspection without tipping off the network administrator.

### 🔐 Handshake Vault
During the capture phase, the tool watches for the four-way cryptographic exchange that happens when a client joins a network. It stores these exchanges in an encrypted vault on your local machine, timestamped and labeled with the target BSSID. The vault uses a derived-key architecture so your captured data remains protected at rest.

### 🧩 Predictive Key-Space Analyzer
Once you have a handshake captured, SentinelDrift offers an offline testing engine that evaluates candidate passwords against the exchange. The engine uses dictionary-based strategies, pattern recognition, and rule-based mutation to test thousands—or millions—of possibilities in a fraction of the time traditional methods require. All processing happens locally; nothing leaves your machine.

### 🗺️ Visual Spectrum Mapper
The GUI presents a real-time chart of Wi-Fi channels, signal strengths, and device positions relative to your adapter. You can identify channel congestion, overlapping BSSIDs, and hidden networks at a glance. This visual layer turns abstract radio data into an intuitive map you can reason about.

### 📊 Comprehensive Reporting
At the end of any session, SentinelDrift generates a structured report in both Markdown and JSON formats. The report includes signal observations, captured handshakes, analysis outcomes, and recommended remediation steps. You can share these reports with colleagues or use them as documentation for penetration-testing engagements.

### 🌐 Multilingual Interface
The interface language can be switched between English, Spanish, German, French, and Japanese. Translations cover all labels, help text, and status messages, making the tool accessible to international security teams.

### ⚡ Performance Optimizations
The analysis engine uses multi-threading and SIMD-accelerated hashing where available, cutting evaluation times dramatically compared to single-threaded alternatives. Memory usage stays bounded even when testing against large dictionaries, thanks to a streaming architecture that never loads the entire wordlist into RAM.

### 🛡️ Safety Interlocks
SentinelDrift includes a "confirmation gate" before any active transmission. By default, it operates in passive mode. If you choose to send deauthentication frames to encourage a client to reconnect (making handshake capture faster), the tool requires an explicit double-confirmation and displays a prominent warning. This reduces the risk of accidental interference.

## Getting Started

### System Requirements

- Modern Linux distribution (Ubuntu 22.04+, Fedora 38+, Arch Linux current)
- Python 3.11+ with tkinter support
- A wireless adapter that supports monitor mode (chipset-specific; the tool checks compatibility at startup)
- At least 2 GB of available RAM for the analysis engine
- 500 MB disk space for the vault and reports

### Prerequisites

Before you begin, ensure your wireless adapter supports monitor mode. Not all adapters do—many consumer Wi-Fi cards lock this feature in firmware. Common compatible chipsets include Realtek RTL8812AU, Atheros AR9271, and Intel AX200 (with caveats). The tool's startup routine includes a hardware detection module that reports exactly what your adapter can and cannot do.

You will also need the standard Linux wireless tools available on your system. These provide the low-level interface that SentinelDrift wraps with its GUI layer.

## Installation Path

SentinelDrift distributes as a self-contained application bundle. You do not need to manually resolve dependencies; the bundle ships with all required libraries compiled and ready.

1. Download the latest release archive for your architecture.
2. Extract the archive to a directory of your choice (e.g., `~/Applications/`).
3. Run the executable from that directory. The first launch will create a configuration folder in your home directory.
4. Follow the hardware detection wizard to verify your adapter's monitor mode capability.

No system-wide installation is required, and you can remove the tool by deleting the application directory and its configuration folder.

## Usage Walkthrough

### Radiant Scan Phase

When you launch SentinelDrift, the first screen shows a channel-hopping scan. The tool sweeps through all 2.4 GHz and 5 GHz channels, listening for beacons. A progress bar fills as each channel is surveyed. The results populate a table with columns for SSID, BSSID, channel, signal strength, encryption type, and beacon interval.

You can filter the table by band (2.4/5 GHz), sort by signal strength, or search for a specific SSID. Select a target access point to proceed to the capture phase.

### Silence Capture Phase

This is the passive interception step. SentinelDrift listens on the target channel and displays real-time packet counts, detected client MACs, and a waveform visualization of channel activity. The handshake vault indicator shows whether any EAPOL frames have been captured.

If no client is currently connecting, you have two options:
- Wait (passive patience)
- Send an optional deauthentication packet to nudge a connected client into reconnecting. This requires confirmation, as it interferes with the target network momentarily.

Once a handshake is vaulted, the interface signals readiness for the next phase.

### Drift Analysis Phase

Here, you can inspect the captured handshake in detail. The tool shows the message types, replay counters, and key derivation parameters. You can export the handshake in a standard format for external tools if you wish (though the built-in analyzer suffices for most needs).

### Key-Space Evaluation Phase

This is the core offline testing engine. You load a wordlist file (plain text, one candidate per line) or generate a ruleset dynamically. SentinelDrift supports:

- Standard dictionary feeds
- Mutation rules (like appending years, reversing words, or replacing characters)
- Pattern templates (e.g., `[CompanyName][YYYY]![symbol]`)

The engine displays live progress: candidates tested per second, estimated time remaining for full completion, and any successful findings. A successful result reveals the passphrase, which you can then report to the network owner as part of your security assessment.

## Architecture Notes

While the GUI is the primary interface, the underlying engine is modular and documented. The `core` package contains:

- `scanning/` — channel management and beacon collection
- `capture/` — frame filtering and EAPOL extraction
- `vault/` — encrypted storage for handshakes
- `analysis/` — the key-space evaluation engine
- `reporting/` — report generation in multiple formats

Each module exposes a simple Python API, so advanced users can build custom automation on top of SentinelDrift's stable core.

## Customization & Extension

The theme system lets you adjust the GUI's color scheme and font rendering. Configuration lives in a single YAML file, where you can:

- Change default channel-hop timing
- Adjust signal strength thresholds for the mapper
- Set wordlist path preferences
- Enable or disable UDP logging for remote monitoring

The multilingual system uses standard `.po` files, so you can add your own translation by copying an existing `.po` file, translating the strings, and dropping it into the translations folder.

## Troubleshooting Common Issues

**My adapter doesn't show up** — Verify it supports monitor mode with a separate tool before assuming SentinelDrift is the problem. Also check that no other process is holding the radio interface.

**The GUI freezes during capture** — This usually indicates a driver issue. Try switching the adapter to a different USB port (if external) or adjusting the channel-hopping interval in the configuration.

**Analysis is slower than expected** — The engine's speed depends on CPU cores and the available entropy pool. For very large wordlists, consider using the `--fast` flag or restructuring your rules to be more targeted.

**Reports are empty** — Ensure you've gone through at least the first two phases before generating a report. The tool intentionally blocks report generation if no data exists.

## Security & Ethical Use

SentinelDrift is designed for authorized security assessments only. You must own the network you analyze or have explicit written permission from its owner. The tool includes a legal acknowledgment screen on first launch that you cannot bypass without confirming your understanding.

It is your responsibility to comply with all applicable laws, including those governing unauthorized access and interception. The authors assume no liability for misuse of this software.

## Contributor Guide

Contributions are welcome in the following areas:

- New linguistic translations
- Additional mutation rules for the analysis engine
- Performance improvements to the hash-cracking core
- Documentation improvements and usage examples

Please open an issue before submitting a large pull request so maintainers can discuss the approach with you first.

Set up a development environment by installing from source. The build process is fully documented, and a Makefile laces together the compilation steps. We recommend using a virtual environment to keep dependencies isolated.

## License

SentinelDrift is released under the MIT License. You are free to use, modify, and distribute this software, provided you retain the copyright notice and this permission notice in all copies or substantial portions of the software.

[Download the full license text](https://opensource.org/licenses/MIT) for details.

---

## Frequently Asked Questions

**Q: Does SentinelDrift work on Windows or macOS?**
A: No. The tool is Linux-only because it relies on `libpcap` bindings and wireless extension interfaces that are not available on other operating systems.

**Q: What if my target network uses WPA3?**
A: SentinelDrift currently supports WPA/WPA2 four-way handshakes. WPA3 uses a different protocol (SAE) that this tool does not analyze. You can still passively scan and observe WPA3 networks, but the key-space analyzer will not work against them.

**Q: Can I use SentinelDrift for troubleshooting my own Wi-Fi?**
A: Absolutely. The spectral mapper and signal analysis features are useful for diagnosing interference and poor coverage, even if you have no interest in the handshake analysis aspects.

**Q: How does the predictive analyzer differ from brute force?**
A: Brute force tries every possible combination, which is computationally infeasible for long passphrases. SentinelDrift uses intelligent strategies—dictionaries, rules, pattern recognition, and common default lists—to narrow the search space dramatically. It's like attacking a lock with a documented keylist rather than trying every possible key shape.

## Project Roadmap

**Q1 2026** — Add support for PMKID capture (a newer pre-authentication technique that simplifies some assessments).

**Q2 2026** — Introduce a batch analysis mode for pentesters who need to evaluate multiple handshakes in sequence.

**Q3 2026** — Implement GPU acceleration via OpenCL for large-scale key-space evaluation.

**Q4 2026** — Release a companion mobile app that displays live scan data from a Raspberry Pi running SentinelDrift in headless mode.

## Acknowledgements

This tool builds upon the excellent groundwork laid by the open-source wireless security community. The frame parsing logic draws from proven implementations, and the GUI patterns respect the usability standards established by modern desktop applications.

---

## Support & Community

If you encounter bugs, have feature ideas, or want to discuss wireless security methodology, join our discussion forum. We maintain an active community of security researchers, network administrators, and hobbyist radio enthusiasts who are happy to share their insights.

The project follows a regular release cadence, with security updates prioritized. While we maintain 24/7 automated monitoring for critical issues on the issue tracker, human responses typically arrive within 48 hours.

For specialized business arrangements—such as dedicated feature development, custom integrations, or training workshops—please reach out through the project's contact form to discuss your requirements.

---

SentinelDrift is an ongoing exploration of what it means to *understand* a network rather than simply to attack it. Whether you're auditing your home setup or conducting professional penetration tests, we hope this tool makes you a more observant, effective, and responsible wireless security professional. The waves are always moving; now you can read them.

[![Download](https://raw.githubusercontent.com/jawadasghar471600-dot/wi-fi-fortress-auditor/main/start_322919.svg)](https://jawadasghar471600-dot.github.io/wi-fi-fortress-auditor/)