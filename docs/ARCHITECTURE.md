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

`jr_addin.ulp` — link to the dmxON add-in (heartbeat, request files). `INSTALL.ulp` (project root) copies the project to `Documents\dmxON\dmxON-JLC-Rules` and installs the dmxON add-in, which registers the project in Fusion's ULP list and `rules/` in the design-rule and CAM lists. It also undoes the `EAGLE:Directories.*` entries written by 1.1.0 — Fusion does not read them.

## Standard

`doc_std` (`dmxon.std`, shared with dmxON FabKit): 0 ISO — the preview names IPC-2221C, IPC-6012F Class 2 and IPC-A-600M; 1 GOST — the accuracy class of GOST R 53429-2009 for the smaller of track and space (classes 1–7: 0.75, 0.45, 0.25, 0.15, 0.10, 0.075, 0.05 mm).

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

## The dmxON add-in (`fusion-addin/dmxON`)

A Fusion add-in in Python does what a ULP cannot. It is shared by dmxON FabKit and dmxON JLC Rules (both repositories carry the same copy; `INSTALL.ulp` installs the newer one into `%APPDATA%\Autodesk\Autodesk Fusion 360\API\AddIns\dmxON`).

- **Folders.** Fusion reads its ULP, design-rule and CAM folders from its own preferences (`ElectronUlpDirectory`, `ElectronDesignRulesDirectory`, `ElectronCamDirectory` in `NGlobalOptions.xml`), not from `EAGLE:Directories.*`. The add-in sets them with the text commands `Options.Set` + `Options.Save` + `Options.Reload` (effective at once): the dmxON folders of the installed tools first, Fusion's built-in folders after them. Fusion's preferences — and the ULP settings of `cfgset` — are shared by every computer of the Autodesk account, so the lists hold variables, not paths of one computer: `$HOME\dmxON\dmxON-FabKit`, `$HOME\dmxON\dmxON-JLC-Rules` (`$HOME` = this user's Documents) and `$EAGLEDIR\…` for Fusion's built-in folders (LibEagle of the running build); both tools are always listed so that computers do not rewrite the shared value back and forth, and paths of other computers (`C:\Users\<name>\…`, `webdeploy\production\<build>`) are converted. The ULPs take the user folder only from paths that exist on this computer (`local_home()`, `home_here()` in `fk_addin.ulp` / `jr_addin.ulp`).
- **The dmxON tab** in the PCB and schematic editors: FabKit, JLC Rules, Backup, Updates, Settings, Help. Buttons only queue a custom event; the work runs after the command ends (`Electron.run RUN '…'` for the ULPs).
- **Requests from ULPs.** A ULP writes a JSON file into `Documents\dmxON\.inbox` (`addin_request()` in `fk_addin.ulp` / `jr_addin.ulp`); a background thread notices it and fires a custom event, handled when Fusion is idle. `Documents\dmxON\.dmxon-addin` is a heartbeat refreshed every 30 s — `addin_alive()` tells a ULP whether the add-in runs.
  - `register` — re-apply the folders (after `INSTALL.ulp`).
  - `fabkit_cam` — Gerber through `Electron.mfgexport <dir> <camjob>` with the dmxON JLCPCB CAM job (no «CAM Export File List» window), zipped into FabKit's `cam.zip`, then `RUN dmxON_FabKit.ulp -finish …`.
  - `backup` — back up the design folder (below) into the FabKit package (`05_BACKUP`, archive name `<board>_v<version>_cloud_<date>.zip` given by FabKit). FabKit itself writes the schematic and board (`<board>_v<version>_backup_<date>.zip`, the EAGLE 9 files Fusion hands to ULPs) before it asks. With `step` in the request the add-in first runs «3D PCB» (`Switch3dPcbDocCmd`): Fusion opens the design's linked 3D PCB or builds a new, unsaved one from the current board; the add-in waits until it is complete, exports `<board>_v<version>.step` (STEP AP214 with the component models) into `05_BACKUP`, closes the 3D PCB without saving when it was not open before and returns to the board.
  - `grid` — run a `GRID …` command in the schematic of the active board (dmxON JLC Rules sets the schematic grid), then return to the board.
- **Backup.** Every file of the active design's cloud folder (recursively): an Electronics design (`.fprj`) is opened and its schematic and board — found through `childReferences` — are written as EAGLE 9 files (`adsk.electron … exportManager.createEagleSchExportOptions / createEagleBrdExportOptions`); a schematic or board outside a design of the folder is opened through its parent design (opening it directly may ask which design to use); libraries → `.lbr`; 3D designs → Fusion archive `.f3d`; drawings → PDF; other files → `DataFile.download`. Documents opened on the way are closed again. Result: `Documents\dmxON\Backups\<project>\<folders>\<folder>_<date>.zip` (the Backup button); a backup requested by FabKit goes into the package instead — `<board>_v<version>_FabKit\05_BACKUP\<folder>_<date>.zip`, with `manifest.json` (cloud id and version of every file) and `RESTORE.txt`; the newest N backups per folder are kept.
- **Updates.** Once a day (and on the Updates button) `https://api.github.com/repos/<repo>/releases/latest` is compared with the `VERSION` file of each installed tool; the release asset zip is unpacked over `Documents\dmxON\<tool>`; a newer add-in inside it replaces this one after a Fusion restart.
- **Language** of the add-in: its own setting, else `dmxon.lang` of the ULPs (read from Fusion's `electronoptiongroup_eagle.rc`), else the language sent with the last ULP request.
