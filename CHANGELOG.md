# История версий / Changelog

Версия меняется при каждой переделке: `JR_VERSION` и `JR_DATE` в `lib/jr_core.ulp`, файл `VERSION`, пакет `rules/` (пересобрать `-export`) и запись здесь.
The version is bumped on every change: `JR_VERSION` and `JR_DATE` in `lib/jr_core.ulp`, the `VERSION` file, the `rules/` pack (rebuild with `-export`) and an entry here.

Нумерация / Numbering: `MAJOR.MINOR.PATCH` — новая возможность → MINOR, исправление → PATCH.
New feature → MINOR, fix → PATCH.

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
