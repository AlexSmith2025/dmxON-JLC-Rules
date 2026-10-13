<p align="center">
  <img src="docs/assets/banner.svg" alt="dmxON JLC Rules — reguły projektowe JLCPCB dla płytek 2-, 4-, 6- i 8-warstwowych oraz konfiguracja płytki dla Autodesk Fusion Electronics" width="100%">
</p>

<p align="center">
  <a href="https://github.com/AlexSmith2025/dmxON-JLC-Rules-Fusion-Electronics/releases/latest"><img src="https://img.shields.io/github/v/release/AlexSmith2025/dmxON-JLC-Rules-Fusion-Electronics?style=for-the-badge&color=b4744a&label=release" alt="Najnowsza wersja"></a>
  <a href="https://github.com/AlexSmith2025/dmxON-JLC-Rules-Fusion-Electronics/releases"><img src="https://img.shields.io/github/downloads/AlexSmith2025/dmxON-JLC-Rules-Fusion-Electronics/total?style=for-the-badge&color=24574a&label=downloads" alt="Pobrania"></a>
  <img src="https://img.shields.io/badge/Autodesk%20Fusion-Electronics-e2ab7f?style=for-the-badge&logo=autodesk&logoColor=white" alt="Autodesk Fusion Electronics">
  <img src="https://img.shields.io/badge/Windows-10%20%7C%2011-3b4a5a?style=for-the-badge" alt="Windows 10 | 11">
  <a href="https://www.paypal.com/donate/?business=smith.show2025%40gmail.com&no_recurring=0&item_name=dmxON+JLC+Rules&currency_code=EUR"><img src="https://img.shields.io/badge/PayPal-Wesprzyj-003087?style=for-the-badge&logo=paypal&logoColor=white" alt="Wesprzyj przez PayPal"></a>
</p>

<p align="center">
  <a href="https://github.com/AlexSmith2025/dmxON-JLC-Rules-Fusion-Electronics/releases/latest/download/dmxON-JLC-Rules.zip"><img src="https://img.shields.io/badge/%E2%AC%87%20Pobierz-dmxON--JLC--Rules.zip-b4744a?style=for-the-badge" alt="Pobierz najnowszą wersję"></a>
</p>

<p align="center">
  <a href="README.md">English</a> · <a href="README.ru.md">Русский</a> · <a href="README.es.md">Español</a> · <a href="README.de.md">Deutsch</a> · <b>Polski</b>
</p>

<p align="center">
  <a href="#instalacja">Instalacja</a> ·
  <a href="#szybki-start">Szybki start</a> ·
  <a href="#zgodność">Zgodność</a> ·
  <a href="#profile">Profile</a> ·
  <a href="#pliki-reguł-bez-konfiguratora">Pliki reguł</a> ·
  <a href="#wesprzyj-projekt">Wesprzyj</a>
</p>

**Reguły projektowe (DRC) JLCPCB dla płytek 2-, 4-, 6- i 8-warstwowych, zadania CAM z nazwami plików Gerber JLCPCB oraz `dmxON_JLC_Setup.ulp` — konfiguracja płytki jednym kliknięciem dla Autodesk Fusion Electronics (Fusion 360 Electronics): dobiera właściwy stos warstw JLCPCB, wczytuje reguły, sprawdza płytkę i uruchamia DRC.**

<p align="center">
  <a href="https://www.paypal.com/donate/?business=smith.show2025%40gmail.com&no_recurring=0&item_name=dmxON+JLC+Rules&currency_code=EUR"><img src="docs/assets/donate.pl.svg" alt="Wesprzyj dmxON JLC Rules przez PayPal — smith.show2025@gmail.com" width="760"></a>
</p>

---

## Co zawiera

| | |
|---|---|
| 🧭 | **`dmxON_JLC_Setup.ulp`** — rozpoznaje warstwy płytki, tworzy reguły JLCPCB dla Twojego profilu, grubości i miedzi, wczytuje je, sprawdza płytkę i pokazuje podsumowanie DRC |
| 📏 | **12 plików reguł DRC** (`rules/*.dru`): 2, 4, 6, 8 warstw × **Standard**, **Gęsty**, **Ekstremalny** |
| 🗂️ | **4 zadania CAM** (`rules/*.cam`): Gerber RS-274X + Excellon z nazwami plików JLCPCB (GTL, G1…, GBL, GTS, GBS, GTP, GBP, GTO, GBO, GKO, XLN) |
| 🧱 | **77 stosów warstw JLCPCB** (4, 6, 8 warstw · 0.8–2.0 mm · miedź 1–2 oz) — grubości prepregu i rdzenia dokładnie jak w zamówieniu |
| 🛟 | **Kopia zapasowa** poprzednich reguł przed każdym uruchomieniem i przywracanie jednym przyciskiem |
| 🔎 | **Kontrola wstępna** tego, czego DRC nie widzi: rozmiar opisów, otwory niemetalizowane, rozmiar płytki, miedź poza stosem — z listą tego, co leży na złej warstwie |
| 🌐 | **5 języków**: angielski, rosyjski, hiszpański, niemiecki, polski — wybór w oknie; pliki reguł mają opis we wszystkich pięciu |
| 📐 | **ISO lub GOST**: wybór normy obok języka, wspólny z dmxON FabKit; podgląd i podsumowanie podają IPC-2221C / IPC-6012F klasa 2 / IPC-A-600M albo **klasę dokładności wg GOST R 53429-2009** dla Twojej ścieżki i odstępu |
| 🧩 | **Karta dmxON w Fusion** (dodatek): JLC Rules, FabKit, kopia całego folderu projektu i aktualizacje z GitHuba jednym kliknięciem; pakiet reguł i zadania CAM są na listach Fusion |

---

## Zgodność

| | Konfigurator `dmxON_JLC_Setup.ulp` | Pliki reguł `.dru` | Zadania CAM `.cam` |
|---|---|---|---|
| **Autodesk Fusion (Electronics), Windows 10/11** | ✅ sprawdzone na Fusion **2705.1.30** (październik 2026) | ✅ sprawdzone | ✅ CAM Processor |
| Autodesk Fusion na macOS | ❌ korzysta z poleceń pomocniczych Windows | ✅ ten sam format | ✅ ten sam format |
| EAGLE 9.x | ❌ wymaga pętli ULP Fusion `polyPours`/`polyShapes` | ✅ format EAGLE 9 | ✅ format zadań EAGLE 8.6–9.6 |
| KiCad, Altium, EasyEDA | ❌ | ❌ inny format reguł | ❌ |

Starsze i nowsze wersje Fusion zwykle też działają; jeśli coś przestanie działać po aktualizacji Fusion, [zgłoś issue](https://github.com/AlexSmith2025/dmxON-JLC-Rules-Fusion-Electronics/issues). Nie potrzeba internetu ani dodatkowego oprogramowania.

---

## Instalacja

1. [**Pobierz `dmxON-JLC-Rules.zip`**](https://github.com/AlexSmith2025/dmxON-JLC-Rules-Fusion-Electronics/releases/latest/download/dmxON-JLC-Rules.zip) i rozpakuj w dowolnym miejscu.
2. W Fusion Electronics: **Automation → Run ULP → `INSTALL.ulp`** z rozpakowanego folderu, wybierz język i naciśnij **Zainstaluj**.
3. **Uruchom ponownie Fusion jeden raz.** Edytory płytki i schematu dostaną kartę **dmxON**, `dmxON_JLC_Setup` będzie w **Run ULP**, pakiet reguł w **DRC → Load…**, a zadania CAM na liście CAM.

Instalator kopiuje projekt do `Dokumenty\dmxON\dmxON-JLC-Rules` i instaluje **dodatek dmxON** (`%APPDATA%\Autodesk\Autodesk Fusion 360\API\AddIns\dmxON`), który stawia foldery dmxON na początku list ULP, reguł i CAM w Fusion (Preferences → General → Electronics → Directory) i naprawia je po aktualizacjach; wbudowane foldery pozostają. Ponowne uruchomienie `INSTALL.ulp` aktualizuje pliki; **Usuń** kasuje skopiowany projekt, a z ostatnim narzędziem dmxON także dodatek. Bez ponownego uruchomienia: **Utilities → Add-Ins → Scripts and Add-Ins → dmxON → Run**.

---

## Szybki start

1. Otwórz **płytkę** w Fusion Electronics.
2. Naciśnij **dmxON → JLC Rules** (albo **Automation → Run ULP → `dmxON_JLC_Setup`**).
3. W prawym górnym rogu wybierz **normę** (ISO lub GOST) i **język**, sprawdź liczbę warstw, profil i grubość — podgląd pokazuje każdą wartość, stos warstw i uwagi do płytki.
4. Naciśnij **Zastosuj**. Po kilku sekundach pojawi się podsumowanie z wynikiem DRC.
5. **Zapisz płytkę** (Ctrl+S) — reguły są w niej zapisywane, a Fusion eksportuje Gerber z zapisanej wersji.

Najlepiej uruchomić **przed trasowaniem** (wtedy ścieżki od początku idą wg reguł JLCPCB) i **jeszcze raz przed eksportem**.

---

## Okno

| Pole | Co ustawia |
|---|---|
| **Język** (prawy górny róg) | English, Русский, Español, Deutsch, Polski — okno przełącza się od razu; wspólne z dmxON FabKit |
| **Norma** (prawy górny róg) | ISO lub GOST — jakie normy podają podgląd i podsumowanie oraz jaką dokumentację tworzy dmxON FabKit; wspólna z FabKit |
| **Warstwy miedzi** | 2, 4, 6 lub 8. Domyślnie: to, co wynika ze stosu płytki i miedzi na jej warstwach |
| **Profil** | Standard, Gęsty, Ekstremalny — zob. [Profile](#profile) |
| **Grubość, mm** | 0.4–2.0. JLCPCB robi 4–8 warstw w grubości 0.8–2.0 mm; niedostępny wybór zastępowany jest najbliższym z uwagą |
| **Miedź zewnętrzna** | 1 oz (35 µm) lub 2 oz (70 µm); 2 oz wymaga szerszych ścieżek i odstępów |
| **Miedź wewnętrzna** | 0.5, 1 lub 2 oz — dla 4–8 warstw |
| **Kolor maski** | do wskazówki o mostku maski (0.10 mm; biała i czarna 0.13 mm) i dla dmxON FabKit |
| **Przelotki pod maską** | przelotki o otworze do 0.5 mm są przykryte maską (jak «Tented» na stronie zamówienia) |
| **Panel V-cut** | miedź co najmniej 0.4 mm od krawędzi płytki |
| **Klasy sieci nie poniżej minimum** | podnosi klasy, których szerokość, odstęp lub wiercenie są poniżej profilu; klasa 0 dostaje minimum jako domyślną wartość trasowania |
| **Pakiet reguł i CAM do Dokumenty/EAGLE** | wszystkie 12 plików reguł, plik dla Twojej płytki i zadanie CAM trafiają do `Dokumenty\EAGLE\design rules` i `\cam`; nic nie jest zapisywane w folderze programu Fusion |
| **Grubość i maska do dmxON FabKit** | [dmxON FabKit](https://github.com/AlexSmith2025/dmxON-FabKit-Fusion-Electronics) bierze te wartości do zamówienia |

Przyciski: **Zastosuj** · **Tylko pliki…** (zapisuje `.dru` i `.cam` dla wybranych ustawień w dowolnym folderze, płytka pozostaje nietknięta) · **Przywróć poprzednie reguły** (po wcześniejszej konfiguracji) · **Anuluj**.

---

## Profile

Wszystkie wymiary w milimetrach, miedź 1 oz.

| mm | 2 warstwy Standard | 4–8 warstw Standard | 2 warstwy Gęsty | 4–8 warstw Gęsty | 2 warstwy Ekstremalny | 4–8 warstw Ekstremalny |
|---|---|---|---|---|---|---|
| Ścieżka i odstęp | 0.127 | 0.127 | 0.10 | 0.10 | 0.10 | 0.09 ¹ |
| Pad–pad, różne sieci | 0.15 | 0.15 | 0.15 | 0.15 | 0.10 | 0.09 |
| Przelotka: otwór / średnica | 0.3 / 0.45 | 0.3 / 0.45 | 0.3 / 0.40 | 0.3 / 0.40 | 0.15 / 0.25 ² | 0.15 / 0.25 ² |
| Pierścień przelotki, warstwy wewnętrzne | — | 0.08 | — | 0.10 | — | 0.11 |
| Pierścień PTH | 0.25 | 0.20 | 0.18 | 0.15 | 0.18 | 0.15 |
| Pierścień PTH, warstwy wewnętrzne | — | 0.20 | — | 0.20 | — | 0.21 |
| Minimalne wiercenie | 0.3 | 0.3 | 0.3 | 0.3 | 0.15 ² | 0.15 ² |
| Miedź do krawędzi | 0.30 | 0.30 | 0.25 | 0.25 | 0.20 | 0.20 |
| Otwór–otwór | 0.25 | 0.25 | 0.20 | 0.20 | 0.20 | 0.20 |
| Poszerzenie maski | 0.05 | 0.05 | 0.05 | 0.05 | 0.05 | 0.05 |

¹ Ścieżki 3–3.5 mil na płytkach wielowarstwowych podnoszą cenę o **+20 %**. ² Otwory poniżej 0.3 mm są dodatkowo płatne — wybierz **Min via hole size** na stronie zamówienia.

- **Standard** — większość płytek: zapas technologiczny, bez dopłat.
- **Gęsty** — gęste projekty na granicy tego, co JLCPCB robi bez dopłat.
- **Ekstremalny** — BGA i drobny raster; bezwzględne minimum JLCPCB, niektóre wartości są dodatkowo płatne.

**Dlaczego pierścień wewnętrzny jest większy:** na warstwach wewnętrznych JLCPCB wymaga 0.20 mm od otworu przelotki i 0.30 mm od otworu pinu do obcej miedzi; reguły osiągają to przez pierścień, więc zwykły odstęp się nie zmienia.
**Miedź 2 oz:** ścieżka i odstęp 0.20 (Standard), 0.16 na 2 warstwach / 0.15 na wielowarstwowych (Gęsty, Ekstremalny); pierścień PTH 0.26; mostek maski od 0.20.
**Odstępy w obrębie tego samego sygnału** (`mdSmdPad`, `mdSmdVia`, `mdSmdSmd`) są równe odstępowi między różnymi sygnałami, więc Fusion nie zadaje pytań przy wczytywaniu.

Wartości dla każdego pliku: [rules/README.md](rules/README.md).

---

## Stos warstw i grubość

Reguły zawierają **stos warstw JLCPCB** — warstwy miedzi, prepreg (`+`) i rdzeń (`*`), grubości miedzi i dielektryka. Fusion buduje z nich fizyczny stos (Layer Stack Manager), więc grubość w 3D i w zadaniu Gerber zgadza się z zamówieniem.

| Warstwy | 1.6 mm, 1 oz / 0.5 oz | Dielektryki od góry do dołu, mm |
|---|---|---|
| 2 | `(1*16)` | rdzeń 1.53 |
| 4 | `(1+2*15+16)` | prepreg 7628 0.2104 · rdzeń 1.065 · prepreg 7628 0.2104 |
| 6 | `(1+2*3+14*15+16)` | 3313 0.0994 · rdzeń 0.55 · 2116 0.1164 · rdzeń 0.55 · 3313 0.0994 |
| 8 | `(1+2*3+4*13+14*15+16)` | 2116 0.1164 · rdzeń 0.30 · 1080×2 0.1528 · rdzeń 0.30 · 1080×2 0.1528 · rdzeń 0.30 · 2116 0.1164 |

Wszystkie 77 stosów: [docs/STACKUPS.md](docs/STACKUPS.md). Warstwy wewnętrzne, które już mają miedź, zachowują numery; w przeciwnym razie używane są zwykłe numery (4 warstwy: 2, 15 · 6 warstw: 2, 3, 14, 15 · 8 warstw: 2, 3, 4, 13, 14, 15).

---

## Kontrola wstępna

| Kontrola | Dlaczego |
|---|---|
| Miedź na warstwach spoza wybranego stosu — z listą znalezionych tam ścieżek, wylewek, przelotek, padów i części | zniknęłaby z plików Gerber |
| Brak obrysu płytki (warstwa 20) | bez obrysu nie ma płytki |
| Rozmiar płytki: od 3 × 3 mm do 670 × 600 (2 warstwy), 663 × 593 (4 warstwy), 656 × 586 mm (6–8 warstw) | limity JLCPCB |
| Ścieżki cieńsze i przelotki mniejsze niż minimum profilu; przelotki poniżej 0.3 mm | prognoza DRC i dopłata za małe otwory |
| Otwory niemetalizowane poniżej 0.5 mm | minimum JLCPCB |
| Opisy niższe niż 1.0 mm lub z kreską cieńszą niż 0.15 mm; linie cieńsze niż 0.15 mm | mogą być nieczytelne lub przerwane |
| Klasy sieci poniżej minimum | DRC i trasowanie się nimi kierują |
| Zatwierdzone komunikaty DRC na płytce | zob. uwagę poniżej |

---

## Podsumowanie

Po wczytaniu reguł konfigurator przelicza wylewki (`RATSNEST`), uruchamia DRC i pokazuje, jakie reguły wczytano i gdzie zapisano poprzednie, które klasy sieci podniesiono, gdzie zainstalowano pakiet, **błędy DRC wg rodzaju** (odstęp, miedź przy krawędzi, odstęp otworów, rozmiar wiertła, niepołączone…) z osobno liczonymi ostrzeżeniami i zatwierdzeniami, oraz wskazówki typu «otwory poniżej 0.3 mm są w JLCPCB dodatkowo płatne». Sama lista błędów jest w panelu **ERRORS** Fusion.

---

## Przywracanie poprzednich reguł

Przed każdym uruchomieniem bieżące reguły płytki są zapisywane w `%LOCALAPPDATA%\dmxon_jlc\rules_backup`. Aby je przywrócić, **uruchom konfigurator ponownie** i naciśnij **Przywróć poprzednie reguły** — wracają reguły, stos warstw i klasy sieci, potem wylewki są przeliczane i uruchamia się DRC.

> **Zatwierdzone komunikaty DRC.** Sprawdzenie z nowymi regułami usuwa zatwierdzenia, które przestały pasować, a przywrócenie reguł ich nie odtworzy. Konfigurator ostrzega, gdy płytka ma zatwierdzenia — najpierw zapisz wersję płytki (File → Save / Create Version).

---

## Tryb wsadowy

```
RUN dmxON_JLC_Setup.ulp -batch [-std iso|gost] [-layers 2|4|6|8] [-profile Standard|Dense|Extreme] [-thick 1.6] [-outer 1|2] [-inner 0.5|1|2] [-mask Green] [-vcut] [-open] [-noclass] [-noinstall] [-nofabkit] [-lang en|ru|es|de|pl]
RUN dmxON_JLC_Setup.ulp -export <folder>
```

`-vcut` miedź 0.4 mm od krawędzi · `-open` przelotki bez maski · `-noclass` / `-noinstall` / `-nofabkit` pomiń klasy / pakiet / FabKit · `-lang` język podsumowania · `-export` tylko zapisuje pakiet (12 `.dru` + 4 `.cam`), płytka niepotrzebna. Ustawienia trybu wsadowego nie są zapamiętywane. · `-std iso|gost` norma

---

## Pliki reguł bez konfiguratora

**Reguły:** Fusion — **DRC → Load…** (lub `DRC LOAD 'ścieżka/plik.dru'`), potem **DRC**. EAGLE 9 — **Tools → DRC → File → Load…**.
**Zadanie CAM:** **Manufacturing → CAM Processor → Load job file** → `rules/dmxON_JLCPCB_<N>L.cam` → **Process Job**, spakuj wynik do zip i wgraj na jlcpcb.com.
Pliki reguł zakładają 1.6 mm, 1 oz / 0.5 oz, przelotki pod maską i zwykłe trasowanie; w innych przypadkach użyj **Tylko pliki…** w konfiguratorze.

---

## Razem z dmxON FabKit

[**dmxON FabKit**](https://github.com/AlexSmith2025/dmxON-FabKit-Fusion-Electronics) zamienia płytkę w kompletne zamówienie JLCPCB: zip z plikami Gerber, BOM i CPL z częściami LCSC, raport, dokumentację montażową A4 i arkusze do termotransferu.
Kolejność: `dmxON_JLC_Setup` (reguły, stos, DRC bez błędów) → **zapisz płytkę** (Ctrl+S) → `dmxON_FabKit` (pakiet zamówienia; grubość i kolor maski już wpisane).

> **Zapisz płytkę po konfiguracji.** Fusion eksportuje Gerber z ostatniej *zapisanej* wersji; bez zapisu nowe reguły (pierścienie, przelotki, maska) nie trafią do plików Gerber.

---

## Pytania i problemy

| Pytanie | Odpowiedź |
|---|---|
| Po instalacji brak karty **dmxON** | uruchom ponownie Fusion jeden raz albo włącz dodatek: **Utilities → Add-Ins → Scripts and Add-Ins → dmxON → Run** |
| Jak zaktualizować? | **dmxON → Aktualizacje** sprawdza GitHub i instaluje nowe wersje; dodatek sprawdza też sam raz dziennie |
| Rozpoznano złą liczbę warstw | konfigurator czyta stos płytki i miedź na jej warstwach; wybierz właściwą liczbę z listy |
| «Warstwa N jest poza stosem, a zawiera: …» | uwaga wymienia, co leży na tej warstwie; usuń to z niej lub wybierz więcej warstw |
| Błędy «Drill Size» | w profilach Standard i Gęsty otwory poniżej 0.3 mm są błędem, bo JLCPCB dolicza za nie opłatę; powiększ je lub wybierz Ekstremalny |
| Błędy «Drill Clearance» | otwory bliżej niż odstęp otworów w profilu (0.25 / 0.20 mm) |
| Wiele błędów «miedź przy krawędzi» | Standard trzyma 0.3 mm (V-cut 0.4 mm); dla gęstej płytki użyj profilu Gęsty (0.25) lub Ekstremalny (0.2) |
| Pierścienie padów urosły | reguły ustawiają minimalny pierścień JLCPCB; większy pad z biblioteki pozostaje bez zmian |
| Gdzie są pliki? | reguły płytki i kopie — `%LOCALAPPDATA%\dmxon_jlc`; pakiet — `Dokumenty\EAGLE\design rules` i `\cam` |

---

## Jak to działa

Krok 0 — `DRC SAVE` bieżących reguł (kopia i rzeczywisty stos) · krok 1 — analiza płytki, okno, kontrola wstępna, plik reguł · krok 2 — `DRC LOAD`, `CLASS`, `RATSNEST`, `DRC` · krok 3 — podsumowanie DRC. Szczegóły: [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md) · zmiany: [CHANGELOG.md](CHANGELOG.md). **Dodatek dmxON** (`fusion-addin/dmxON`, Python) robi to, czego nie potrafi ULP: ustawienia folderów Fusion, kartę dmxON, kopie zapasowe i aktualizacje.

```
dmxON-JLC-Rules/
├── dmxON_JLC_Setup.ulp     konfigurator płytki
├── INSTALL.ulp             dodaje projekt do folderów ULP, reguł i CAM Fusion
├── lib/                    jr_core (napisy, pliki, język), jr_lang (teksty es/de/pl), jr_rules (wartości, .dru, .cam), jr_stack (77 stosów)
├── lang/                   strings.tsv — wszystkie teksty interfejsu w pięciu językach
├── rules/                  12 .dru + 4 .cam + README
└── docs/                   ARCHITECTURE.md, STACKUPS.md, assets/
```

Źródła: [możliwości JLCPCB](https://jlcpcb.com/capabilities/pcb-capabilities) · [dopłaty](https://jlcpcb.com/help/article/In-what-cases-will-there-be-charged-extra) · [kalkulator impedancji / stosy](https://jlcpcb.com/impedance). Wartości sprawdzone 2026-10-09; JLCPCB co jakiś czas zmienia możliwości — przed zamówieniem sprawdź ich stronę i raport DFM.

---

## Wesprzyj projekt

dmxON JLC Rules jest **darmowy**. Za nim stoi wiele wieczorów testów w Fusion, analiza możliwości JLCPCB i sprawdzenie każdego stosu co do mikrometra. Jeśli uchronił Cię przed nieudanym zamówieniem, zaoszczędził wieczór z ustawieniami DRC albo po prostu pieniądze — wesprzyj dalszy rozwój: nowe wersje, aktualizacje reguł, gdy JLCPCB zmienia możliwości, i poprawki pod nowe wersje Fusion.

<p align="center">
  <a href="https://www.paypal.com/donate/?business=smith.show2025%40gmail.com&no_recurring=0&item_name=dmxON+JLC+Rules&currency_code=EUR"><img src="docs/assets/donate.pl.svg" alt="Wesprzyj dmxON JLC Rules przez PayPal" width="760"></a>
</p>

<p align="center">
  <b>PayPal:</b> <a href="https://www.paypal.com/donate/?business=smith.show2025%40gmail.com&no_recurring=0&item_name=dmxON+JLC+Rules&currency_code=EUR">smith.show2025@gmail.com</a> — każda kwota pomaga. Dziękuję! ⭐ Gwiazdka na GitHub też pomaga innym znaleźć projekt.
</p>

---

## Licencja

Bezpłatne użycie z podaniem autora; kopiowanie kodu, modyfikacja i użycie komercyjne są zabronione — zob. [LICENSE.md](LICENSE.md). JLCPCB jest znakiem towarowym jego właściciela; projekt nie jest powiązany z JLCPCB.

**dmxON by AlexSmith 2026** · [dmxon512.com](https://dmxon512.com) · projekt siostrzany: [dmxON FabKit](https://github.com/AlexSmith2025/dmxON-FabKit-Fusion-Electronics)
