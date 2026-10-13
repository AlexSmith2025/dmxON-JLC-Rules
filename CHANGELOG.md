# Changelog

The version is bumped on every change: `JR_VERSION` and `JR_DATE` in `lib/jr_core.ulp`, the `VERSION` file, the `rules/` pack (rebuild with `-export`) and an entry here.
Numbering: `MAJOR.MINOR.PATCH` — new feature → MINOR, fix → PATCH.

---

## 1.1.0 — 2026-10-13

**New**

- **Five languages, one at a time.** The dialog, the preview, the findings and the DRC summary come out in a single language — English (default), Russian, Spanish, German or Polish — instead of two languages side by side. The language is picked in the top-right corner of the dialog and switches it at once; dmxON FabKit uses the same setting.
- `-lang en|ru|es|de|pl` for batch mode.
- The rule files carry their description in all five languages (`description[en]`, `[ru]`, `[es]`, `[de]`, `[pl]`), so Fusion's DRC dialog can show it in Fusion's own interface language.
- **`INSTALL.ulp`** — copies the project to `Documents\dmxON\dmxON-JLC-Rules` and adds it to Fusion's ULP, design-rule and CAM directories through Fusion's own settings, so `dmxON_JLC_Setup` is in the Run ULP list and the rule pack in DRC → Load… after a restart. **Remove** restores the previous folders (shared with the dmxON FabKit installer).
- Translation table `lang/strings.tsv` → `lib/jr_lang.ulp` (Spanish, German, Polish), keyed by the English text.
- README in English, Russian, Spanish, German and Polish; a donation card for each language.

**Changed**

- Changelog, license, architecture notes and the rule pack README are in English only.

---

## 1.0.3 — 2026-10-13

**Changed**

- The repository is renamed to **dmxON-JLC-Rules-Fusion-Electronics** so it is easier to find when searching for «Fusion Electronics». Links in the program and docs are updated; GitHub redirects the old addresses.

---

## 1.0.2 — 2026-10-13

**Changed**

- The summary window shows a support line (PayPal) and a GitHub link; links open in the browser.
- README in English (main page) and Russian (`README.ru.md`): banner, version and download badges, a Download button, a compatibility table by program and version.
- README: save the board after the setup — Fusion exports Gerber from the last saved version.
- Releases carry a ready `dmxON-JLC-Rules.zip` (a permanent link to the latest version).

---

## 1.0.1 — 2026-10-13

**Fixed**

- DRC summary: «Drill Clearance» (hole spacing) is no longer reported as «drill below minimum», and the hint about paid holes under 0.3 mm shows only for real drill-size errors. The translation is checked against every Fusion and EAGLE error name, including the new ones («Maximum Drill Size», «Minimum PTH Drill Size», «Soldermask - Silkscreen Clearance»).
- The «copper outside the stack-up» finding now goes layer by layer and says what is there: tracks and pours of which nets, vias, lines, texts, pads and graphics of which parts. If Fusion marks a layer as used but nothing is found, it says so.

---

## 1.0.0 — 2026-10-09

First release of dmxON JLC Rules.

**New**

- DRC rule pack for 2, 4, 6 and 8 layers in three profiles: Standard (with margin, no extra cost), Dense (no-surcharge limit), Extreme (JLCPCB minimum).
- CAM jobs for 2, 4, 6 and 8 layers with JLCPCB file names (GTL, G1…, GBL, GTS, GBS, GTP, GBP, GTO, GBO, GKO, XLN).
- A table of 77 JLCPCB stack-ups (4, 6, 8 layers; 0.8–2.0 mm; 1–2 oz copper): Fusion builds the physical stack and board thickness from the rules.
- The `dmxON_JLC_Setup.ulp` setup: rule backup, layer detection from the stack and copper, rules for any thickness and copper, V-cut, tented or open vias, net classes, pack installation into user folders, pre-flight check, rule loading, polygon recalculation, DRC and a summary by error type; restore of the previous rules; batch mode and `-export`.
- Thickness and mask colour passed to dmxON FabKit.
- Everything in Russian and English.

**Verified in Fusion**

- The 4 and 8-layer stacks Fusion builds from the rules match the JLCPCB stack-ups to the micron; restoring yields a file identical to the backup.
