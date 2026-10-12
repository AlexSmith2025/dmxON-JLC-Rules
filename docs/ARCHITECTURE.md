# Как устроено / How it works

## Шаги / Steps

| Шаг / Step | Где / Where | Что происходит / What happens |
|---|---|---|
| 0 | `dmxON_JLC_Setup.ulp` | `DRC SAVE` текущих правил в `%LOCALAPPDATA%\dmxon_jlc\rules_backup` — это и резервная копия, и источник стека (`layerSetup`); затем `RUN … -stage2` с прежними аргументами / backup and stack source, then `RUN … -stage2` |
| 1 | `-stage2` | разбор платы (`js_scan`), стек из копии, диалог с предпросмотром, предварительная проверка, файл правил под плату, установка пакета, состояние для итога / board scan, stack from the backup, dialog with preview, pre-flight check, board rule file, pack install, state for the summary |
| 2 | команды Fusion / Fusion commands | `DRC LOAD`, `CLASS …`, `RATSNEST`, `DRC`, `RUN … -summary` |
| 3 | `-summary` | ошибки DRC по видам (`UL_ERROR`: описание, тип, состояние), замечания, предупреждения профиля / DRC errors by type, findings, profile notes |

Возврат прежних правил — отдельный запуск: шаг 0 → кнопка в диалоге → `DRC LOAD копия`, прежние `CLASS`, `RATSNEST`, `DRC`.
Restoring is a separate run: step 0 → the dialog button → `DRC LOAD backup`, previous `CLASS`, `RATSNEST`, `DRC`.

`-export <папка>` — без платы: пишет 12 `.dru` и 4 `.cam` для 1.6 мм / 1 oz / 0.5 oz.
`-export <folder>` — no board: writes 12 `.dru` and 4 `.cam` for 1.6 mm / 1 oz / 0.5 oz.

## Модули / Modules (`lib/`)

| Файл / File | Назначение / Purpose |
|---|---|
| `jr_core.ulp` | версия, двуязычные строки, HTML-сущности, файлы, команды без окон (`wscript`), состояние между шагами / version, bilingual strings, HTML entities, files, windowless commands, cross-step state |
| `jr_rules.ulp` | входные параметры, расчёт значений профиля (`jr_calc`), выбор стека, текст `.dru`, задание CAM, пакет / inputs, profile values, stack choice, `.dru` text, CAM job, pack |
| `jr_stack.ulp` | таблица 77 стеков JLCPCB: слои, толщина, медь, диэлектрики сверху вниз (P/C, толщина, ткань, Er) / the 77 JLCPCB stack-ups |

## Правила в `.dru` / Rules in `.dru`

- `layerSetup` — слои меди сверху вниз; между ними `+` (препрег) или `*` (ядро), всё в скобках — сквозные переходные.
  Copper layers top to bottom; `+` (prepreg) or `*` (core) between them; the outer brackets mean through vias.
- `mtCopper` — толщина меди слоёв 1…16; `mtIsolate[i]` — толщина диэлектрика под слоем `i+1`.
  Copper thickness of layers 1…16; `mtIsolate[i]` is the dielectric under layer `i+1`.
- `mdWireWire`, `mdWirePad`, `mdWireVia`, `mdPadPad`, `mdPadVia`, `mdViaVia` — зазоры разных цепей; `mdSmdPad`, `mdSmdVia`, `mdSmdSmd` — зазоры **одной** цепи (не больше зазоров разных, иначе Fusion задаёт вопрос при загрузке).
  Different-signal clearances; `mdSmdPad`, `mdSmdVia`, `mdSmdSmd` are **same-signal** clearances (not larger than the different-signal ones, or Fusion asks a question when loading).
- Поясок: `rv…` — доля сверла, `rlMin…`/`rlMax…` — пределы; внутренний поясок поднят так, чтобы от отверстия до чужой меди было 0.20 (переходное) и 0.30 мм (вывод).
  Ring: `rv…` is the share of the drill, `rlMin…`/`rlMax…` the limits; the inner ring is raised to keep 0.20 (via) and 0.30 mm (pin) from the hole to foreign copper.
- `mlViaStopLimit` — переходные со сверлом до этого значения закрыты маской.
  Vias drilled up to this value are covered by mask.

## Особенности Fusion / Fusion specifics

- `UL_LAYER.used` во Fusion значит «на слое есть объекты», а не «слой в стеке» — стек берётся из `DRC SAVE`.
  In Fusion `UL_LAYER.used` means «the layer has objects», not «the layer is in the stack» — the stack comes from `DRC SAVE`.
- Если в одной цепочке команд после `DRC` снова выполнить `DRC LOAD`, Fusion падает: очередь обновления панели ошибок ссылается на уже удалённые ошибки. Поэтому правила меняются только в начале цепочки, а возврат — отдельным запуском.
  A `DRC LOAD` after `DRC` in the same command chain crashes Fusion: the error panel's queued update points at deleted errors. So rules change only at the start of a chain, and restoring is a separate run.
- После смены правил Fusion держит полигоны неразлитыми — `RATSNEST` перед `DRC` обязателен, иначе DRC видит сотни «неразведённых» связей.
  After a rule change Fusion leaves polygons unpoured — `RATSNEST` before `DRC` is required, otherwise DRC sees hundreds of «unrouted» connections.
- `DRC` с новыми правилами удаляет одобрения ошибок, которые перестали совпадать.
  `DRC` with new rules deletes approvals of messages that no longer match.
- `path_dru[]` и `path_cam[]` во Fusion указывают внутрь папки программы (`webdeploy`) — туда не пишем.
  In Fusion `path_dru[]` and `path_cam[]` point inside the program folder (`webdeploy`) — never written to.
- Цикл `polygons()` во Fusion устарел и останавливает ULP: у цепей — `polyPours()`, у платы и корпусов — `polyShapes()`; у корпуса нет `smds()` — `contacts()` и `C.smd`.
  The `polygons()` loop is deprecated in Fusion and stops the ULP: signals use `polyPours()`, boards and footprints `polyShapes()`; footprints have no `smds()` — use `contacts()` and `C.smd`.
- Имя переменной цикла (`B.signals(S)`) живёт до конца блока: у каждого цикла своё имя.
  A loop variable name (`B.signals(S)`) lives until the end of the block: every loop has its own name.
- `output()` пишет в однобайтовой кодировке Windows: русский текст в `.dru` — числовыми ссылками HTML, в `.cam` — `\uXXXX`.
  `output()` writes in the Windows ANSI code page: Russian text in `.dru` goes out as numeric HTML references, in `.cam` as `\uXXXX`.
- Служебные команды (`mkdir`, `del`) идут через `dmxon_jlc_run.vbs` (`wscript`, без окна) — иначе в Windows 11 каждый вызов открывает окно Терминала.
  Helper commands (`mkdir`, `del`) go through `dmxon_jlc_run.vbs` (`wscript`, windowless) — otherwise every call opens a Terminal window on Windows 11.
