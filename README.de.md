<p align="center">
  <img src="docs/assets/banner.svg" alt="dmxON JLC Rules — JLCPCB-Designregeln für 2-, 4-, 6- und 8-lagige Platinen und Platinen-Setup für Autodesk Fusion Electronics" width="100%">
</p>

<p align="center">
  <a href="https://github.com/AlexSmith2025/dmxON-JLC-Rules-Fusion-Electronics/releases/latest"><img src="https://img.shields.io/github/v/release/AlexSmith2025/dmxON-JLC-Rules-Fusion-Electronics?style=for-the-badge&color=b4744a&label=release" alt="Neueste Version"></a>
  <a href="https://github.com/AlexSmith2025/dmxON-JLC-Rules-Fusion-Electronics/releases"><img src="https://img.shields.io/github/downloads/AlexSmith2025/dmxON-JLC-Rules-Fusion-Electronics/total?style=for-the-badge&color=24574a&label=downloads" alt="Downloads"></a>
  <img src="https://img.shields.io/badge/Autodesk%20Fusion-Electronics-e2ab7f?style=for-the-badge&logo=autodesk&logoColor=white" alt="Autodesk Fusion Electronics">
  <img src="https://img.shields.io/badge/Windows-10%20%7C%2011-3b4a5a?style=for-the-badge" alt="Windows 10 | 11">
  <a href="https://www.paypal.com/donate/?business=smith.show2025%40gmail.com&no_recurring=0&item_name=dmxON+JLC+Rules&currency_code=EUR"><img src="https://img.shields.io/badge/PayPal-Spenden-003087?style=for-the-badge&logo=paypal&logoColor=white" alt="Mit PayPal spenden"></a>
</p>

<p align="center">
  <a href="https://github.com/AlexSmith2025/dmxON-JLC-Rules-Fusion-Electronics/releases/latest/download/dmxON-JLC-Rules.zip"><img src="https://img.shields.io/badge/%E2%AC%87%20Download-dmxON--JLC--Rules.zip-b4744a?style=for-the-badge" alt="Neueste Version herunterladen"></a>
</p>

<p align="center">
  <a href="README.md">English</a> · <a href="README.ru.md">Русский</a> · <a href="README.es.md">Español</a> · <b>Deutsch</b> · <a href="README.pl.md">Polski</a>
</p>

<p align="center">
  <a href="#installation">Installation</a> ·
  <a href="#schnellstart">Schnellstart</a> ·
  <a href="#kompatibilität">Kompatibilität</a> ·
  <a href="#profile">Profile</a> ·
  <a href="#regeldateien-ohne-setup">Regeldateien</a> ·
  <a href="#projekt-unterstützen">Spenden</a>
</p>

**JLCPCB-Designregeln (DRC) für 2-, 4-, 6- und 8-lagige Platinen, CAM-Jobs mit den JLCPCB-Gerber-Namen und `dmxON_JLC_Setup.ulp` — das Platinen-Setup per Klick für Autodesk Fusion Electronics (Fusion 360 Electronics): wählt den passenden JLCPCB-Lagenaufbau, lädt die Regeln, prüft die Platine und startet den DRC.**

<p align="center">
  <a href="https://www.paypal.com/donate/?business=smith.show2025%40gmail.com&no_recurring=0&item_name=dmxON+JLC+Rules&currency_code=EUR"><img src="docs/assets/donate.de.svg" alt="dmxON JLC Rules mit PayPal unterstützen — smith.show2025@gmail.com" width="760"></a>
</p>

---

## Was enthalten ist

| | |
|---|---|
| 🧭 | **`dmxON_JLC_Setup.ulp`** — erkennt die Lagen der Platine, erzeugt JLCPCB-Regeln für Ihr Profil, Ihre Dicke und Kupferstärke, lädt sie, prüft die Platine und zeigt eine DRC-Zusammenfassung |
| 📏 | **12 DRC-Regeldateien** (`rules/*.dru`): 2, 4, 6, 8 Lagen × **Standard**, **Dicht**, **Extrem** |
| 🗂️ | **4 CAM-Jobs** (`rules/*.cam`): Gerber RS-274X + Excellon mit den JLCPCB-Dateinamen (GTL, G1…, GBL, GTS, GBS, GTP, GBP, GTO, GBO, GKO, XLN) |
| 🧱 | **77 JLCPCB-Lagenaufbauten** (4, 6, 8 Lagen · 0.8–2.0 mm · 1–2 oz Kupfer) — Prepreg- und Kerndicken genau wie bestellt |
| 🛟 | **Sicherung** der bisherigen Regeln vor jedem Lauf und Wiederherstellung per Knopfdruck |
| 🔎 | **Vorabprüfung** dessen, was der DRC nicht sieht: Bestückungsdruckgröße, nicht durchkontaktierte Bohrungen, Platinengröße, Kupfer außerhalb des Aufbaus — mit einer Liste, was auf der falschen Lage liegt |
| 🌐 | **5 Sprachen**: Englisch, Russisch, Spanisch, Deutsch, Polnisch — Auswahl im Dialog; die Regeldateien tragen ihre Beschreibung in allen fünf |

---

## Kompatibilität

| | Setup `dmxON_JLC_Setup.ulp` | Regeldateien `.dru` | CAM-Jobs `.cam` |
|---|---|---|---|
| **Autodesk Fusion (Electronics), Windows 10/11** | ✅ getestet mit Fusion **2705.1.11** und **2705.1.30** (Oktober 2026) | ✅ getestet | ✅ CAM Processor |
| Autodesk Fusion unter macOS | ❌ nutzt Windows-Hilfsbefehle | ✅ gleiches Format | ✅ gleiches Format |
| EAGLE 9.x | ❌ braucht die Fusion-ULP-Schleifen `polyPours`/`polyShapes` | ✅ EAGLE-9-Format | ✅ Jobformat EAGLE 8.6–9.6 |
| KiCad, Altium, EasyEDA | ❌ | ❌ anderes Regelformat | ❌ |

Ältere oder neuere Fusion-Builds funktionieren meist ebenfalls; wenn nach einem Fusion-Update etwas nicht geht, bitte [ein Issue öffnen](https://github.com/AlexSmith2025/dmxON-JLC-Rules-Fusion-Electronics/issues). Weder Internet noch zusätzliche Software sind nötig.

---

## Installation

1. [**`dmxON-JLC-Rules.zip` herunterladen**](https://github.com/AlexSmith2025/dmxON-JLC-Rules-Fusion-Electronics/releases/latest/download/dmxON-JLC-Rules.zip) und an beliebiger Stelle entpacken.
2. In Fusion Electronics: **Automation → Run ULP → `INSTALL.ulp`** aus dem entpackten Ordner, Sprache wählen und **Installieren** drücken.
3. **Fusion neu starten.** `dmxON_JLC_Setup` steht nun in der Liste **Run ULP** neben den integrierten ULPs, das Regelpaket unter **DRC → Load…** und im CAM Processor; die integrierten Dateien von Fusion bleiben erhalten.

Der Installer kopiert das Projekt nach `Dokumente\dmxON\dmxON-JLC-Rules` und trägt es über die eigenen Einstellungen von Fusion in die Ordner für ULPs, Designregeln und CAM ein. Ein erneuter Aufruf von `INSTALL.ulp` aktualisiert die Dateien; **Entfernen** stellt die vorherigen Ordner von Fusion wieder her. Manuell: den entpackten Ordner vollständig lassen (`dmxON_JLC_Setup.ulp` lädt seine Module aus `lib\` daneben) und mit `RUN 'C:/Pfad/dmxON_JLC_Setup.ulp'` starten.

---

## Schnellstart

1. Die **Platine** in Fusion Electronics öffnen.
2. **Automation → Run ULP → `dmxON_JLC_Setup`** starten.
3. Oben rechts die **Sprache** wählen (Standard: Englisch), Lagenzahl, Profil und Dicke prüfen — die Vorschau zeigt jeden Wert, den Lagenaufbau und die Befunde der Platine.
4. **Anwenden** drücken. Wenige Sekunden später erscheint die Zusammenfassung mit dem DRC-Ergebnis.
5. **Platine speichern** (Strg+S) — die Regeln werden in ihr gespeichert, und Fusion exportiert Gerber aus der gespeicherten Version.

Am besten **vor dem Routen** ausführen (dann folgt das Routing von Anfang an den JLCPCB-Regeln) und **noch einmal vor dem Export**.

---

## Der Dialog

| Feld | Was es einstellt |
|---|---|
| **Sprache** (oben rechts) | English, Русский, Español, Deutsch, Polski — der Dialog wechselt sofort; gemeinsam mit dmxON FabKit |
| **Kupferlagen** | 2, 4, 6 oder 8. Standard: was der Lagenaufbau der Platine und das Kupfer auf ihren Lagen ergeben |
| **Profil** | Standard, Dicht, Extrem — siehe [Profile](#profile) |
| **Dicke, mm** | 0.4–2.0. JLCPCB fertigt 4–8 Lagen in 0.8–2.0 mm; eine nicht verfügbare Wahl fällt mit Hinweis auf den nächsten Wert zurück |
| **Kupfer außen** | 1 oz (35 µm) oder 2 oz (70 µm); 2 oz braucht breitere Leiterbahnen und Abstände |
| **Kupfer innen** | 0.5, 1 oder 2 oz — für 4–8 Lagen |
| **Lötstoppfarbe** | für den Hinweis zum Maskensteg (0.10 mm; Weiß und Schwarz 0.13 mm) und für dmxON FabKit |
| **Abgedeckte Vias** | Vias bis 0.5 mm Bohrung werden vom Lötstopp abgedeckt (wie «Tented» auf der Bestellseite) |
| **V-Cut-Nutzen** | Kupfer mindestens 0.4 mm vom Platinenrand |
| **Netzklassen nicht unter dem Minimum** | hebt Klassen an, deren Breite, Abstand oder Bohrung unter dem Profil liegt; Klasse 0 erhält das Minimum als Routing-Standard |
| **Regelpaket und CAM nach Dokumente/EAGLE** | alle 12 Regeldateien, die Datei für Ihre Platine und der CAM-Job landen in `Dokumente\EAGLE\design rules` und `\cam`; in den Fusion-Programmordner wird nichts geschrieben |
| **Dicke und Lötstopp an dmxON FabKit** | [dmxON FabKit](https://github.com/AlexSmith2025/dmxON-FabKit-Fusion-Electronics) übernimmt diese Werte für die Bestellung |

Schaltflächen: **Anwenden** · **Nur Dateien…** (schreibt `.dru` und `.cam` für die gewählten Einstellungen in einen beliebigen Ordner, die Platine bleibt unberührt) · **Bisherige Regeln wiederherstellen** (nach einem früheren Setup) · **Abbrechen**.

---

## Profile

Alle Maße in Millimetern, 1 oz Kupfer.

| mm | 2 Lagen Standard | 4–8 Lagen Standard | 2 Lagen Dicht | 4–8 Lagen Dicht | 2 Lagen Extrem | 4–8 Lagen Extrem |
|---|---|---|---|---|---|---|
| Leiterbahn und Abstand | 0.127 | 0.127 | 0.10 | 0.10 | 0.10 | 0.09 ¹ |
| Pad zu Pad, verschiedene Netze | 0.15 | 0.15 | 0.15 | 0.15 | 0.10 | 0.09 |
| Via-Bohrung / Durchmesser | 0.3 / 0.45 | 0.3 / 0.45 | 0.3 / 0.40 | 0.3 / 0.40 | 0.15 / 0.25 ² | 0.15 / 0.25 ² |
| Via-Restring, Innenlagen | — | 0.08 | — | 0.10 | — | 0.11 |
| PTH-Restring | 0.25 | 0.20 | 0.18 | 0.15 | 0.18 | 0.15 |
| PTH-Restring, Innenlagen | — | 0.20 | — | 0.20 | — | 0.21 |
| Minimale Bohrung | 0.3 | 0.3 | 0.3 | 0.3 | 0.15 ² | 0.15 ² |
| Kupfer zum Rand | 0.30 | 0.30 | 0.25 | 0.25 | 0.20 | 0.20 |
| Bohrung zu Bohrung | 0.25 | 0.25 | 0.20 | 0.20 | 0.20 | 0.20 |
| Lötstopp-Erweiterung | 0.05 | 0.05 | 0.05 | 0.05 | 0.05 | 0.05 |

¹ 3–3.5-mil-Leiterbahnen auf Mehrlagenplatinen kosten **+20 %**. ² Bohrungen unter 0.3 mm kosten extra — auf der Bestellseite **Min via hole size** wählen.

- **Standard** — die meisten Platinen: technologische Reserve, keine Aufpreise.
- **Dicht** — dichte Layouts an der Grenze dessen, was JLCPCB ohne Aufpreis fertigt.
- **Extrem** — BGA und feines Raster; das absolute JLCPCB-Minimum, manche Werte kosten extra.

**Warum der Innenring größer ist:** auf Innenlagen verlangt JLCPCB 0.20 mm von einer Via-Bohrung und 0.30 mm von einer Pin-Bohrung bis zu fremdem Kupfer; die Regeln erreichen das über den Restring, damit der normale Abstand gleich bleibt.
**2 oz Kupfer:** Leiterbahn und Abstand 0.20 (Standard), 0.16 bei 2 Lagen / 0.15 bei Mehrlagen (Dicht, Extrem); PTH-Restring 0.26; Maskensteg ab 0.20.
**Abstände desselben Signals** (`mdSmdPad`, `mdSmdVia`, `mdSmdSmd`) entsprechen dem Abstand verschiedener Signale, damit Fusion beim Laden keine Fragen stellt.

Werte pro Datei: [rules/README.md](rules/README.md).

---

## Lagenaufbau und Dicke

Die Regeln enthalten den **JLCPCB-Lagenaufbau** — Kupferlagen, Prepreg (`+`) und Kern (`*`), Kupfer- und Dielektrikumsdicken. Fusion baut daraus den physischen Aufbau (Layer Stack Manager), sodass die Dicke in 3D und im Gerber-Job zu Ihrer Bestellung passt.

| Lagen | 1.6 mm, 1 oz / 0.5 oz | Dielektrika von oben nach unten, mm |
|---|---|---|
| 2 | `(1*16)` | Kern 1.53 |
| 4 | `(1+2*15+16)` | Prepreg 7628 0.2104 · Kern 1.065 · Prepreg 7628 0.2104 |
| 6 | `(1+2*3+14*15+16)` | 3313 0.0994 · Kern 0.55 · 2116 0.1164 · Kern 0.55 · 3313 0.0994 |
| 8 | `(1+2*3+4*13+14*15+16)` | 2116 0.1164 · Kern 0.30 · 1080×2 0.1528 · Kern 0.30 · 1080×2 0.1528 · Kern 0.30 · 2116 0.1164 |

Alle 77 Aufbauten: [docs/STACKUPS.md](docs/STACKUPS.md). Innenlagen, die bereits Kupfer tragen, behalten ihre Nummern; sonst werden die üblichen Nummern verwendet (4 Lagen: 2, 15 · 6 Lagen: 2, 3, 14, 15 · 8 Lagen: 2, 3, 4, 13, 14, 15).

---

## Vorabprüfung

| Prüfung | Warum |
|---|---|
| Kupfer auf Lagen außerhalb des gewählten Aufbaus — mit einer Liste der dort gefundenen Leiterbahnen, Flächen, Vias, Pads und Bauteile | es würde im Gerber fehlen |
| Keine Platinenkontur (Lage 20) | ohne Kontur keine Platine |
| Platinengröße: 3 × 3 mm bis 670 × 600 (2 Lagen), 663 × 593 (4 Lagen), 656 × 586 mm (6–8 Lagen) | JLCPCB-Grenzen |
| Leiterbahnen dünner und Vias kleiner als das Profilminimum; Vias unter 0.3 mm | DRC-Prognose und Aufpreis für kleine Bohrungen |
| Nicht durchkontaktierte Bohrungen unter 0.5 mm | JLCPCB-Minimum |
| Bestückungsdrucktexte unter 1.0 mm oder mit Strichen unter 0.15 mm; Linien unter 0.15 mm | evtl. unlesbar oder unterbrochen |
| Netzklassen unter dem Minimum | DRC und Routing folgen ihnen |
| Genehmigte DRC-Meldungen auf der Platine | siehe Hinweis unten |

---

## Die Zusammenfassung

Nach dem Laden der Regeln berechnet das Setup die Polygone neu (`RATSNEST`), startet den DRC und zeigt, welche Regeln geladen und wo die alten gespeichert wurden, welche Netzklassen angehoben wurden, wohin das Paket installiert wurde, **DRC-Fehler nach Art** (Abstand, Kupfer zum Rand, Bohrabstand, Bohrgröße, nicht geroutet…) mit getrennt gezählten Warnungen und Genehmigungen sowie Hinweise wie «Bohrungen unter 0.3 mm kosten bei JLCPCB extra». Die Fehlerliste selbst steht im Fusion-Bereich **ERRORS**.

---

## Bisherige Regeln wiederherstellen

Vor jedem Lauf werden die aktuellen Regeln der Platine in `%LOCALAPPDATA%\dmxon_jlc\rules_backup` gesichert. Um sie zurückzuholen, **das Setup erneut starten** und **Bisherige Regeln wiederherstellen** drücken — Regeln, Lagenaufbau und Netzklassen kehren zurück, danach werden die Polygone neu berechnet und der DRC läuft.

> **Genehmigte DRC-Meldungen.** Eine Prüfung mit neuen Regeln verwirft Genehmigungen, die nicht mehr passen, und das Wiederherstellen der Regeln bringt sie nicht zurück. Das Setup warnt, wenn die Platine Genehmigungen hat — vorher eine Version der Platine speichern (File → Save / Create Version).

---

## Stapelbetrieb

```
RUN dmxON_JLC_Setup.ulp -batch [-layers 2|4|6|8] [-profile Standard|Dense|Extreme] [-thick 1.6] [-outer 1|2] [-inner 0.5|1|2] [-mask Green] [-vcut] [-open] [-noclass] [-noinstall] [-nofabkit] [-lang en|ru|es|de|pl]
RUN dmxON_JLC_Setup.ulp -export <Ordner>
```

`-vcut` Kupfer 0.4 mm vom Rand · `-open` nicht abgedeckte Vias · `-noclass` / `-noinstall` / `-nofabkit` Klassen / Paket / FabKit auslassen · `-lang` Sprache der Zusammenfassung · `-export` schreibt nur das Paket (12 `.dru` + 4 `.cam`), keine Platine nötig. Einstellungen des Stapelbetriebs werden nicht gespeichert.

---

## Regeldateien ohne Setup

**Regeln:** Fusion — **DRC → Load…** (oder `DRC LOAD 'Pfad/Datei.dru'`), dann **DRC**. EAGLE 9 — **Tools → DRC → File → Load…**.
**CAM-Job:** **Manufacturing → CAM Processor → Load job file** → `rules/dmxON_JLCPCB_<N>L.cam` → **Process Job**, das Ergebnis zippen und auf jlcpcb.com hochladen.
Die Regeldateien gehen von 1.6 mm, 1 oz / 0.5 oz, abgedeckten Vias und normalem Routing aus; für alles andere im Setup **Nur Dateien…** verwenden.

---

## Zusammen mit dmxON FabKit

[**dmxON FabKit**](https://github.com/AlexSmith2025/dmxON-FabKit-Fusion-Electronics) macht aus der Platine eine komplette JLCPCB-Bestellung: Gerber-Zip, BOM und CPL mit LCSC-Teilen, einen Bericht, A4-Bestückungsdokumentation und Blätter für den Tonertransfer.
Ablauf: `dmxON_JLC_Setup` (Regeln, Lagenaufbau, DRC sauber) → **Platine speichern** (Strg+S) → `dmxON_FabKit` (Bestellpaket; Dicke und Lötstoppfarbe bereits eingetragen).

> **Platine nach dem Setup speichern.** Fusion exportiert Gerber aus der zuletzt *gespeicherten* Version; ohne Speichern erreichen die neuen Regeln (Restringe, Vias, Maske) die Gerber-Dateien nicht.

---

## FAQ und Fehlerbehebung

| Frage | Antwort |
|---|---|
| `dmxON_JLC_Setup` fehlt nach der Installation in der Liste Run ULP | Fusion neu starten — die Ordnerliste wird beim Start gelesen |
| Falsche Lagenzahl erkannt | das Setup liest den Lagenaufbau der Platine und das Kupfer auf ihren Lagen; die richtige Zahl in der Liste wählen |
| «Lage N liegt außerhalb des Aufbaus, enthält aber: …» | der Befund listet, was auf dieser Lage liegt; es von der Lage entfernen oder mehr Lagen wählen |
| Fehler «Drill Size» | in Standard und Dicht sind Bohrungen unter 0.3 mm Fehler, weil JLCPCB sie extra berechnet; vergrößern oder Extrem wählen |
| Fehler «Drill Clearance» | Bohrungen näher als der Bohrabstand des Profils (0.25 / 0.20 mm) |
| Viele Fehler «Kupfer zum Rand» | Standard hält 0.3 mm (V-Cut 0.4 mm); für eine dichte Platine Dicht (0.25) oder Extrem (0.2) verwenden |
| Pad-Restringe wurden größer | die Regeln setzen den JLCPCB-Mindestrestring; ein größeres Bibliotheks-Pad bleibt erhalten |
| Wo liegen die Dateien? | Platinenregeln und Sicherungen — `%LOCALAPPDATA%\dmxon_jlc`; das Paket — `Dokumente\EAGLE\design rules` und `\cam` |

---

## Wie es funktioniert

Schritt 0 — `DRC SAVE` der aktuellen Regeln (Sicherung und tatsächlicher Lagenaufbau) · Schritt 1 — Platinenanalyse, Dialog, Vorabprüfung, Regeldatei · Schritt 2 — `DRC LOAD`, `CLASS`, `RATSNEST`, `DRC` · Schritt 3 — DRC-Zusammenfassung. Details: [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md) · Änderungen: [CHANGELOG.md](CHANGELOG.md).

```
dmxON-JLC-Rules/
├── dmxON_JLC_Setup.ulp     das Platinen-Setup
├── INSTALL.ulp             trägt das Projekt in die ULP-, Regel- und CAM-Ordner von Fusion ein
├── lib/                    jr_core (Strings, Dateien, Sprache), jr_lang (Texte es/de/pl), jr_rules (Werte, .dru, .cam), jr_stack (77 Aufbauten)
├── lang/                   strings.tsv — alle Oberflächentexte in fünf Sprachen
├── rules/                  12 .dru + 4 .cam + README
└── docs/                   ARCHITECTURE.md, STACKUPS.md, assets/
```

Quellen: [JLCPCB-Fertigungsmöglichkeiten](https://jlcpcb.com/capabilities/pcb-capabilities) · [Aufpreise](https://jlcpcb.com/help/article/In-what-cases-will-there-be-charged-extra) · [Impedanzrechner / Lagenaufbauten](https://jlcpcb.com/impedance). Werte geprüft am 2026-10-09; JLCPCB ändert seine Möglichkeiten von Zeit zu Zeit — vor der Bestellung deren Seite und den DFM-Bericht prüfen.

---

## Projekt unterstützen

dmxON JLC Rules ist **kostenlos**. Dahinter stecken viele Abende mit Tests in Fusion, der Auswertung der JLCPCB-Möglichkeiten und der Prüfung jedes Lagenaufbaus auf den Mikrometer. Wenn es Ihnen eine misslungene Bestellung, einen Abend mit DRC-Einstellungen oder einfach Geld erspart hat — bitte unterstützen Sie die Weiterentwicklung: neue Versionen, Regelupdates bei Änderungen von JLCPCB und Anpassungen an neue Fusion-Versionen.

<p align="center">
  <a href="https://www.paypal.com/donate/?business=smith.show2025%40gmail.com&no_recurring=0&item_name=dmxON+JLC+Rules&currency_code=EUR"><img src="docs/assets/donate.de.svg" alt="dmxON JLC Rules mit PayPal unterstützen" width="760"></a>
</p>

<p align="center">
  <b>PayPal:</b> <a href="https://www.paypal.com/donate/?business=smith.show2025%40gmail.com&no_recurring=0&item_name=dmxON+JLC+Rules&currency_code=EUR">smith.show2025@gmail.com</a> — jeder Betrag hilft. Danke! ⭐ Ein Stern auf GitHub hilft anderen, das Projekt zu finden.
</p>

---

## Lizenz

Kostenlose Nutzung mit Namensnennung; Kopieren des Codes, Änderung und kommerzielle Nutzung sind nicht gestattet — siehe [LICENSE.md](LICENSE.md). JLCPCB ist eine Marke ihres Inhabers; dieses Projekt steht in keiner Verbindung zu JLCPCB.

**dmxON by AlexSmith 2026** · [dmxon512.com](https://dmxon512.com) · Schwesterprojekt: [dmxON FabKit](https://github.com/AlexSmith2025/dmxON-FabKit-Fusion-Electronics)
