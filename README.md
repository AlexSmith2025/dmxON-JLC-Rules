# dmxON JLC Rules

**Правила JLCPCB для плат на 2, 4, 6 и 8 слоёв и настройщик, который готовит плату Fusion Electronics к заказу — одной командой.**
**JLCPCB rules for 2, 4, 6 and 8-layer boards and a setup that prepares a Fusion Electronics board for ordering — in one run.**

`v1.0.1` · 2026-10-13 · **dmxON by AlexSmith 2026** · [лицензия / license](LICENSE.md)

Работает в **Autodesk Fusion (Electronics)** и **EAGLE 9**. Весь интерфейс и документация — на русском и английском.
Runs in **Autodesk Fusion (Electronics)** and **EAGLE 9**. The whole interface and documentation are in Russian and English.

---

## Содержание / Contents

- [Что внутри / What is inside](#что-внутри--what-is-inside)
- [Установка / Installation](#установка--installation)
- [Быстрый старт / Quick start](#быстрый-старт--quick-start)
- [Диалог / Dialog](#диалог--dialog)
- [Профили / Profiles](#профили--profiles)
- [Стек слоёв и толщина / Layer stack and thickness](#стек-слоёв-и-толщина--layer-stack-and-thickness)
- [Предварительная проверка / Pre-flight check](#предварительная-проверка--pre-flight-check)
- [Итог / Summary](#итог--summary)
- [Вернуть прежние правила / Restore previous rules](#вернуть-прежние-правила--restore-previous-rules)
- [Пакетный режим / Batch mode](#пакетный-режим--batch-mode)
- [Файлы правил без настройщика / Rule files without the setup](#файлы-правил-без-настройщика--rule-files-without-the-setup)
- [Вместе с dmxON FabKit / Together with dmxON FabKit](#вместе-с-dmxon-fabkit--together-with-dmxon-fabkit)
- [Вопросы и неполадки / FAQ and troubleshooting](#вопросы-и-неполадки--faq-and-troubleshooting)
- [Как устроено / How it works](#как-устроено--how-it-works)
- [Источники / Sources](#источники--sources)

---

## Что внутри / What is inside

| | Русский | English |
|---|---|---|
| 🧭 | **Настройщик `dmxON_JLC_Setup.ulp`** — определяет слои платы, строит правила под JLCPCB, загружает их, проверяет плату и показывает итог | **The `dmxON_JLC_Setup.ulp` setup** — detects the board layers, builds JLCPCB rules, loads them, checks the board and shows a summary |
| 📏 | **12 файлов правил DRC** (`rules/*.dru`): 2, 4, 6, 8 слоёв × профили Стандарт, Плотный, Предельный | **12 DRC rule files** (`rules/*.dru`): 2, 4, 6, 8 layers × Standard, Dense, Extreme profiles |
| 🗂️ | **4 задания CAM** (`rules/*.cam`): Gerber RS-274X и Excellon с именами файлов JLCPCB | **4 CAM jobs** (`rules/*.cam`): Gerber RS-274X and Excellon with JLCPCB file names |
| 🧱 | **77 стеков JLCPCB** (4, 6, 8 слоёв; 0.8–2.0 мм; медь 1–2 oz) — толщины препрегов и ядер как в заказе | **77 JLCPCB stack-ups** (4, 6, 8 layers; 0.8–2.0 mm; 1–2 oz copper) — prepreg and core thicknesses as ordered |
| 🛟 | **Резервная копия** прежних правил перед каждой настройкой и возврат одной кнопкой | **A backup** of the previous rules before every setup and restore with one button |
| 🔎 | **Предварительная проверка** того, что DRC не видит: шелкография, неметаллизированные отверстия, размер платы, медь вне стека | **A pre-flight check** for what DRC does not see: silkscreen, non-plated holes, board size, copper outside the stack |

---

## Установка / Installation

1. Скачайте последнюю версию со страницы [Releases](https://github.com/AlexSmith2025/dmxON-JLC-Rules/releases/latest) (архив **Source code (zip)**) и распакуйте в любую папку, например `Documents\dmxON-JLC-Rules`.
   Download the latest version from [Releases](https://github.com/AlexSmith2025/dmxON-JLC-Rules/releases/latest) (**Source code (zip)**) and unpack it anywhere, e.g. `Documents\dmxON-JLC-Rules`.
2. Структуру не меняйте: `dmxON_JLC_Setup.ulp` ищет модули в `lib\` рядом с собой.
   Keep the layout: `dmxON_JLC_Setup.ulp` loads its modules from `lib\` next to it.
3. По желанию добавьте папку в пути ULP: **Electronics → Preferences → Directories → ULPs** — тогда хватит `RUN dmxON_JLC_Setup`.
   Optionally add the folder to the ULP paths: **Electronics → Preferences → Directories → ULPs** — then `RUN dmxON_JLC_Setup` is enough.

Требования / Requirements: Windows 10/11, Fusion (Electronics) или EAGLE 9. Интернет не нужен. / Internet is not needed.

---

## Быстрый старт / Quick start

1. Откройте **плату** (Board) в Fusion Electronics. / Open the **board** in Fusion Electronics.
2. Запустите / Run: **Automation → Run ULP → `dmxON_JLC_Setup.ulp`**
   или в командной строке / or in the command line:
   ```
   RUN 'C:/путь/path/dmxON_JLC_Setup.ulp'
   ```
3. Проверьте число слоёв, профиль и толщину; предпросмотр внизу покажет все значения, стек и замечания по плате.
   Check the layer count, profile and thickness; the preview below shows every value, the stack and the board findings.
4. Нажмите **Настроить / Apply**. Через несколько секунд появится итог с результатом DRC.
   Press **Apply**. A few seconds later the summary with the DRC result appears.

Лучше всего запускать настройщик **до разводки** (тогда трассировка сразу идёт по правилам JLCPCB) и **ещё раз перед выгрузкой**.
Best run the setup **before routing** (so routing follows the JLCPCB rules from the start) and **once more before export**.

---

## Диалог / Dialog

| Поле / Field | Что задаёт / What it sets |
|---|---|
| **Слоёв меди / Copper layers** | 2, 4, 6, 8. По умолчанию — сколько найдено в стеке платы и по меди на слоях. / By default — what the board stack and the copper on the layers say. |
| **Профиль / Profile** | Стандарт, Плотный, Предельный — см. [Профили](#профили--profiles). / Standard, Dense, Extreme — see [Profiles](#профили--profiles). |
| **Толщина, мм / Thickness, mm** | 0.4–2.0. Для 4–8 слоёв JLCPCB делает 0.8–2.0; если выбрано то, чего нет, берётся ближайшее и пишется замечание. / For 4–8 layers JLCPCB makes 0.8–2.0; an unavailable choice falls back to the nearest one with a note. |
| **Медь снаружи / Outer copper** | 1 oz (35 мкм) или 2 oz (70 мкм). 2 oz требует более широких дорожек и зазоров. / 1 oz (35 µm) or 2 oz (70 µm). 2 oz needs wider tracks and gaps. |
| **Медь внутри / Inner copper** | 0.5, 1, 2 oz — только для 4–8 слоёв. / 0.5, 1, 2 oz — only for 4–8 layers. |
| **Цвет маски / Mask colour** | Для подсказки о перемычке маски (0.10 мм; белая и чёрная — 0.13 мм) и для dmxON FabKit. / For the mask dam hint (0.10 mm; white and black — 0.13 mm) and for dmxON FabKit. |
| **Переходные под маской / Tented vias** | Переходные со сверлом до 0.5 мм закрываются маской (как «Tented» на странице заказа). / Vias drilled up to 0.5 mm are covered by mask (like «Tented» on the order page). |
| **Панель V-cut / V-cut panel** | Медь не ближе 0.4 мм к краю. / Copper at least 0.4 mm from the edge. |
| **Классы цепей не ниже минимума / Net classes not below the minimum** | Классы, у которых ширина, зазор или сверло меньше минимума профиля, поднимаются; класс 0 получает минимум как значение по умолчанию для разводки. / Classes with width, clearance or drill below the profile minimum are raised; class 0 gets the minimum as the routing default. |
| **Пакет правил и CAM — в Документы/EAGLE / Rule pack and CAM into Documents/EAGLE** | Все 12 файлов правил, файл под вашу плату и задание CAM кладутся в `Documents\EAGLE\design rules` и `Documents\EAGLE\cam` (или `Documents\dmxON JLC Rules\…`). В папку программы Fusion ничего не пишется. / All 12 rule files, the file for your board and the CAM job go into `Documents\EAGLE\design rules` and `Documents\EAGLE\cam` (or `Documents\dmxON JLC Rules\…`). Nothing is written into the Fusion program folder. |
| **Толщину и маску — в dmxON FabKit / Thickness and mask to dmxON FabKit** | Если у вас есть [dmxON FabKit](https://github.com/AlexSmith2025/dmxON-FabKit), он возьмёт эти значения для заказа. / If you use dmxON FabKit, it takes these values for the order. |

Кнопки / Buttons: **Настроить / Apply** · **Только файлы… / Files only…** (записать `.dru` и `.cam` под выбранные параметры в любую папку, плату не трогать / write `.dru` and `.cam` for the chosen settings into any folder without touching the board) · **Вернуть прежние правила / Restore previous rules** (если плата уже настраивалась / if the board was set up before) · **Отмена / Cancel**.

---

## Профили / Profiles

Все размеры в миллиметрах, медь 1 oz. / All sizes in millimetres, 1 oz copper.

| мм / mm | 2 слоя Стандарт | 4–8 слоёв Стандарт | 2 слоя Плотный | 4–8 слоёв Плотный | 2 слоя Предельный | 4–8 слоёв Предельный |
|---|---|---|---|---|---|---|
| Дорожка и зазор / Track and space | 0.127 | 0.127 | 0.10 | 0.10 | 0.10 | 0.09 ¹ |
| Площадки разных цепей / Pad to pad | 0.15 | 0.15 | 0.15 | 0.15 | 0.10 | 0.09 |
| Переходное: сверло / диаметр · Via drill / diameter | 0.3 / 0.45 | 0.3 / 0.45 | 0.3 / 0.40 | 0.3 / 0.40 | 0.15 / 0.25 ² | 0.15 / 0.25 ² |
| Поясок переходного внутри / Via ring, inner | — | 0.08 | — | 0.10 | — | 0.11 |
| Поясок вывода / PTH ring | 0.25 | 0.20 | 0.18 | 0.15 | 0.18 | 0.15 |
| Поясок вывода внутри / PTH ring, inner | — | 0.20 | — | 0.20 | — | 0.21 |
| Наименьшее сверло / Min drill | 0.3 | 0.3 | 0.3 | 0.3 | 0.15 ² | 0.15 ² |
| Медь до края / Copper to edge | 0.30 | 0.30 | 0.25 | 0.25 | 0.20 | 0.20 |
| Между отверстиями / Hole to hole | 0.25 | 0.25 | 0.20 | 0.20 | 0.20 | 0.20 |
| Маска на сторону / Mask expansion | 0.05 | 0.05 | 0.05 | 0.05 | 0.05 | 0.05 |

¹ Дорожки 3–3.5 mil на многослойных платах — **+20 %** к цене. / 3–3.5 mil tracks on multilayer boards — **+20 %** price.
² Отверстия меньше 0.3 мм — доплата; на странице заказа выберите **Min via hole size**. / Holes under 0.3 mm cost extra; choose **Min via hole size** on the order page.

- **Стандарт / Standard** — для большинства плат: с запасом по технологии и без доплат. / For most boards: technological margin and no surcharges.
- **Плотный / Dense** — плотный монтаж на пределе того, что JLCPCB делает без доплаты. / Dense layouts at the limit of what JLCPCB makes without surcharge.
- **Предельный / Extreme** — BGA и мелкий шаг; абсолютный минимум JLCPCB, часть значений платная. / BGA and fine pitch; the JLCPCB absolute minimum, some values cost extra.

**Почему поясок внутри больше.** Во внутренних слоях JLCPCB требует от отверстия переходного до чужой меди 0.20 мм, а от отверстия вывода — 0.30 мм. Правила добирают это пояском, чтобы обычный зазор не рос.
**Why the inner ring is larger.** On inner layers JLCPCB needs 0.20 mm from a via hole and 0.30 mm from a pin hole to foreign copper. The rules get there through the ring so the normal clearance stays the same.

**Медь 2 oz.** Дорожка и зазор — 0.20 (Стандарт), 0.16 на 2 слоях и 0.15 на многослойных (Плотный и Предельный); поясок вывода 0.26; перемычка маски от 0.20.
**2 oz copper.** Track and space 0.20 (Standard), 0.16 on 2 layers and 0.15 on multilayer boards (Dense and Extreme); PTH ring 0.26; mask dam from 0.20.

**Зазоры внутри одной цепи** (`mdSmdPad`, `mdSmdVia`, `mdSmdSmd`) равны зазору разных цепей — так Fusion не задаёт лишних вопросов при загрузке правил.
**Same-signal clearances** (`mdSmdPad`, `mdSmdVia`, `mdSmdSmd`) equal the different-signal clearance — so Fusion asks no extra questions when loading the rules.

Полная таблица по каждому файлу — [rules/README.md](rules/README.md). / The full per-file table — [rules/README.md](rules/README.md).

---

## Стек слоёв и толщина / Layer stack and thickness

Правила содержат **стек JLCPCB**: какие слои меди есть, где препрег (`+`), где ядро (`*`), толщины меди и диэлектриков. Fusion строит по ним физический стек (Layer Stack Manager) — толщина в 3D и в задании Gerber совпадает с тем, что вы закажете.
The rules carry the **JLCPCB stack-up**: which copper layers exist, where prepreg (`+`) and core (`*`) are, copper and dielectric thicknesses. Fusion builds the physical stack (Layer Stack Manager) from them — the 3D and Gerber job thickness matches what you order.

| Слои / Layers | 1.6 мм, 1 oz / 0.5 oz | Диэлектрики сверху вниз, мм / Dielectrics top to bottom, mm |
|---|---|---|
| 2 | `(1*16)` | ядро / core 1.53 |
| 4 | `(1+2*15+16)` | препрег 7628 0.2104 · ядро 1.065 · препрег 7628 0.2104 |
| 6 | `(1+2*3+14*15+16)` | 3313 0.0994 · ядро 0.55 · 2116 0.1164 · ядро 0.55 · 3313 0.0994 |
| 8 | `(1+2*3+4*13+14*15+16)` | 2116 0.1164 · ядро 0.30 · 1080×2 0.1528 · ядро 0.30 · 1080×2 0.1528 · ядро 0.30 · 2116 0.1164 |

Все 77 стеков для других толщин и меди — [docs/STACKUPS.md](docs/STACKUPS.md). / All 77 stack-ups for other thicknesses and copper — [docs/STACKUPS.md](docs/STACKUPS.md).

**Номера внутренних слоёв.** Если на плате уже есть медь на внутренних слоях (например, полигон земли на слое 2), их номера сохраняются. Если стек платы уже нужного размера — сохраняется и он. Иначе берутся привычные номера: 4 слоя — 2, 15; 6 слоёв — 2, 3, 14, 15; 8 слоёв — 2, 3, 4, 13, 14, 15.
**Inner layer numbers.** If inner layers already carry copper (e.g. a ground pour on layer 2), their numbers are kept. If the board stack already has the right size, it is kept too. Otherwise the usual numbers are used: 4 layers — 2, 15; 6 layers — 2, 3, 14, 15; 8 layers — 2, 3, 4, 13, 14, 15.

---

## Предварительная проверка / Pre-flight check

Видна прямо в диалоге и повторяется в итоге. / Shown right in the dialog and repeated in the summary.

| Проверка / Check | Почему / Why |
|---|---|
| Медь на слоях вне выбранного стека — с перечнем, что именно там лежит / Copper on layers outside the chosen stack — listing what exactly is there | при уменьшении числа слоёв медь пропала бы из Gerber / it would vanish from Gerber when reducing the layer count |
| Нет контура (слой 20) / No outline (layer 20) | без контура плату не изготовить / no board without an outline |
| Размер платы / Board size | от 3 × 3 мм до 670 × 600 (2 слоя), 663 × 593 (4 слоя), 656 × 586 мм (6–8 слоёв) / from 3 × 3 mm up to the JLCPCB maximum |
| Дорожки тоньше минимума профиля / Tracks thinner than the profile minimum | прогноз того, что отметит DRC / a forecast of what DRC will flag |
| Переходные меньше минимума и меньше 0.3 мм / Vias below the minimum and below 0.3 mm | DRC и доплата за малые отверстия / DRC and the small-hole surcharge |
| Неметаллизированные отверстия меньше 0.5 мм / Non-plated holes under 0.5 mm | минимум JLCPCB / the JLCPCB minimum |
| Надписи шелкографии ниже 1.0 мм и с линией тоньше 0.15 мм / Silkscreen texts under 1.0 mm or with strokes under 0.15 mm | могут не читаться / may be unreadable |
| Линии шелкографии тоньше 0.15 мм / Silkscreen lines under 0.15 mm | напечатаются тонко или с разрывами / print thin or broken |
| Классы цепей ниже минимума / Net classes below the minimum | DRC и разводка по ним / DRC and routing follow them |
| Одобренные ошибки DRC / Approved DRC messages | см. ниже / see below |

---

## Итог / Summary

После загрузки правил настройщик пересчитывает полигоны (`RATSNEST`), запускает DRC и показывает:
After loading the rules the setup recalculates polygons (`RATSNEST`), runs DRC and shows:

- какие правила загружены и куда сохранена копия прежних / which rules were loaded and where the previous ones were backed up;
- какие классы цепей подняты (было → стало) / which net classes were raised (before → after);
- куда установлен пакет правил и задание CAM / where the rule pack and CAM job were installed;
- **ошибки DRC по видам** с переводом (зазор, медь у края, сверло, неразведённые соединения…), отдельно — предупреждения и одобренные / **DRC errors by type** with a translation, warnings and approvals counted separately;
- подсказки: например, что отверстия меньше 0.3 мм у JLCPCB платные / hints, e.g. that holes under 0.3 mm cost extra at JLCPCB;
- замечания предварительной проверки и профиля / pre-flight and profile notes.

Сам список ошибок — в панели **ERRORS** Fusion. / The error list itself is in the Fusion **ERRORS** panel.

---

## Вернуть прежние правила / Restore previous rules

Перед каждой настройкой текущие правила платы сохраняются в `%LOCALAPPDATA%\dmxon_jlc\rules_backup`. Чтобы вернуть их, **запустите настройщик ещё раз** и нажмите **«Вернуть прежние правила»**: вернутся правила, стек и классы цепей, затем полигоны пересчитаются и пройдёт DRC.
Before every setup the board's current rules are saved to `%LOCALAPPDATA%\dmxon_jlc\rules_backup`. To bring them back, **run the setup again** and press **«Restore previous rules»**: rules, stack and net classes return, then polygons are recalculated and DRC runs.

> Кнопки возврата нет в окне итога намеренно: менять правила в той же цепочке команд сразу после DRC небезопасно для Fusion.
> The summary window has no restore button on purpose: changing rules in the same command chain right after DRC is unsafe for Fusion.

> **Одобренные ошибки DRC.** Проверка с новыми правилами удаляет одобрения, которые перестали совпадать, и возврат правил их не восстанавливает. Если на плате есть одобренные ошибки, настройщик предупредит — **сохраните версию платы перед настройкой** (File → Save / Create Version).
> **Approved DRC messages.** A check with new rules drops approvals that no longer match, and restoring the rules does not bring them back. The setup warns if the board has approvals — **save a board version first** (File → Save / Create Version).

---

## Пакетный режим / Batch mode

```
RUN dmxON_JLC_Setup.ulp -batch [-layers 2|4|6|8] [-profile Standard|Dense|Extreme] [-thick 1.6] [-outer 1|2] [-inner 0.5|1|2] [-mask Green] [-vcut] [-open] [-noclass] [-noinstall] [-nofabkit]
RUN dmxON_JLC_Setup.ulp -export <папка/folder>
```

| Ключ / Flag | Значение / Meaning |
|---|---|
| `-batch` | без диалога; не указанное — как определено или как в прошлый раз / no dialog; anything not given — as detected or as last time |
| `-layers N` | 2, 4, 6 или 8 / 2, 4, 6 or 8 |
| `-profile P` | `Standard`, `Dense`, `Extreme` |
| `-thick T` | толщина платы, мм / board thickness, mm |
| `-outer`, `-inner` | медь снаружи и внутри, oz / outer and inner copper, oz |
| `-mask C` | `Green`, `Purple`, `Red`, `Yellow`, `Blue`, `White`, `Black` |
| `-vcut` | панель V-cut: медь от края 0.4 мм / V-cut panel: copper 0.4 mm from the edge |
| `-open` | переходные без маски / untented vias |
| `-noclass`, `-noinstall`, `-nofabkit` | не трогать классы / не ставить пакет / не передавать в FabKit / leave classes / skip the pack / skip FabKit |
| `-export <folder>` | только записать пакет (12 `.dru` + 4 `.cam`); плата не нужна / only write the pack; no board needed |

Настройки пакетного режима не запоминаются. / Batch settings are not remembered.

---

## Файлы правил без настройщика / Rule files without the setup

**Правила / Rules.** Fusion: **DRC → Load…** (или `DRC LOAD 'путь/файл.dru'`), затем **DRC**. EAGLE 9: **Tools → DRC → File → Load…**.
Fusion: **DRC → Load…** (or `DRC LOAD 'path/file.dru'`), then **DRC**. EAGLE 9: **Tools → DRC → File → Load…**.

**Задание CAM / CAM job.** **Manufacturing → CAM Processor → Load job file** → `rules/dmxON_JLCPCB_<N>L.cam` → **Process Job**. Получатся файлы `плата_copper_l1.GTL`, `….G1`, `….GBL`, `….GTS`, `….GTO`, `….GKO`, `плата_drill.XLN` и т. д. — заархивируйте их и загрузите на jlcpcb.com.
You get `board_copper_l1.GTL`, `….G1`, `….GBL`, `….GTS`, `….GTO`, `….GKO`, `board_drill.XLN` and so on — zip them and upload to jlcpcb.com.

Файлы правил рассчитаны на 1.6 мм, медь 1 oz / 0.5 oz, переходные под маской и обычную фрезеровку. Для других параметров используйте **Только файлы…** в настройщике.
The rule files assume 1.6 mm, 1 oz / 0.5 oz copper, tented vias and regular routing. For other settings use **Files only…** in the setup.

---

## Вместе с dmxON FabKit / Together with dmxON FabKit

[**dmxON FabKit**](https://github.com/AlexSmith2025/dmxON-FabKit) собирает из платы полный пакет для JLCPCB: Gerber с архивом, BOM и CPL с подбором деталей, отчёт, документацию A4 и листы ЛУТ. Порядок работы:
[**dmxON FabKit**](https://github.com/AlexSmith2025/dmxON-FabKit) builds a complete JLCPCB package from the board: zipped Gerber, BOM and CPL with part selection, a report, A4 documentation and toner-transfer sheets. Workflow:

1. `dmxON_JLC_Setup` — правила и стек JLCPCB, DRC без ошибок. / JLCPCB rules and stack, DRC clean.
2. `dmxON_FabKit` — пакет для заказа; толщина платы и цвет маски уже подставлены. / The order package; board thickness and mask colour already filled in.

---

## Вопросы и неполадки / FAQ and troubleshooting

| Вопрос / Question | Ответ / Answer |
|---|---|
| Определилось не то число слоёв / Wrong layer count detected | настройщик смотрит на стек платы и медь на слоях; выберите нужное число в списке / the setup looks at the board stack and the copper on the layers; pick the right number in the list |
| «Слой N не входит в стек, а на нём: …» / «Layer N is outside the stack-up but holds: …» | в замечании перечислено, что лежит на слое (дорожки и полигоны цепей, переходные, площадки и графика деталей); уберите это со слоя или выберите больше слоёв / the finding lists what is on the layer; move it off the layer or choose more layers |
| Ошибки «сверло меньше минимума» / «Drill Size» errors | в профилях Стандарт и Плотный отверстия меньше 0.3 мм считаются ошибкой — у JLCPCB они платные; увеличьте сверло или выберите Предельный / in Standard and Dense holes under 0.3 mm are errors because JLCPCB charges for them; enlarge them or choose Extreme |
| Много «медь у края» / Many «copper to edge» errors | Стандарт держит 0.3 мм; для плотной платы — Плотный (0.25) или Предельный (0.2) / Standard keeps 0.3 mm; for a dense board use Dense (0.25) or Extreme (0.2) |
| Пояски площадок стали больше / Pad rings got larger | правила задают минимальный поясок JLCPCB; если площадка в библиотеке больше — используется она / the rules set the JLCPCB minimum ring; a larger library pad is kept |
| Пропали одобренные ошибки / Approved messages are gone | так работает DRC с новыми правилами; откатитесь на сохранённую версию платы / that is how DRC behaves with new rules; go back to a saved board version |
| Где файлы? / Where are the files? | правила под плату и копии — `%LOCALAPPDATA%\dmxon_jlc`, пакет — `Documents\EAGLE\design rules` и `\cam` / board rules and backups — `%LOCALAPPDATA%\dmxon_jlc`, the pack — `Documents\EAGLE\design rules` and `\cam` |

---

## Как устроено / How it works

Подробно — [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md). Коротко: шаг 0 — `DRC SAVE` текущих правил (копия и настоящий стек); шаг 1 — разбор платы, диалог, предварительная проверка, файл правил; шаг 2 — `DRC LOAD`, `CLASS`, `RATSNEST`, `DRC`; шаг 3 — итог по ошибкам DRC.
Details — [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md). In short: step 0 — `DRC SAVE` of the current rules (backup and the real stack); step 1 — board scan, dialog, pre-flight check, rule file; step 2 — `DRC LOAD`, `CLASS`, `RATSNEST`, `DRC`; step 3 — a summary of the DRC errors.

```
dmxON-JLC-Rules/
├── dmxON_JLC_Setup.ulp     настройщик / the setup
├── lib/
│   ├── jr_core.ulp         версия, строки, файлы, команды / version, strings, files, commands
│   ├── jr_rules.ulp        значения профилей, стек, .dru, .cam / profile values, stack, .dru, .cam
│   └── jr_stack.ulp        77 стеков JLCPCB / 77 JLCPCB stack-ups
├── rules/                  12 .dru + 4 .cam + README
└── docs/                   ARCHITECTURE.md, STACKUPS.md
```

История версий / Changelog — [CHANGELOG.md](CHANGELOG.md).

---

## Источники / Sources

- Возможности JLCPCB / JLCPCB capabilities: <https://jlcpcb.com/capabilities/pcb-capabilities>
- Доплаты / Extra charges: <https://jlcpcb.com/help/article/In-what-cases-will-there-be-charged-extra>
- Стеки и Er / Stack-ups and Er: калькулятор импеданса JLCPCB / the JLCPCB impedance calculator, <https://jlcpcb.com/impedance>

Значения проверены 2026-10-09. JLCPCB иногда меняет возможности и цены — перед заказом сверяйтесь с их страницей и отчётом DFM.
Values checked on 2026-10-09. JLCPCB changes capabilities and prices from time to time — check their page and the DFM report before ordering.

---

## Лицензия / License

Бесплатно с указанием автора; копирование кода, изменение и коммерческое использование запрещены — см. [LICENSE.md](LICENSE.md).
Free to use with attribution; copying the code, modification and commercial use are not permitted — see [LICENSE.md](LICENSE.md).

JLCPCB — товарный знак его владельца; проект с JLCPCB не связан. / JLCPCB is a trademark of its owner; this project is not affiliated with JLCPCB.

**dmxON by AlexSmith 2026**
