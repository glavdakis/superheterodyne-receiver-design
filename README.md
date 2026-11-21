# Analysis and Synthesis of Radio Systems – Project

This repository contains the design and analysis of a **multi-channel superheterodyne receiver** for the **Analysis and Synthesis of Radio Systems** course at ECE AUTH during the 2025-2026 academic year.

**Author:** Georgios Lavdakis

## Overview

The receiver covers **10 channels of 10 MHz** at

$$f_{RF} = 2355 + 10i \ \text{MHz}, \quad i = 0, \dots, 9 \quad (2355 - 2445\ \text{MHz})$$

and uses two mixing stages:

```
Antenna → LNA → BPF1 → Mixer 1 → SAW (IF = 280 MHz) → Amp2 → Mixer 2 → LPF → A/D
                          ↑                                     ↑
                      f_LO1 (PLL1)                         f_LO2 (PLL2)
```

- **PLL1** synthesizes $f_{LO1} = 2075 + 10i$ MHz. VCO1 output is divided by 4, down-converted
  with a fixed $f_L = 513.75$ MHz (from a second loop with VCO2) and divided by a
  programmable divider $M = 2 + i$ against $f_{ref1} = 2.5$ MHz.
- **PLL2** synthesizes the fixed $f_{LO2} = 280$ MHz with a ÷4 feedback divider ($f_{ref3} = 70$ MHz).
- The low IF places all image frequencies ($1795 - 1885$ MHz) outside the BPF1 passband.

### Main results

| Quantity | Value |
|---|---|
| Total gain $G_{total}$ | 49.8 dB |
| Noise figure $F_{cas}$ | 1.26 dB |
| Minimum detectable signal (MDS) | −102.7 dBm |
| Input 1 dB compression point $P_{in,1dB}$ (due to Amp2) | −42.3 dBm |
| Dynamic range $DR_{1dB}$ | 60.4 dB |
| Equivalent $IIP_3$ (due to Mixer 2) | −37.3 dBm |
| SFDR | 43.6 dB |
| A/D input range (16 bit, 5 V, 50 Ω) | −72 dBm … 24 dBm |
| Minimum input power (SNR ≥ 10 dB) | −92.7 dBm |
| Maximum input power (SIR ≥ 20 dB) | −47.3 dBm |

## Repository structure

```
.
├── docs/
│   ├── report.pdf                         # Project report
│   ├── Components - Links - everythingRF.pdf  # Component search links (course material)
│   └── ΑΣΡΣ - Εκφώνηση Εργασίας.pdf       # Assignment description (in Greek)
├── datasheets/                            # Datasheets of the selected components
│   └── All_Datasheets.pdf                 # All datasheets merged in one file
└── README.md
```

## Components

All components were selected from [everythingRF](https://www.everythingrf.com) (and TI for the
programmable divider). The full list of links is in Section 4 of the report.

| Block | Part | Block | Part |
|---|---|---|---|
| LNA | MITEQ AFD3-020025-12 | VCO1 | Dynamic Engineers VCO1212BQ |
| BPF1 | Echo Microwave EMA8J2400P100G30D | VCO2 | Pasternack PE1V31016 |
| Mixer 1 | Crane DTG-2B-1250-SQ | VCO3 | Z-Comm V200ME01-LF |
| SAW Filter | Anatech AM280S813 | Phase detector | Mini-Circuits ZRPD-1+ |
| Amp2 | Wenteq ALN0035-29-4006 | Prescaler / fixed dividers | Fairview FMFD4004 |
| Mixer 2 | Lorch FC-7-2-1200 | Programmable divider | TI CD74HC4059 |
| LPF | KR Electronics 2378 | LPF1 / LPF2 / LPF3 / LPF4 | LPF-B0R5+ / AE6L8839 / KR 2416-100 / PLP-7-75+ |
| A/D | Analog Devices AD4008 | Crystals | Bomar BC11, JB2, Croven CR141-U |
