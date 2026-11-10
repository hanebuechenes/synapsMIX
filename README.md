# synapsMIX — 4-Channel Analog VCA & Mixer (Eurorack)

**synapsMIX** is a compact, high-performance 4-channel analog VCA and summing sub-mixer for the Eurorack modular synth format.

## ⚡ Overview & Features

* **4 Independent VCAs:** Built around dual **LM13700** Operational Transconductance Amplifiers (OTAs) for linear CV response and clean signal amplification.

* **Low-Noise Master Summing:** Integrated summing bus routed through a **TL074** quad operational amplifier stage with manual output level control.

* **Per-Channel Visual Monitoring:**

  * **Audio In LEDs:** Antiparallel diode-protected (`1N4148W`) indicators for active signal detection on every channel.

  * **VCA Level LEDs:** Direct envelope/CV brightness feedback on each VCA control channel.

  * **Master Out LED:** Antiparallel-protected LED monitoring output audio level.

* **Eurorack Power Section:** Standard 10-pin power header with polarity protection, ferrite beads, and high/low-frequency decoupling capacitors.

## 🎛️ Signal Architecture

```
                               ┌─────────────────┐
[ Audio In 1 ] ──► [ VCA 1 ] ──┤                 │
[ Audio In 2 ] ──► [ VCA 2 ] ──┤  SUM_BUS (U3)   ├──► [ Master Vol ] ──► [ Master Out ]
[ Audio In 3 ] ──► [ VCA 3 ] ──┤ (TL074 Buffer)  │                           │
[ Audio In 4 ] ──► [ VCA 4 ] ──┤                 │                      (D11/D10 LED)
                               └─────────────────┘
      ▲                ▲
 [ CV In 1..4 ]   [ Trimmers ]

```

## 🛠️ Circuit Breakdown & Critical Design Notes

### 1. VCA & CV Control Stage (LM13700)

* **Control Input:** Accepts standard $+5\text{V}$ to $+10\text{V}$ envelopes/LFOs via `CVin1..4`.

* **CV LED Driver:** `D9` (and equivalents) tapped directly at `CVin` node with a $1\text{ k}\Omega$ current-limiting resistor (`R30`), returning to `GND`.

### 2. Audio Inputs & Antiparallel Indicators

* Audio input jacks feature antiparallel diode pairs (Standard LED + `1N4148W`) across the signal path to prevent reverse bias voltage breakdowns and visually reflect AC signal polarity.

### 3. Master Output & Buffer (TL074)

* Summed signals feed into `U3B` (TL074).

* The output path features an output protection resistor (`R28`, $1\text{ k}\Omega$) and an antiparallel-protected output LED (`D11` / `D10`).

* **Pin Orientation:** `D11` Anode points down to TL074 Output (Pin 7) via `R31`; Cathode connects to `GND`. `D10` (`1N4148W`) is placed antiparallel.

## 📄 License

This hardware design is released under the **MIT License**.