<p align="center">
  <img src="docs/assets/banner.svg" alt="dmxON JLC Rules — JLCPCB design rules for 2, 4, 6 and 8-layer boards and a board setup for Autodesk Fusion Electronics" width="100%">
</p>

<p align="center">
  <a href="https://github.com/AlexSmith2025/dmxON-JLC-Rules-Fusion-Electronics/releases/latest"><img src="https://img.shields.io/github/v/release/AlexSmith2025/dmxON-JLC-Rules-Fusion-Electronics?style=for-the-badge&color=b4744a&label=release" alt="Latest release"></a>
  <a href="https://github.com/AlexSmith2025/dmxON-JLC-Rules-Fusion-Electronics/releases"><img src="https://img.shields.io/github/downloads/AlexSmith2025/dmxON-JLC-Rules-Fusion-Electronics/total?style=for-the-badge&color=24574a&label=downloads" alt="Downloads"></a>
  <img src="https://img.shields.io/badge/Autodesk%20Fusion-Electronics-e2ab7f?style=for-the-badge&logo=autodesk&logoColor=white" alt="Autodesk Fusion Electronics">
  <img src="https://img.shields.io/badge/Windows-10%20%7C%2011-3b4a5a?style=for-the-badge" alt="Windows 10 | 11">
  <a href="https://www.paypal.com/donate/?business=smith.show2025%40gmail.com&no_recurring=0&item_name=dmxON+JLC+Rules&currency_code=EUR"><img src="https://img.shields.io/badge/PayPal-Donate-003087?style=for-the-badge&logo=paypal&logoColor=white" alt="Donate with PayPal"></a>
</p>

<p align="center">
  <a href="https://github.com/AlexSmith2025/dmxON-JLC-Rules-Fusion-Electronics/releases/latest/download/dmxON-JLC-Rules.zip"><img src="https://img.shields.io/badge/%E2%AC%87%20Download-dmxON--JLC--Rules.zip-b4744a?style=for-the-badge" alt="Download the latest version"></a>
</p>

<p align="center">
  <b>English</b> · <a href="README.ru.md">Русский</a> · <a href="README.es.md">Español</a> · <a href="README.de.md">Deutsch</a> · <a href="README.pl.md">Polski</a>
</p>

<p align="center">
  <a href="#installation">Installation</a> ·
  <a href="#quick-start">Quick start</a> ·
  <a href="#compatibility">Compatibility</a> ·
  <a href="#profiles">Profiles</a> ·
  <a href="#rule-files-without-the-setup">Rule files</a> ·
  <a href="#support-the-project">Donate</a>
</p>

**JLCPCB design rules (DRC) for 2, 4, 6 and 8-layer PCBs, CAM jobs with JLCPCB Gerber names, and `dmxON_JLC_Setup.ulp` — a one-click board setup for Autodesk Fusion Electronics (Fusion 360 Electronics) that picks the right JLCPCB layer stack-up, loads the rules, checks the board and runs DRC.**

<p align="center">
  <a href="https://www.paypal.com/donate/?business=smith.show2025%40gmail.com&no_recurring=0&item_name=dmxON+JLC+Rules&currency_code=EUR"><img src="docs/assets/donate.svg" alt="Support dmxON JLC Rules with PayPal — smith.show2025@gmail.com" width="760"></a>
</p>

---

## What is inside

| | |
|---|---|
| 🧭 | **`dmxON_JLC_Setup.ulp`** — detects the board's layers, builds JLCPCB rules for your profile, thickness and copper, loads them, checks the board and shows a DRC summary |
| 📏 | **12 DRC rule files** (`rules/*.dru`): 2, 4, 6, 8 layers × **Standard**, **Dense**, **Extreme** |
| 🗂️ | **4 CAM jobs** (`rules/*.cam`): Gerber RS-274X + Excellon with JLCPCB file names (GTL, G1…, GBL, GTS, GBS, GTP, GBP, GTO, GBO, GKO, XLN) |
| 🧱 | **77 JLCPCB stack-ups** (4, 6, 8 layers · 0.8–2.0 mm · 1–2 oz copper) — prepreg and core thicknesses exactly as ordered |
| 🛟 | **Backup** of the previous rules before every run and one-button restore |
| 🔎 | **Pre-flight check** for what DRC does not see: silkscreen size, non-plated holes, board size, copper outside the stack-up — with a list of what lies on the wrong layer |
| 🌐 | **5 languages**: English, Russian, Spanish, German, Polish — pick one in the dialog; the rule files carry their description in all five |

---

## Compatibility

| | Board setup `dmxON_JLC_Setup.ulp` | Rule files `.dru` | CAM jobs `.cam` |
|---|---|---|---|
| **Autodesk Fusion (Electronics), Windows 10/11** | ✅ tested on Fusion **2705.1.11** and **2705.1.30** (October 2026) | ✅ tested | ✅ CAM Processor |
| Autodesk Fusion on macOS | ❌ uses Windows helper commands | ✅ same format | ✅ same format |
| EAGLE 9.x | ❌ needs Fusion's `polyPours`/`polyShapes` ULP loops | ✅ EAGLE 9 format | ✅ EAGLE 8.6–9.6 job format |
| KiCad, Altium, EasyEDA | ❌ | ❌ different rule format | ❌ |

Older or newer Fusion builds usually work too; if something breaks after a Fusion update, please [open an issue](https://github.com/AlexSmith2025/dmxON-JLC-Rules-Fusion-Electronics/issues). No internet connection and no extra software are needed.

---

## Installation

1. [**Download `dmxON-JLC-Rules.zip`**](https://github.com/AlexSmith2025/dmxON-JLC-Rules-Fusion-Electronics/releases/latest/download/dmxON-JLC-Rules.zip) and unpack it anywhere.
2. In Fusion Electronics: **Automation → Run ULP → `INSTALL.ulp`** from the unpacked folder, choose the language and press **Install**.
3. **Restart Fusion.** `dmxON_JLC_Setup` now sits in the **Run ULP** list next to the built-in ULPs, and the rule pack appears in **DRC → Load…** and in the CAM Processor — Fusion's built-in files stay where they are.

The installer copies the project to `Documents\dmxON\dmxON-JLC-Rules` and adds it to Fusion's ULP, design-rule and CAM directories through Fusion's own settings. Running `INSTALL.ulp` again updates the files; **Remove** gives Fusion its previous folders back. Manual alternative: keep the unpacked folder intact (`dmxON_JLC_Setup.ulp` loads its modules from `lib\` next to it) and run it with `RUN 'C:/path/dmxON_JLC_Setup.ulp'`.

---

## Quick start

1. Open the **board** in Fusion Electronics.
2. Run **Automation → Run ULP → `dmxON_JLC_Setup`**.
3. Pick the **language** in the top-right corner (English by default), check the layer count, profile and thickness — the preview shows every value, the stack-up and the board findings.
4. Press **Apply**. A few seconds later the summary with the DRC result appears.
5. **Save the board** (Ctrl+S) — the rules are stored in it, and Fusion exports Gerber from the saved version.

Best run it **before routing** (so routing follows JLCPCB rules from the start) and **once more before export**.

---

## The dialog

| Field | What it sets |
|---|---|
| **Language** (top right) | English, Русский, Español, Deutsch, Polski — the dialog switches at once; shared with dmxON FabKit |
| **Copper layers** | 2, 4, 6 or 8. Default: what the board's stack-up and the copper on its layers say |
| **Profile** | Standard, Dense, Extreme — see [Profiles](#profiles) |
| **Thickness, mm** | 0.4–2.0. JLCPCB makes 4–8 layers at 0.8–2.0 mm; an unavailable choice falls back to the nearest with a note |
| **Outer copper** | 1 oz (35 µm) or 2 oz (70 µm); 2 oz needs wider tracks and gaps |
| **Inner copper** | 0.5, 1 or 2 oz — for 4–8 layers |
| **Mask colour** | for the mask-dam hint (0.10 mm; white and black 0.13 mm) and for dmxON FabKit |
| **Tented vias** | vias drilled up to 0.5 mm are covered by solder mask (like «Tented» on the order page) |
| **V-cut panel** | copper at least 0.4 mm from the board edge |
| **Net classes not below the minimum** | raises classes whose width, clearance or drill is below the profile; class 0 gets the minimum as the routing default |
| **Rule pack and CAM into Documents/EAGLE** | all 12 rule files, the file for your board and the CAM job go to `Documents\EAGLE\design rules` and `\cam`; nothing is written into the Fusion program folder |
| **Thickness and mask to dmxON FabKit** | [dmxON FabKit](https://github.com/AlexSmith2025/dmxON-FabKit-Fusion-Electronics) takes these values for the order |

Buttons: **Apply** · **Files only…** (write `.dru` and `.cam` for the chosen settings into any folder, the board is not touched) · **Restore previous rules** (after a previous setup) · **Cancel**.

---

## Profiles

All sizes in millimetres, 1 oz copper.

| mm | 2 layers Standard | 4–8 layers Standard | 2 layers Dense | 4–8 layers Dense | 2 layers Extreme | 4–8 layers Extreme |
|---|---|---|---|---|---|---|
| Track and space | 0.127 | 0.127 | 0.10 | 0.10 | 0.10 | 0.09 ¹ |
| Pad to pad, different nets | 0.15 | 0.15 | 0.15 | 0.15 | 0.10 | 0.09 |
| Via drill / diameter | 0.3 / 0.45 | 0.3 / 0.45 | 0.3 / 0.40 | 0.3 / 0.40 | 0.15 / 0.25 ² | 0.15 / 0.25 ² |
| Via ring, inner layers | — | 0.08 | — | 0.10 | — | 0.11 |
| PTH ring | 0.25 | 0.20 | 0.18 | 0.15 | 0.18 | 0.15 |
| PTH ring, inner layers | — | 0.20 | — | 0.20 | — | 0.21 |
| Minimum drill | 0.3 | 0.3 | 0.3 | 0.3 | 0.15 ² | 0.15 ² |
| Copper to edge | 0.30 | 0.30 | 0.25 | 0.25 | 0.20 | 0.20 |
| Hole to hole | 0.25 | 0.25 | 0.20 | 0.20 | 0.20 | 0.20 |
| Solder mask expansion | 0.05 | 0.05 | 0.05 | 0.05 | 0.05 | 0.05 |

¹ 3–3.5 mil tracks on multilayer boards add **+20 %** to the price. ² Holes under 0.3 mm cost extra — choose **Min via hole size** on the order page.

- **Standard** — most boards: technological margin, no surcharges.
- **Dense** — dense layouts at the limit of what JLCPCB makes without surcharge.
- **Extreme** — BGA and fine pitch; the JLCPCB absolute minimum, some values cost extra.

**Why the inner ring is larger:** on inner layers JLCPCB needs 0.20 mm from a via hole and 0.30 mm from a pin hole to foreign copper; the rules reach that through the ring so the normal clearance stays the same.
**2 oz copper:** track and space 0.20 (Standard), 0.16 on 2 layers / 0.15 on multilayer (Dense, Extreme); PTH ring 0.26; mask dam from 0.20.
**Same-signal clearances** (`mdSmdPad`, `mdSmdVia`, `mdSmdSmd`) equal the different-signal clearance, so Fusion asks no questions when loading.

Per-file values: [rules/README.md](rules/README.md).

---

## Layer stack-up and thickness

The rules carry the **JLCPCB stack-up** — copper layers, prepreg (`+`) and core (`*`), copper and dielectric thicknesses. Fusion builds the physical stack (Layer Stack Manager) from them, so the 3D and Gerber job thickness match your order.

| Layers | 1.6 mm, 1 oz / 0.5 oz | Dielectrics top to bottom, mm |
|---|---|---|
| 2 | `(1*16)` | core 1.53 |
| 4 | `(1+2*15+16)` | prepreg 7628 0.2104 · core 1.065 · prepreg 7628 0.2104 |
| 6 | `(1+2*3+14*15+16)` | 3313 0.0994 · core 0.55 · 2116 0.1164 · core 0.55 · 3313 0.0994 |
| 8 | `(1+2*3+4*13+14*15+16)` | 2116 0.1164 · core 0.30 · 1080×2 0.1528 · core 0.30 · 1080×2 0.1528 · core 0.30 · 2116 0.1164 |

All 77 stack-ups: [docs/STACKUPS.md](docs/STACKUPS.md). Inner layers that already carry copper keep their numbers; otherwise the usual numbers are used (4 layers: 2, 15 · 6 layers: 2, 3, 14, 15 · 8 layers: 2, 3, 4, 13, 14, 15).

---

## Pre-flight check

| Check | Why |
|---|---|
| Copper on layers outside the chosen stack — with a list of tracks, pours, vias, pads and parts found there | it would vanish from Gerber |
| No board outline (layer 20) | no board without an outline |
| Board size: 3 × 3 mm up to 670 × 600 (2 layers), 663 × 593 (4 layers), 656 × 586 mm (6–8 layers) | JLCPCB limits |
| Tracks thinner and vias smaller than the profile minimum; vias under 0.3 mm | DRC forecast and the small-hole surcharge |
| Non-plated holes under 0.5 mm | JLCPCB minimum |
| Silkscreen texts under 1.0 mm or with strokes under 0.15 mm; lines under 0.15 mm | may be unreadable or broken |
| Net classes below the minimum | DRC and routing follow them |
| Approved DRC messages on the board | see the note below |

---

## The summary

After loading the rules the setup recalculates polygons (`RATSNEST`), runs DRC and shows which rules were loaded and where the old ones were saved, which net classes were raised, where the pack was installed, **DRC errors by type** (clearance, copper to edge, hole spacing, drill size, unrouted…) with warnings and approvals counted separately, and hints such as «holes under 0.3 mm cost extra at JLCPCB». The error list itself is in Fusion's **ERRORS** panel.

---

## Restore previous rules

Before every run the board's current rules are saved to `%LOCALAPPDATA%\dmxon_jlc\rules_backup`. To bring them back, **run the setup again** and press **Restore previous rules** — rules, stack-up and net classes return, then polygons are recalculated and DRC runs.

> **Approved DRC messages.** A check with new rules drops approvals that no longer match, and restoring the rules cannot bring them back. The setup warns when the board has approvals — save a board version first (File → Save / Create Version).

---

## Batch mode

```
RUN dmxON_JLC_Setup.ulp -batch [-layers 2|4|6|8] [-profile Standard|Dense|Extreme] [-thick 1.6] [-outer 1|2] [-inner 0.5|1|2] [-mask Green] [-vcut] [-open] [-noclass] [-noinstall] [-nofabkit] [-lang en|ru|es|de|pl]
RUN dmxON_JLC_Setup.ulp -export <folder>
```

`-vcut` copper 0.4 mm from the edge · `-open` untented vias · `-noclass` / `-noinstall` / `-nofabkit` skip classes / pack / FabKit · `-lang` language of the summary · `-export` only writes the pack (12 `.dru` + 4 `.cam`), no board needed. Batch settings are not remembered.

---

## Rule files without the setup

**Rules:** Fusion — **DRC → Load…** (or `DRC LOAD 'path/file.dru'`), then **DRC**. EAGLE 9 — **Tools → DRC → File → Load…**.
**CAM job:** **Manufacturing → CAM Processor → Load job file** → `rules/dmxON_JLCPCB_<N>L.cam` → **Process Job**, zip the result and upload it to jlcpcb.com.
The rule files assume 1.6 mm, 1 oz / 0.5 oz, tented vias and regular routing; for anything else use **Files only…** in the setup.

---

## Together with dmxON FabKit

[**dmxON FabKit**](https://github.com/AlexSmith2025/dmxON-FabKit-Fusion-Electronics) turns the board into a complete JLCPCB order: Gerber zip, BOM and CPL with LCSC parts, a report, A4 assembly documentation and toner-transfer sheets.
Workflow: `dmxON_JLC_Setup` (rules, stack-up, DRC clean) → **save the board** (Ctrl+S) → `dmxON_FabKit` (order package; thickness and mask colour already filled in).

> **Save the board after the setup.** Fusion exports Gerber from the last *saved* version; without saving, the new rules (rings, vias, mask) do not reach the Gerber files.

---

## FAQ and troubleshooting

| Question | Answer |
|---|---|
| `dmxON_JLC_Setup` is not in the Run ULP list after installing | restart Fusion — it reads its folder list at start-up |
| Wrong layer count detected | the setup reads the board's stack-up and the copper on its layers; pick the right number in the list |
| «Layer N is outside the stack-up but holds: …» | the finding lists what is on that layer; move it off the layer or choose more layers |
| «Drill Size» errors | in Standard and Dense, holes under 0.3 mm are errors because JLCPCB charges for them; enlarge them or choose Extreme |
| «Drill Clearance» errors | holes closer than the profile's hole-to-hole distance (0.25 / 0.20 mm) |
| Many «copper to edge» errors | Standard keeps 0.3 mm (V-cut 0.4 mm); for a dense board use Dense (0.25) or Extreme (0.2) |
| Pad rings got larger | the rules set the JLCPCB minimum ring; a larger library pad is kept |
| Where are the files? | board rules and backups — `%LOCALAPPDATA%\dmxon_jlc`; the pack — `Documents\EAGLE\design rules` and `\cam` |

---

## How it works

Step 0 — `DRC SAVE` of the current rules (backup and the real stack-up) · step 1 — board scan, dialog, pre-flight check, rule file · step 2 — `DRC LOAD`, `CLASS`, `RATSNEST`, `DRC` · step 3 — DRC summary. Details: [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md) · changelog: [CHANGELOG.md](CHANGELOG.md).

```
dmxON-JLC-Rules/
├── dmxON_JLC_Setup.ulp     the board setup
├── INSTALL.ulp             adds the project to Fusion's ULP, rule and CAM folders
├── lib/                    jr_core (strings, files, language), jr_lang (es/de/pl texts), jr_rules (values, .dru, .cam), jr_stack (77 stack-ups)
├── lang/                   strings.tsv — all interface texts in five languages
├── rules/                  12 .dru + 4 .cam + README
└── docs/                   ARCHITECTURE.md, STACKUPS.md, assets/
```

Sources: [JLCPCB capabilities](https://jlcpcb.com/capabilities/pcb-capabilities) · [extra charges](https://jlcpcb.com/help/article/In-what-cases-will-there-be-charged-extra) · [impedance calculator / stack-ups](https://jlcpcb.com/impedance). Values checked on 2026-10-09; JLCPCB changes capabilities from time to time — check their page and the DFM report before ordering.

---

## Support the project

dmxON JLC Rules is **free**. It took many evenings of testing in Fusion, digging through JLCPCB capabilities and checking every stack-up to the micron. If it saved you a failed order, an evening of fiddling with DRC settings or simply some money — please support further development: new versions, rule updates when JLCPCB changes its capabilities, and fixes for new Fusion releases.

<p align="center">
  <a href="https://www.paypal.com/donate/?business=smith.show2025%40gmail.com&no_recurring=0&item_name=dmxON+JLC+Rules&currency_code=EUR"><img src="docs/assets/donate.svg" alt="Support dmxON JLC Rules with PayPal" width="760"></a>
</p>

<p align="center">
  <b>PayPal:</b> <a href="https://www.paypal.com/donate/?business=smith.show2025%40gmail.com&no_recurring=0&item_name=dmxON+JLC+Rules&currency_code=EUR">smith.show2025@gmail.com</a> — any amount helps. Thank you! ⭐ A star on GitHub also helps other people find the project.
</p>

---

## License

Free to use with attribution; copying the code, modification and commercial use are not permitted — see [LICENSE.md](LICENSE.md). JLCPCB is a trademark of its owner; this project is not affiliated with JLCPCB.

**dmxON by AlexSmith 2026** · [dmxon512.com](https://dmxon512.com) · companion project: [dmxON FabKit](https://github.com/AlexSmith2025/dmxON-FabKit-Fusion-Electronics)
