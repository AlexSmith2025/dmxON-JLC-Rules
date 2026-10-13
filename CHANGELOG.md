# История версий / Changelog

Версия меняется при каждой переделке: `JR_VERSION` и `JR_DATE` в `lib/jr_core.ulp`, файл `VERSION`, пакет `rules/` (пересобрать `-export`) и запись здесь.
The version is bumped on every change: `JR_VERSION` and `JR_DATE` in `lib/jr_core.ulp`, the `VERSION` file, the `rules/` pack (rebuild with `-export`) and an entry here.

Нумерация / Numbering: `MAJOR.MINOR.PATCH` — новая возможность → MINOR, исправление → PATCH.
New feature → MINOR, fix → PATCH.

---

## 1.0.3 — 2026-10-13

**Изменено / Changed**

- Репозиторий переименован в **dmxON-JLC-Rules-Fusion-Electronics** — так его проще найти по запросу «Fusion Electronics». Ссылки в программе и документации обновлены; старые адреса GitHub перенаправляет сам.
  The repository is renamed to **dmxON-JLC-Rules-Fusion-Electronics** so it is easier to find when searching for «Fusion Electronics». Links in the program and docs are updated; GitHub redirects the old addresses.

---

## 1.0.2 — 2026-10-13

**Изменено / Changed**

- В окне итога — строка поддержки проекта (PayPal) и ссылка на GitHub; ссылки открываются в браузере.
  The summary window shows a support line (PayPal) and a GitHub link; links open in the browser.
- README на английском (главная страница) и на русском (`README.ru.md`): баннер, значки версии и скачиваний, кнопка «Скачать», таблица совместимости по программам и версиям.
  README in English (main page) and Russian (`README.ru.md`): banner, version and download badges, a Download button, a compatibility table by program and version.
- README: после настройки сохраните плату — Gerber Fusion делает из последней сохранённой версии.
  README: save the board after the setup — Fusion exports Gerber from the last saved version.
- В релизе — готовый архив `dmxON-JLC-Rules.zip` (постоянная ссылка на последнюю версию).
  Releases carry a ready `dmxON-JLC-Rules.zip` (a permanent link to the latest version).

---

## 1.0.1 — 2026-10-13

**Исправлено / Fixed**

- Итог DRC: «Drill Clearance» (расстояние между отверстиями) больше не переводится как «сверло меньше минимума», и подсказка про платные отверстия меньше 0.3 мм появляется только при настоящих ошибках размера сверла. Перевод сверен со всеми названиями ошибок Fusion и EAGLE, включая новые («Maximum Drill Size», «Minimum PTH Drill Size», «Soldermask - Silkscreen Clearance»).
  DRC summary: «Drill Clearance» (hole spacing) is no longer reported as «drill below minimum», and the hint about paid holes under 0.3 mm shows only for real drill-size errors. The translation is checked against every Fusion and EAGLE error name, including the new ones.
- Замечание «медь вне стека» теперь по каждому слою и говорит, что на нём лежит: дорожки и полигоны каких цепей, переходные, линии, тексты, площадки и графика каких деталей. Если Fusion отмечает слой занятым, а объектов нет, — так и пишет.
  The «copper outside the stack-up» finding now goes layer by layer and says what is there: tracks and pours of which nets, vias, lines, texts, pads and graphics of which parts. If Fusion marks a layer as used but nothing is found, it says so.

---

## 1.0.0 — 2026-10-09

Первый выпуск dmxON JLC Rules. / First release of dmxON JLC Rules.

**Новое / New**

- Пакет правил DRC для 2, 4, 6 и 8 слоёв в трёх профилях: Стандарт (с запасом, без доплат), Плотный (предел без доплат), Предельный (минимум JLCPCB).
  DRC rule pack for 2, 4, 6 and 8 layers in three profiles: Standard (with margin, no extra cost), Dense (no-surcharge limit), Extreme (JLCPCB minimum).
- Задания CAM для 2, 4, 6 и 8 слоёв с именами файлов JLCPCB (GTL, G1…, GBL, GTS, GBS, GTP, GBP, GTO, GBO, GKO, XLN).
  CAM jobs for 2, 4, 6 and 8 layers with JLCPCB file names.
- Таблица 77 стеков JLCPCB (4, 6, 8 слоёв; 0.8–2.0 мм; медь 1–2 oz): Fusion строит по правилам физический стек и толщину платы.
  A table of 77 JLCPCB stack-ups (4, 6, 8 layers; 0.8–2.0 mm; 1–2 oz copper): Fusion builds the physical stack and board thickness from the rules.
- Настройщик `dmxON_JLC_Setup.ulp`: резервная копия правил, определение слоёв по стеку и меди, правила под любую толщину и медь, V-cut, переходные с маской или без, классы цепей, установка пакета в папки пользователя, предварительная проверка, загрузка правил, пересчёт полигонов, DRC и итог по видам ошибок; возврат прежних правил; пакетный режим и `-export`.
  The `dmxON_JLC_Setup.ulp` setup: rule backup, layer detection from the stack and copper, rules for any thickness and copper, V-cut, tented or open vias, net classes, pack installation into user folders, pre-flight check, rule loading, polygon recalculation, DRC and a summary by error type; restore of the previous rules; batch mode and `-export`.
- Передача толщины и цвета маски в dmxON FabKit.
  Thickness and mask colour passed to dmxON FabKit.
- Всё на русском и английском. / Everything in Russian and English.

**Проверено в Fusion / Verified in Fusion**

- Стеки 4 и 8 слоёв, построенные Fusion по правилам, совпадают со стеками JLCPCB до микрона; возврат правил даёт файл, идентичный резервной копии.
  The 4 and 8-layer stacks Fusion builds from the rules match the JLCPCB stack-ups to the micron; restoring yields a file identical to the backup.
