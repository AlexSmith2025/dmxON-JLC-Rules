# How it works

## Steps

| Step | Where | What happens |
|---|---|---|
| 0 | `dmxON_JLC_Setup.ulp` | `DRC SAVE` of the current rules to `%LOCALAPPDATA%\dmxon_jlc\rules_backup` — both the backup and the source of the stack-up (`layerSetup`); then `RUN … -stage2` with the same arguments |
| 1 | `-stage2` | board scan (`js_scan`), stack-up from the backup, dialog with preview, pre-flight check, board rule file, pack install, state for the summary |
| 2 | Fusion commands | `DRC LOAD`, `CLASS …`, `RATSNEST`, `DRC`, `RUN … -summary` |
| 3 | `-summary` | DRC errors by type (`UL_ERROR`: description, type, state), findings, profile notes |

Restoring is a separate run: step 0 → the dialog button → `DRC LOAD backup`, previous `CLASS`, `RATSNEST`, `DRC`.

`-export <folder>` — no board: writes 12 `.dru` and 4 `.cam` for 1.6 mm / 1 oz / 0.5 oz.

## Languages

- Every user-visible text is written in the code as a pair: `L("Russian", "English")`, or `Lf("…{0}…", "…{0}…", a, b, c)` for templates; `Lx(lg, …)` / `Lfx(lg, …)` produce a text in a given language (used for the five `description[…]` entries of a `.dru`).
- `ui_lang` selects the language: 0 English (default), 1 Russian, 2 Spanish, 3 German, 4 Polish. English and Russian come straight from the code; Spanish, German and Polish are looked up by the English text in `lib/jr_lang.ulp`. A missing translation falls back to English.
- `lib/jr_lang.ulp` is generated from `lang/strings.tsv` (columns `en ru es de pl`); edit the TSV, not the generated file.
- The choice is stored in the Fusion setting `dmxon.lang`, shared with dmxON FabKit; the dialog's language list re-opens the dialog in the new language.

## Modules (`lib/`)

| File | Purpose |
|---|---|
| `jr_core.ulp` | version, language selection, HTML entities, files, windowless commands (`wscript`), cross-step state |
| `jr_lang.ulp` | Spanish, German and Polish texts (generated) |
| `jr_rules.ulp` | inputs, profile values (`jr_calc`), stack-up choice, `.dru` text, CAM job, pack |
| `jr_stack.ulp` | the 77 JLCPCB stack-ups: layers, thickness, copper, dielectrics top to bottom (P/C, thickness, glass style, Er) |

`INSTALL.ulp` (project root) copies the project to `Documents\dmxON\dmxON-JLC-Rules` and adds it to `EAGLE:Directories.Ulp`, `.Dru` and `.Cam` through `cfgset`; Fusion applies directory changes after a restart. The original «use default directories» state is remembered once for both dmxON projects (`dmxon.install.usedefault`) and restored when the last of them is removed.

## Rules in `.dru`

- `layerSetup` — copper layers top to bottom; `+` (prepreg) or `*` (core) between them; the outer brackets mean through vias.
- `mtCopper` — copper thickness of layers 1…16; `mtIsolate[i]` — the dielectric under layer `i+1`.
- `mdWireWire`, `mdWirePad`, `mdWireVia`, `mdPadPad`, `mdPadVia`, `mdViaVia` — different-signal clearances; `mdSmdPad`, `mdSmdVia`, `mdSmdSmd` — **same-signal** clearances (not larger than the different-signal ones, or Fusion asks a question when loading).
- Ring: `rv…` is the share of the drill, `rlMin…`/`rlMax…` the limits; the inner ring is raised to keep 0.20 (via) and 0.30 mm (pin) from the hole to foreign copper.
- `mlViaStopLimit` — vias drilled up to this value are covered by mask.

## Fusion specifics

- In Fusion `UL_LAYER.used` means «the layer has objects», not «the layer is in the stack» — the stack comes from `DRC SAVE`.
- A `DRC LOAD` after `DRC` in the same command chain crashes Fusion: the error panel's queued update points at deleted errors. So rules change only at the start of a chain, and restoring is a separate run.
- After a rule change Fusion leaves polygons unpoured — `RATSNEST` before `DRC` is required, otherwise DRC sees hundreds of «unrouted» connections.
- `DRC` with new rules deletes approvals of messages that no longer match.
- In Fusion `path_dru[]` and `path_cam[]` point inside the program folder (`webdeploy`) — never written to.
- The `polygons()` loop is deprecated in Fusion and stops the ULP: signals use `polyPours()`, boards and footprints `polyShapes()`; footprints have no `smds()` — use `contacts()` and `C.smd`.
- A loop variable name (`B.signals(S)`) lives until the end of the block: every loop has its own name.
- `output()` writes in the Windows ANSI code page: non-ASCII text in `.dru` goes out as numeric HTML references, in `.cam` as `\uXXXX`.
- Helper commands (`mkdir`, `del`, `robocopy`) go through `dmxon_jlc_run.vbs` (`wscript`, windowless) — otherwise every call opens a Terminal window on Windows 11.
