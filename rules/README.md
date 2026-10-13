# Пакет правил JLCPCB / JLCPCB rule pack

**Правила DRC и задания CAM под JLCPCB для плат на 2, 4, 6 и 8 слоёв — для Fusion Electronics и EAGLE 9.**
**JLCPCB DRC rules and CAM jobs for 2, 4, 6 and 8-layer boards — for Fusion Electronics and EAGLE 9.**

Часть [dmxON JLC Rules](../README.md) · **dmxON by AlexSmith 2026** · [лицензия / license](../LICENSE.md)

> Проще всего — не ставить файлы вручную, а запустить настройщик `dmxON_JLC_Setup.ulp`: он сам определит слои платы, подберёт стек JLCPCB для любой толщины и меди, загрузит правила, проверит плату и покажет итог. См. [README](../README.ru.md#быстрый-старт) / see [README](../README.md#quick-start).
> The easiest way is not to install the files by hand but to run the `dmxON_JLC_Setup.ulp` setup: it detects the board layers, picks the JLCPCB stack-up for any thickness and copper, loads the rules, checks the board and shows a summary.

---

## Что в папке / What is inside

| Файл / File | Что это / What it is |
|---|---|
| `dmxON_JLCPCB_2L_Standard.dru` … `8L_Standard.dru` | **Стандарт** — с запасом, без доплат. Рекомендуется для большинства плат. / **Standard** — with margin, no extra cost. Recommended for most boards. |
| `dmxON_JLCPCB_2L_Dense.dru` … `8L_Dense.dru` | **Плотный** — на пределе того, что JLCPCB делает без доплаты. / **Dense** — at the limit of what JLCPCB makes without surcharge. |
| `dmxON_JLCPCB_2L_Extreme.dru` … `8L_Extreme.dru` | **Предельный** — абсолютный минимум JLCPCB; отдельные значения стоят дороже. / **Extreme** — the JLCPCB absolute minimum; some values cost extra. |
| `dmxON_JLCPCB_2L.cam` … `8L.cam` | Задания CAM: Gerber RS-274X и Excellon с именами файлов JLCPCB (GTL, G1…, GBL, GTS, GBS, GTP, GBP, GTO, GBO, GKO, XLN). / CAM jobs: Gerber RS-274X and Excellon with JLCPCB file names. |

Файлы правил рассчитаны на плату **1.6 мм, медь 1 oz снаружи и 0.5 oz внутри, переходные под маской, обычная фрезеровка**. Для другой толщины, меди 2 oz, панели с V-cut или открытых переходных настройщик создаёт свой файл с точным стеком JLCPCB.
The rule files assume a **1.6 mm board, 1 oz outer and 0.5 oz inner copper, tented vias, regular routing**. For another thickness, 2 oz copper, a V-cut panel or untented vias the setup writes its own file with the exact JLCPCB stack-up.

---

## Значения / Values

Все размеры в миллиметрах. / All sizes in millimetres.

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
| Переходные под маской до / Tented vias up to | 0.5 | 0.5 | 0.5 | 0.5 | 0.5 | 0.5 |

¹ Дорожки 3–3.5 mil на многослойных платах — **+20 %** к цене. / 3–3.5 mil tracks on multilayer boards — **+20 %** price.
² Отверстия меньше 0.3 мм — доплата; на странице заказа выберите **Min via hole size**. / Holes under 0.3 mm cost extra; choose **Min via hole size** on the order page.

**Почему поясок внутри больше.** Во внутренних слоях JLCPCB требует от отверстия переходного до чужой меди 0.20 мм, а от отверстия вывода — 0.30 мм; правила добирают это пояском, чтобы обычный зазор оставался прежним.
**Why the inner ring is larger.** On inner layers JLCPCB needs 0.20 mm from a via hole and 0.30 mm from a pin hole to foreign copper; the rules get there through the ring so the normal clearance stays the same.

**Медь 2 oz.** Дорожка и зазор — 0.20 (Стандарт), 0.16 на 2 слоях и 0.15 на многослойных (Плотный и Предельный); поясок вывода 0.26; перемычка маски от 0.20.
**2 oz copper.** Track and space 0.20 (Standard), 0.16 on 2 layers and 0.15 on multilayer boards (Dense and Extreme); PTH ring 0.26; mask dam from 0.20.

**Перемычка маски** между площадками: 0.10 мм для зелёной, красной, жёлтой, синей и фиолетовой маски, 0.13 мм — для белой и чёрной.
**Mask dam** between pads: 0.10 mm for green, red, yellow, blue and purple, 0.13 mm for white and black.

**V-cut.** У панели с V-cut медь должна стоять от края не ближе 0.4 мм — в настройщике есть флажок.
**V-cut.** On a V-cut panel copper must stay at least 0.4 mm from the edge — the setup has a checkbox for it.

---

## Стеки слоёв 1.6 мм / Stack-ups, 1.6 mm

Стандартные стеки JLCPCB («No requirement» на странице заказа), медь 1 oz снаружи и 0.5 oz внутри. Медь внутри после обработки — 0.0152 мм.
JLCPCB default stack-ups («No requirement» on the order page), 1 oz outer and 0.5 oz inner copper. Inner copper after processing is 0.0152 mm.

| Слои / Layers | Стек в правилах / Rule stack | Диэлектрики сверху вниз, мм / Dielectrics top to bottom, mm | Итого / Total |
|---|---|---|---|
| 2 | `(1*16)` | ядро / core 1.53 | 1.60 |
| 4 | `(1+2*15+16)` | препрег 7628 0.2104 · ядро 1.065 · препрег 7628 0.2104 | 1.586 |
| 6 | `(1+2*3+14*15+16)` | 3313 0.0994 · ядро 0.55 · 2116 0.1164 · ядро 0.55 · 3313 0.0994 | 1.546 |
| 8 | `(1+2*3+4*13+14*15+16)` | 2116 0.1164 · ядро 0.30 · 1080×2 0.1528 · ядро 0.30 · 1080×2 0.1528 · ядро 0.30 · 2116 0.1164 | 1.600 |

`+` — препрег, `*` — ядро. Fusion строит по этим числам физический стек платы (Layer Stack Manager), так что толщина в 3D и в задании Gerber совпадает с заказом. Настройщик знает все стеки JLCPCB для 4, 6 и 8 слоёв толщиной 0.8–2.0 мм с медью 1–2 oz — [docs/STACKUPS.md](../docs/STACKUPS.md).
`+` is prepreg, `*` is core. Fusion builds the physical board stack (Layer Stack Manager) from these numbers, so the 3D and Gerber job thickness matches the order. The setup knows every JLCPCB stack-up for 4, 6 and 8 layers, 0.8–2.0 mm, 1–2 oz copper — [docs/STACKUPS.md](../docs/STACKUPS.md).

---

## Ручная установка / Manual installation

**Правила / Rules.** Fusion: **DRC → Load…** (или команда `DRC LOAD 'путь/файл.dru'`), затем **DRC**. EAGLE 9: **Tools → DRC → File → Load…**.
Fusion: **DRC → Load…** (or the `DRC LOAD 'path/file.dru'` command), then **DRC**. EAGLE 9: **Tools → DRC → File → Load…**.

**Задание CAM / CAM job.** **Manufacturing → CAM Processor → Load job file** → `dmxON_JLCPCB_<N>L.cam` → **Process Job**. Номера внутренних слоёв в задании — как в стеке выше (6 слоёв: 2, 3, 14, 15). Если у платы другие номера, настройщик запишет задание под них.
Inner layer numbers in the job follow the stack above (6 layers: 2, 3, 14, 15). If the board uses other numbers, the setup writes a job for them.

> [**dmxON FabKit**](https://github.com/AlexSmith2025/dmxON-FabKit) делает Gerber сам (с именами JLCPCB и архивом) — задание CAM нужно, только если вы выгружаете вручную.
> [**dmxON FabKit**](https://github.com/AlexSmith2025/dmxON-FabKit) produces Gerber itself (JLCPCB names and zip) — the CAM job is only needed for manual export.

---

## Откуда значения / Where the values come from

- Возможности JLCPCB / JLCPCB capabilities: <https://jlcpcb.com/capabilities/pcb-capabilities>
- Доплаты / Extra charges: <https://jlcpcb.com/help/article/In-what-cases-will-there-be-charged-extra>
- Стеки и Er / Stack-ups and Er: калькулятор импеданса JLCPCB / the JLCPCB impedance calculator, <https://jlcpcb.com/impedance>

Значения проверены 2026-10-09. JLCPCB иногда меняет возможности и цены — перед заказом сверяйтесь с их страницей и отчётом DFM.
Values checked on 2026-10-09. JLCPCB changes capabilities and prices from time to time — check their page and the DFM report before ordering.
