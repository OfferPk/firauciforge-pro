# FiRaUCIForge Pro (v1.0.0)

### FiRa Consortium & IEEE 802.15.4z Ultra-Wideband (UWB) Command Interface (UCI) Protocol Studio, DS-TWR / AoA Distance Vector Synthesizer & 10-Point Normative Zero-Trust Compliance Auditor

[![FiRa Consortium](https://img.shields.io/badge/FiRa%20Consortium-UCI%20v1.1%2Fv2.0-blue.svg)](https://www.firaconsortium.org/) [![IEEE Standard](https://img.shields.io/badge/IEEE-802.15.4z--2020%20HRP-blueviolet.svg)](https://standards.ieee.org/) ![Zero Dependencies](https://img.shields.io/badge/Dependencies-Zero-brightgreen.svg) ![Automated Tests](https://img.shields.io/badge/Tests-10%2F10%20Passing-success.svg)

---

## 1\. Executive Summary

**FiRaUCIForge Pro** is an industrial-grade protocol engineering studio, Double-Sided Two-Way Ranging (DS-TWR) distance calculation engine, and zero-trust verification suite for the **FiRa Consortium UWB Command Interface (UCI)** and **IEEE 802.15.4z High-Rate Pulse (HRP) PHY**.

Built specifically for automotive digital key engineers (Car Connectivity Consortium CCC Digital Key Release 3/4), smart lock developers (Apple Home Key, Aliro, ASSA ABLOY), mobile IoT architects, and hardware cybersecurity testing labs, FiRaUCIForge Pro eliminates the friction of designing, simulating, and auditing raw SPI/UART packets across NXP Trimension (NCJ29D5/SR150), Qorvo (DW3000/DW3110), Apple U1/U2, and STMicroelectronics (STM32UWB) silicon without needing \$50,000+ proprietary RF hardware benches.

---

## 2\. Key Architecture & Protocol Capabilities

### 2.1 Standard 4-Byte UCI Packet Framing

* Full support for FiRa UCI v1.1 and v2.0 message structures:  
  - **Message Types (MT):** Command (`001b`), Response (`010b`), Notification (`011b`), Data (`000b`).  
  - **Packet Boundary Flag (PBF):** Segmented vs complete framing.  
  - **Group Identifiers (GID):** Core (`0x00`), Session Configuration (`0x01`), Ranging Control (`0x02`), RF Testing (`0x0E`), Vendor Proprietary (`0x0F`).  
  - **Opcode Identifiers (OID):** `CORE_DEVICE_RESET`, `SESSION_INIT`, `SESSION_SET_APP_CONFIG`, `RANGE_START`, `RANGE_STOP`, and `RANGE_DATA_NTF`.

### 2.2 Double-Sided Two-Way Ranging (DS-TWR) Engine

* Nanosecond-precision Time-of-Flight calculation eliminating clock drift: \$\$\\text{ToF} \= \\frac{T\_{\\text{round1}} \\cdot T\_{\\text{round2}} \- T\_{\\text{reply1}} \\cdot T\_{\\text{reply2}}}{T\_{\\text{round1}} \+ T\_{\\text{round2}} \+ T\_{\\text{reply1}} \+ T\_{\\text{reply2}}}\$\$  
* Antenna propagation delay compensation (\$t\_{\\text{ant\_delay}}\$) with centimeter distance resolution (\$d \= c \\cdot \\text{ToF}\_{\\text{cal}}\$).

### 2.3 Angle of Arrival (AoA) Phase Vector Model

* Converts Phase Difference of Arrival (PDoA) into hemispherical Azimuth angles: \$\$\\theta \= \\arcsin\\left(\\frac{\\Delta \\phi \\cdot \\lambda}{2\\pi \\cdot d\_{\\text{ant}}}\\right)\$\$  
* Covers Worldwide UWB Channels: Channel 5 (\$6489.6\\text{ MHz}\$, \$\\lambda \= 46.2\\text{ mm}\$) and Channel 9 (\$7987.2\\text{ MHz}\$, \$\\lambda \= 37.5\\text{ mm}\$).

### 2.4 10-Point Normative Zero-Trust Compliance Auditor

Automatically audits packet byte streams against strict standards:

1. **RULE-01 (UCI Header Envelope):** \$\\text{MT} \\le 3\$, \$\\text{PBF} \\in {0, 1}\$, Reserved octet \$= 0x00\$.  
2. **RULE-02 (GID & OID Standard Taxonomy):** Verifies GID/OID against FiRa Technical Specification registries.  
3. **RULE-03 (Payload Length Symmetry):** Header declared length matches payload octets.  
4. **RULE-04 (Session ID Integer Envelope):** Validates non-zero 32-bit session ID.  
5. **RULE-05 (UWB RF Channel Regulatory Boundary):** Channel \$\\in {5, 6, 8, 9}\$ within spectrum masks.  
6. **RULE-06 (Slot Duration & Timing Budget):** Validates slot duration \$\\ge 1200\\text{ }\\mu\\text{s}\$.  
7. **RULE-07 (STS Cryptographic Mode Anti-Relay):** Enforces Dynamic STS (`0x02`) for relay resistance.  
8. **RULE-08 (DS-TWR Verification):** Validates Two-Way Ranging measurement modes.  
9. **RULE-09 (Angle of Arrival Angular Limits):** Enforces physical \$-90^\\circ \\le \\text{AoA} \\le \+90^\\circ\$ bounds.  
10. **RULE-10 (High-Impact State Modification):** Flags disruptive reset/deinit commands.

---

## 3\. Directory Layout

product\_306/

├── README.md                                \# Master product documentation

├── test\_firauci.py                          \# Automated 10-test verification suite

├── source-code/

│   ├── index.html                           \# Multi-tab responsive Web Studio

│   ├── uci.css                              \# Modern dark theme stylesheet

│   ├── uci-engine.js                        \# Core protocol framing & TWR/AoA engine

│   ├── uci-auditor.js                       \# 10-point normative zero-trust auditor

│   └── app.js                               \# Interactive UI controller

├── build/

│   ├── firauci-cli.py                       \# Zero-dependency Python 3 CLI runner

│   └── firauci-pro-v1.0.0.zip               \# Complete production distribution package

├── documentation/

│   ├── ARCHITECTURE.md                      \# Low-level protocol architecture deep dive

│   ├── USER\_GUIDE.md                        \# Operator manual for Web Studio & CLI

│   └── MONETIZATION\_AND\_MARKETING\_PLAYBOOK.md \# B2B commercialization and GTM plan

└── screenshots/

    └── firauci-studio-preview.svg           \# Vector UI & architecture preview diagram

---

## 4\. Quickstart & CLI Verification

### Run Automated Unit Tests (10/10 Verification)

python3 test\_firauci.py

### CLI Command Synthesis

\# Synthesize Core Device Reset

python3 build/firauci-cli.py cmd \--name reset

\# Synthesize Session Init

python3 build/firauci-cli.py cmd \--name session\_init

### CLI DS-TWR Distance & AoA Calculation

python3 build/firauci-cli.py twr \--r1 250.0 \--rep1 200.0 \--r2 240.0 \--rep2 190.0 \--ant\_delay 1.5 \--pdoa 45.0

### CLI Protocol Dissection & Zero-Trust Audit

python3 build/firauci-cli.py dissect "21 03 00 0f 01 00 00 00 03 04 01 09 08 02 b0 04 0e 01 02"

python3 build/firauci-cli.py audit "21 03 00 0f 01 00 00 00 03 04 01 09 08 02 b0 04 0e 01 02"

---

## 5\. Commercial Licensing & Pricing

* **Community Edition (Open Source):** Web Studio with basic UCI packet builder & manual dissection.  
* **Professional Single-Seat (\$199/year or \$399 perpetual):** Full Web Studio, complete standalone Python CLI suite, full DS-TWR & AoA modeling, C firmware array exporter, 10-point normative auditor.  
* **Hardware Team License (\$1,290/year, up to 10 seats):** Automated CI/CD test harness, batch SPI/UART log dissector, priority support.  
* **Enterprise / Silicon OEM (\$4,990/year):** Source code escrow, custom silicon vendor extensions (NXP, Qorvo, ST, Apple), air-gapped deployment, tailored CCC profiles.