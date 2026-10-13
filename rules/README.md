# JLCPCB rule pack

**JLCPCB DRC rules and CAM jobs for 2, 4, 6 and 8-layer boards — for Fusion Electronics and EAGLE 9.**

Part of [dmxON JLC Rules](../README.md) · **dmxON by AlexSmith 2026** · [license](../LICENSE.md)

> The easiest way is not to install the files by hand but to run the `dmxON_JLC_Setup.ulp` setup: it detects the board layers, picks the JLCPCB stack-up for any thickness and copper, loads the rules, checks the board and shows a summary. See the [README](../README.md#quick-start).

---

## What is inside

| File | What it is |
|---|---|
| `dmxON_JLCPCB_2L_Standard.dru` … `8L_Standard.dru` | **Standard** — with margin, no extra cost. Recommended for most boards. |
| `dmxON_JLCPCB_2L_Dense.dru` … `8L_Dense.dru` | **Dense** — at the limit of what JLCPCB makes without surcharge. |
| `dmxON_JLCPCB_2L_Extreme.dru` … `8L_Extreme.dru` | **Extreme** — the JLCPCB absolute minimum; some values cost extra. |
| `dmxON_JLCPCB_2L.cam` … `8L.cam` | CAM jobs: Gerber RS-274X and Excellon with JLCPCB file names (GTL, G1…, GBL, GTS, GBS, GTP, GBP, GTO, GBO, GKO, XLN). |

The rule files assume a **1.6 mm board, 1 oz outer and 0.5 oz inner copper, tented vias, regular routing**. For another thickness, 2 oz copper, a V-cut panel or untented vias the setup writes its own file with the exact JLCPCB stack-up. Each `.dru` carries its description in English, Russian, Spanish, German and Polish — Fusion shows the one matching its interface language.

---

## Values

All sizes in millimetres.

| mm | 2 layers Standard | 4–8 layers Standard | 2 layers Dense | 4–8 layers Dense | 2 layers Extreme | 4–8 layers Extreme |
|---|---|---|---|---|---|---|
| Track and space | 0.127 | 0.127 | 0.10 | 0.10 | 0.10 | 0.09 ¹ |
| Pad to pad, different nets | 0.15 | 0.15 | 0.15 | 0.15 | 0.10 | 0.09 |
| Via drill / diameter | 0.3 / 0.45 | 0.3 / 0.45 | 0.3 / 0.40 | 0.3 / 0.40 | 0.15 / 0.25 ² | 0.15 / 0.25 ² |
| Via ring, inner layers | — | 0.08 | — | 0.10 | — | 0.11 |
| PTH ring | 0.25 | 0.20 | 0.18 | 0.15 | 0.18 | 0.15 |
| PTH ring, inner layers | — | 0.20 | — | 0.20 | — | 0.21 |
| Min drill | 0.3 | 0.3 | 0.3 | 0.3 | 0.15 ² | 0.15 ² |
| Copper to edge | 0.30 | 0.30 | 0.25 | 0.25 | 0.20 | 0.20 |
| Hole to hole | 0.25 | 0.25 | 0.20 | 0.20 | 0.20 | 0.20 |
| Mask expansion | 0.05 | 0.05 | 0.05 | 0.05 | 0.05 | 0.05 |
| Tented vias up to | 0.5 | 0.5 | 0.5 | 0.5 | 0.5 | 0.5 |

¹ 3–3.5 mil tracks on multilayer boards — **+20 %** price.
² Holes under 0.3 mm cost extra; choose **Min via hole size** on the order page.

**Why the inner ring is larger.** On inner layers JLCPCB needs 0.20 mm from a via hole and 0.30 mm from a pin hole to foreign copper; the rules get there through the ring so the normal clearance stays the same.

**2 oz copper.** Track and space 0.20 (Standard), 0.16 on 2 layers and 0.15 on multilayer boards (Dense and Extreme); PTH ring 0.26; mask dam from 0.20.

**Mask dam** between pads: 0.10 mm for green, red, yellow, blue and purple, 0.13 mm for white and black.

**V-cut.** On a V-cut panel copper must stay at least 0.4 mm from the edge — the setup has a checkbox for it.

---

## Stack-ups, 1.6 mm

JLCPCB default stack-ups («No requirement» on the order page), 1 oz outer and 0.5 oz inner copper. Inner copper after processing is 0.0152 mm.

| Layers | Rule stack | Dielectrics top to bottom, mm | Total |
|---|---|---|---|
| 2 | `(1*16)` | core 1.53 | 1.60 |
| 4 | `(1+2*15+16)` | prepreg 7628 0.2104 · core 1.065 · prepreg 7628 0.2104 | 1.586 |
| 6 | `(1+2*3+14*15+16)` | 3313 0.0994 · core 0.55 · 2116 0.1164 · core 0.55 · 3313 0.0994 | 1.546 |
| 8 | `(1+2*3+4*13+14*15+16)` | 2116 0.1164 · core 0.30 · 1080×2 0.1528 · core 0.30 · 1080×2 0.1528 · core 0.30 · 2116 0.1164 | 1.600 |

`+` is prepreg, `*` is core. Fusion builds the physical board stack (Layer Stack Manager) from these numbers, so the 3D and Gerber job thickness matches the order. The setup knows every JLCPCB stack-up for 4, 6 and 8 layers, 0.8–2.0 mm, 1–2 oz copper — [docs/STACKUPS.md](../docs/STACKUPS.md).

---

## Manual installation

**Rules.** Fusion: **DRC → Load…** (or the `DRC LOAD 'path/file.dru'` command), then **DRC**. EAGLE 9: **Tools → DRC → File → Load…**. After `INSTALL.ulp` the pack is already listed in Fusion's design-rules folder.

**CAM job.** **Manufacturing → CAM Processor → Load job file** → `dmxON_JLCPCB_<N>L.cam` → **Process Job**. Inner layer numbers in the job follow the stack above (6 layers: 2, 3, 14, 15). If the board uses other numbers, the setup writes a job for them.

> [**dmxON FabKit**](https://github.com/AlexSmith2025/dmxON-FabKit-Fusion-Electronics) produces Gerber itself (JLCPCB names and zip) — the CAM job is only needed for manual export.

---

## Where the values come from

- JLCPCB capabilities: <https://jlcpcb.com/capabilities/pcb-capabilities>
- Extra charges: <https://jlcpcb.com/help/article/In-what-cases-will-there-be-charged-extra>
- Stack-ups and Er: the JLCPCB impedance calculator, <https://jlcpcb.com/impedance>

Values checked on 2026-10-09. JLCPCB changes capabilities and prices from time to time — check their page and the DFM report before ordering.
