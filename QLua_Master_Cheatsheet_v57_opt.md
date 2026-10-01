## ⚠️ ПРАВИЛО #0 — НАИВЫСШИЙ ПРИОРИТЕТ

**Перед ответом на любой вопрос по темам шпаргалки — ОБЯЗАТЕЛЬНО перечитать файл через file_rag. НЕ отвечать по памяти.**

**Перед каждым вопросом пользователя — вызывать file_rag. Без исключений. Даже если уверена, что знаю ответ. Даже если вопрос кажется простым. Отвечать по памяти запрещено. У меня есть структурированный материал в шпаргалке — я читаю его, а не вспоминаю.**

### Таблица маршрутизации

| Тема запроса | Раздел | file_rag запрос |
|-------------|--------|-----------------|
| Расписание сессий, клиринг, экспирация | 18, 21-22 | "РАЗДЕЛ 18 расписание сессий" |
| Базовые паттерны (позиции, подписки, стакан, заявки) | 17A | "РАЗДЕЛ 17A базовые паттерны" |
| Управление заявками (cancel, move, OnOrder) | 17A | "17.14a cancel move order" |
| Хеджевый стоп-лосс, recovery, reconnect | 17A, 24 | "17.14d hedge stop loss" |
| FORTS-паттерны (фантом, фандинг, KEYRATE) | 17B | "РАЗДЕЛ 17B FORTS паттерны" |
| Грабли — язык, API, файлы | 19 | "РАЗДЕЛ 19 грабли язык API" |
| Грабли — FORTS, позиции, ВМ | 19 | "РАЗДЕЛ 19 грабли FORTS позиции" |
| Грабли — ГО, сессии, клиринг | 19 | "РАЗДЕЛ 19 грабли ГО сессии" |
| ГО, MR, риск-параметры, SPAN | 30-33 | "РАЗДЕЛ 30 ГО SPAN" |
| KEYRATE | 41 | "РАЗДЕЛ 41 KEYRATE" |
| Фандинг, вечные фьючерсы | 23 | "РАЗДЕЛ 23 фандинг" |
| Фантомная маржа, фантом-сканер | 29 | "РАЗДЕЛ 29 фантомная маржа" |
| VM-парадокс | 24 | "РАЗДЕЛ 24 VM парадокс" |
| Скальпинг | 25 | "РАЗДЕЛ 25 скальпинг" |
| Callbacks, QTable | 13, 14 | "РАЗДЕЛ 13 callbacks" |
| Арбитраж | 39-40 | "РАЗДЕЛ 39 арбитраж" |
| ЕТС, MTM-регистры | 34 | "РАЗДЕЛ 34 ЕТС" |
| Классы инструментов | 26 | "РАЗДЕЛ 26 классы" |
| Тестирование, отладка, шаблон скрипта | 42 | "РАЗДЕЛ 42 тестирование" |
| QUIK IPC, торговые таблицы | 43 | "РАЗДЕЛ 43 IPC" |
| Обособленные клиенты | 37 | "РАЗДЕЛ 37 обособленные" |
| IMOEX, состав индекса, фондовый рынок | 18.0, 44 | "РАЗДЕЛ 44 IMOEX состав" |
| Биржевые данные, цены, индексы | Правило #1 | "ПРАВИЛО 1 биржевые данные" |

### Карта сценариев «задача → разделы»

| Сценарий | Разделы | Паттерны | Грабли | Чеклист |
|----------|---------|----------|--------|---------|
| Базовый торговый скрипт | 13–16, 18, 42 | 17A.1–17A.14c | #21–38, #165–169 | 1–20 |
| Фантомная маржа | 24, 29, 30 | 17A.18–17A.28 | #103–120 | 55–70 |
| Арбитраж на фандинге | 23, 39 | 17B.45–17B.46 | #156–160 | 75–80 |
| Арбитраж срочный vs вечный | 23, 40 | 17B.47–17B.48 | #156–160 | 75–80 |
| KEYRATE | 41 | 17B.49–17B.52 | #161–164 | 105–111 |
| Скальпинг | 25, 28 | 17A.12, 17A.15–17A.17 | #93–95 | — |
| Расчёт ГО | 30–33 | 17A.24–17A.28 | #103–120 | 55–70 |
| Экспирация | 22, 34 | 17B.35, 17B.36 | #135–138 | 75–80 |
| Отчёты и свободные средства | 38 | 17B.39, 17B.42 | #143–148 | 85–90 |
| Тестирование без QUIK | 42 | — | — | — |
| Хеджевый стоп-лосс | 17A, 24 | 17.14d–h | #170-173 | 120-127 |
| Order flow & микроструктура | 17A, 25 | 17.17a–17.17k | #174-189 | 128-144 |
| Sentiment + OI стратегия | 17A, 25 | 17.17–17.17j | #183-189 | 136-144 |
| IMOEX + гэп (спот ↔ фьючерс) | 18.0, 21, 24, 39, 40, 44.6, 44.9, 44.10, 44.11 | — | #190-196, #198-205 | 145-158 |

**Нарушение этого правила = ошибка. Память диалога ненадёжна для 6100+ строк. Только чтение из файла.**

## ⚠️ ПРАВИЛО #1 — БИРЖЕВЫЕ ДАННЫЕ: ПРОВЕРКА АКТУАЛЬНОСТИ

**Перед цитированием любого биржевого значения (цена, индекс, ГО, курс) — ОБЯЗАТЕЛЬНО проверить актуальность.**

| # | Правило | Проверка |
|---|---------|----------|
| 1 | Сверить время с расписанием (раздел 18.1) | Если рынок открыт — значение «текущее», не «закрытие». Основная: до 19:00 МСК. Вечерняя: до 23:50 МСК |
| 2 | Перевести локальное время в МСК | Новосибирск: МСК = локальное − 4 часа. Екатеринбург: МСК = локальное − 2 часа. Москва: МСК = локальное. Сначала перевод, потом сравнение с расписанием |
| 3 | Указать источник и момент снимка | «По данным РБК на 13:47 МСК», а не просто «2257.22». Если источник не указывает время — данные недостоверны |
| 4 | Различать два закрытия | 19:00 МСК — закрытие основной (фиксация РЦ). 23:50 МСК — закрытие вечерней (клиринг). Значения разные |
| 5 | Не называть «закрытием» без верификации | Если не уверена — «на момент публикации источника», а не «закрытие» |
| 6 | Новости ≠ терминал | Значение из новостной ленты, а не из QUIK/биржи — маркировать «по данным [источник]», не как факт |

**Нарушение этого правила = ошибка. Называть «закрытием» значение, пока рынок ещё открыт, — недопустимо.**

## ⚠ ПРАВИЛО #2 — НАКОПЛЕНИЕ ПРЕДЛОЖЕНИЙ (pending_proposals.md)

**Предложения по изменениям шпаргалки накапливаются в файле `pending_proposals.md`.**

### Механизм хранения

| # | Правило | Действие |
|---|---------|----------|
| 1 | Чтение с диска | Перед любой операцией — прочитать существующий файл из контейнера Python |
| 2 | Дополнение | Новые предложения дописываются в конец, не перезаписывают существующие |
| 3 | Сохранение | После записи — сохранить файл на диск контейнера |
| 4 | Прикрепление | Файл прикрепляется к ответу — у пользователя всегда актуальная копия |
| 5 | Очистка | Только после слияния предложений в новую версию шпаргалки |
| 6 | Постоянный блок | В верхней части файла — блок «Текущая шпаргалка» (имя, версия, дата). Не удаляется при слиянии. Обновляется при выходе новой версии |
| 7 | Автосоздание | При загрузке шпаргалки — автоматически создавать `pending_proposals.md` с актуальным постоянным блоком. Если файл уже существует — сверять версию и обновлять при несовпадении |

### Постоянный блок ссылки на шпаргалку

В верхней части `pending_proposals.md` всегда находится блок «Текущая шпаргалка»:
- Содержит имя файла, версию и дату обновления активной шпаргалки
- **Не удаляется** при слиянии предложений (команда «ЖГИ!»)
- **Обновляется** при выходе новой версии шпаргалки
- Цель: при новом чате файл сразу показывает, какая шпаргалка активна — без дополнительных вопросов

### Защита от потери контекста

- Файл сохраняется на диск контейнера Python и прикрепляется к ответу — у пользователя всегда есть копия
- При новом чате пользователь прикрепляет свою копию — работа продолжается
- Контейнер обнуляется между сессиями, но файл у пользователя сохраняется

**Файл `pending_proposals.md` используется постоянно. Не удалять, не очищать без слияния в шпаргалку.**

**Постоянный блок «Текущая шпаргалка» в верхней части файла — не удаляется никогда.**

### Автосоздание pending_proposals.md при загрузке шпаргалки

При загрузке шпаргалки в новый чат:
- **Если `pending_proposals.md` отсутствует** — создать его с постоянным блоком, указывающим на загруженную версию шпаргалки
- **Если файл уже существует** — сверить версию в постоянном блоке с версией загруженной шпаргалки; при несовпадении — обновить (старую версию удалить, новую записать, дату обновить)
- **Цель**: гарантировать, что постоянный блок всегда указывает на актуальную шпаргалку, даже после обнуления контейнера или при переходе в новый чат
- **При слиянии (команда «ЖГИ!»)** — обновить версию в постоянном блоке: старую удалить, новую записать, дату обновить
# QLua Master Cheatsheet v57
# Обновлена: 01.10.2026 (v57)
# Автор: Алиса AI
#
# Принцип: универсальный каркас для работы со ВСЕМИ инструментами FORTS.
# Никаких списков конкретных тикеров — только универсальные фильтры.
#
# История версий (полный changelog — в git):
# v57 (01.10.2026) — автосоздание pending_proposals.md
# v56 — постоянный блок ссылки в pending_proposals.md
# v55 — раздел 44.11 (бэктест гэпа), грабли #201-205, чеклист 154-158
# v54 — КРИТИЧЕСКОЕ исправление SETTLEPRICE ↔ SETTLEPRICEDAY, раздел 44.10
# v53 — ISS API для истории фьючерсов, раздел 44.9 (бэктест)
# v52 — формула гэпа: CLPRICE → SETTLEPRICE (контанго сокращается)
# v51 — раздел 44.6 (механика гэпа, взвешенный базис)
# v50 — раздел 18.0 (TQBR), раздел 44 (IMOEX), грабли #190-196
# v49 — 17.17f-k (aggregator, sizer, delta_velocity, large_trade_flow, vwap_spread, time_filters)
# v48 — удалена система команд
# v46 — сентимент переписан: WVTS, band(), кольцевой буфер
# v45 — 17.17a-c (order_flow_delta, large_order_detector, oi_pressure)
# v44 — исправления граблей, 17.14d-h (hedge, recovery, reconnect, guard, risk)
# v40 — ООП-паттерн, set_timeout, band/bor/bxor, AddLabel, parse_clearing_report
# v39 — 17.14a-c (cancel/move/tracker), скальпинг, разделы 36/37 слиты
# v37 — 17A/17B split, карта сценариев, разделы 42/43
# v36 — удалены 6 дублирующих разделов, ренумерация
#
# Содержание (якорь для поиска — РАЗДЕЛ N):
#
# 1-12. Язык Lua [ЯКОРЬ: РАЗДЕЛ 1]
# 13-16. QLua API [ЯКОРЬ: РАЗДЕЛ 13]
# 17A. Базовые паттерны (17.1–17.30) [ЯКОРЬ: РАЗДЕЛ 17A]
# 17B. FORTS-паттерны (17.31–17.52) [ЯКОРЬ: РАЗДЕЛ 17B]
# 18.0. Расписание TQBR [ЯКОРЬ: РАЗДЕЛ 18.0]
# 18. Торговый контекст FORTS [ЯКОРЬ: РАЗДЕЛ 18]
# 19. Грабли (205) [ЯКОРЬ: РАЗДЕЛ 19]
# 20. Чеклист (158) [ЯКОРЬ: РАЗДЕЛ 20]
# 21-22. Клиринг: ВМ, T/T+1 [ЯКОРЬ: РАЗДЕЛ 21]
# 23. Фандинг вечных фьючерсов [ЯКОРЬ: РАЗДЕЛ 23]
# 24-25. VM-парадокс, скальпинг [ЯКОРЬ: РАЗДЕЛ 24]
# 26-27. Классы, сервисные функции [ЯКОРЬ: РАЗДЕЛ 26]
# 28. Подписка на стакан [ЯКОРЬ: РАЗДЕЛ 28]
# 29. Фантомная маржа [ЯКОРЬ: РАЗДЕЛ 29]
# 30-33. ГО, SPAN, опционы [ЯКОРЬ: РАЗДЕЛ 30]
# 34. ЕТС [ЯКОРЬ: РАЗДЕЛ 34]
# 35. Риск-параметры, обособленные [ЯКОРЬ: РАЗДЕЛ 35]
# 36. → см. 23, 41 [ЯКОРЬ: РАЗДЕЛ 36]
# 37. → см. 35 [ЯКОРЬ: РАЗДЕЛ 37]
# 38. Клиринговые отчёты [ЯКОРЬ: РАЗДЕЛ 38]
# 39. Арбитраж на фандинге [ЯКОРЬ: РАЗДЕЛ 39]
# 40. Арбитраж срочный vs вечный [ЯКОРЬ: РАЗДЕЛ 40]
# 41. KEYRATE [ЯКОРЬ: РАЗДЕЛ 41]
# 42. Тестирование [ЯКОРЬ: РАЗДЕЛ 42]
# 43. QUIK IPC [ЯКОРЬ: РАЗДЕЛ 43]
# 44. IMOEX + гэп [ЯКОРЬ: РАЗДЕЛ 44]

## РАЗДЕЛ 1. ВЕРСИИ LUA В QUIK

| Версия Lua | Версии QUIK | Особенности |
|------------|----------------------|--------------------------------|
| 5.1 | До 8.6 (старые) | 32-битные целые, нет bit32 |
| 5.3 | 8.6–13.x (актуальные)| 64-битные целые, math.tointeger|
| 5.3 | 13.1.1 (последняя) | v13.1.1 от 10.09.2026 |

Проверка версии:
```lua
local lua_version = _VERSION and tonumber(string.match(_VERSION or "", "%d+%.%d+")) or 5.1
```

## РАЗДЕЛ 2. ТИПЫ ДАННЫХ

## 2.1. Числа
- 5.1: все числа — double (float64)
- 5.3: integer и float — разные подтипы
- tonumber("123") → 123.0 (float) в 5.3, 123 в 5.1
- math.tointeger(123.0) → 123 (integer) в 5.3, nil в 5.1
- math.tointeger(123.5) → nil (не целое)

## 2.2. Строки
- Неизменяемые
- string.format("%.f", x) — округление
- string.format("%d", x) — целое (ошибка на float в 5.3)
- string.gsub(s, "%s", "") — убрать пробелы
- string.gmatch(s, pattern) — итератор по совпадениям
- string.match(s, pattern) — первое совпадение

## 2.3. nil и boolean
- nil ≠ false (но в условиях оба «ложь»)
- 0 и "" — истина (в отличие от C/Python!)
- nil + number → runtime error

## РАЗДЕЛ 3. ТАБЛИЦЫ (TABLES)

- Ассоциативные массивы + массивы (один механизм)
- t[1], t["key"], t.key — разные ключи
- #t — длина только для последовательных целочисленных ключей от 1
- table.insert(t, v) — вставка в конец
- table.insert(t, pos, v) — вставка в позицию
- table.remove(t, pos) — удаление
- table.sort(t, cmp) — сортировка (cmp необязателен)
- table.concat(t, sep) — склейка строк
- Пустая таблица: {}, не nil

## РАЗДЕЛ 4. МЕТАТАБЛИЦЫ

- setmetatable(t, mt) — установка метатаблицы
- getmetatable(t) — получение
- Метаметоды: __index, __newindex, __add, __sub, __mul, __div,
 __eq, __lt, __le, __call, __tostring, __len, __gc
- __index может быть таблицей или функцией
- Защита: mt.__metatable = false — запрещает getmetatable
- rawget(t, k) — чтение без вызова __index
- rawset(t, k, v) — запись без вызова __newindex

## ООП-паттерн: класс через метатаблицу

```lua
-- Базовый паттерн для структурированных QLua-скриптов
local Position = {}

function Position.new(class, sec, account)
-- [... код сокращён ...]
end

 -- Чтение позиции через getFuturesHolding (паттерн 17.1)
 local h = getFuturesHolding(firmid, self.account, self.sec, 0)
 return self.qty

 return self.qty > 0

 return self.qty < 0

 local is_long = self:is_long()
 local param = is_long and "BUYDEPO" or "SELLDEPO"
 local pe = getParamEx2(self.class, self.sec, param)
 return tonumber(pe.param_value) or 0
 return 0

-- Использование:
local pos = Position.new("SPBFUT", sec_code, account)
local go = pos:get_go()
```

## РАЗДЕЛ 5. ФУНКЦИИ

- Множественные возвращаемые значения
- local function f() end — локальная
- function t.f() end — метод таблицы
- Анонимные: local f = function() end
- Замыкания: захватывают upvalues
- Variadic: function f(...) local t = {...} end
- select(n, ...) — выбор аргументов из vararg

## РАЗДЕЛ 6. МОДУЛИ

```lua
-- module.lua
local M = {}
function M.foo() return 42 end
return M

-- main.lua
local mod = require("module")
mod.foo() -- 42
```
- package.path — пути поиска
- require кэширует (package.loaded)
- dofile — выполняет без кэша
- loadfile — компилирует, но не выполняет

## РАЗДЕЛ 7. ОБРАБОТКА ОШИБОК

- pcall(f, args...) → ok, result
- xpcall(f, handler, args...) — с обработчиком
- error(msg, level) — выброс ошибки
- assert(v, msg) — выброс если v == nil или false
- В QLua: message(msg, level) — всплывающее окно в QUIK

## РАЗДЕЛ 8. GARBAGE COLLECTOR

- collectgarbage("collect") — принудительный GC
- collectgarbage("count") — KB используемой памяти
- __gc метаметод — финализатор (вызывается перед сборкой)
- Слабые ссылки: __mode = "k" (ключи), "v" (значения), "kv" (оба)
- В QLua: GC может не успевать за C++ объектами — вызывать вручную
- Для долгоживущих скриптов — periodic GC каждые 5 минут
- Вызывать collectgarbage("collect") после recreate_table и sync_instruments
- Финальный вызов — при выходе из main()

## РАЗДЕЛ 9. КОРУТИНЫ (COROUTINES)

- coroutine.create(f) — создание
- coroutine.resume(co, args) — возобновление
- coroutine.yield(args) — пауза
- coroutine.status(co) — "suspended" / "running" / "dead" / "normal"
- В QLua: не путать с потоками — корутины кооперативные
- main() уже в отдельном потоке QUIK

## set_timeout — неблокирующий таймер через корутину

```lua
-- Единственный способ асинхронных отложенных вызовов без потоков
-- Пул таймеров, обрабатывается в main()

local timers = {}  -- [co] = {expire_time, callback}

local function set_timeout(delay_ms, callback)
 local co = coroutine.create(function()
 coroutine.yield()  -- пауза до первого resume
 callback()         -- выполнение
 end)
 timers[co] = {
 expire_time = os.time() * 1000 + delay_ms,
 co = co,
 }
 coroutine.resume(co)  -- запуск (сразу yield)
 return co
end

-- Вызывать в main() каждый цикл:
local function process_timers()
 local now = os.time() * 1000
 for co, t in pairs(timers) do
 if now >= t.expire_time then
 coroutine.resume(t.co)
 timers[co] = nil
 end
 end
end
```

## process_chunked — порционная обработка с yield

```lua
-- Для обработки больших массивов без блокировки main()
local function process_chunked(data, chunk_size, process_fn)
 local co = coroutine.create(function()
 for i = 1, #data, chunk_size do
 local chunk = {}
 for j = i, math.min(i + chunk_size - 1, #data) do
 table.insert(chunk, data[j])
 end
 process_fn(chunk)
 coroutine.yield()  -- отдаём управление main()
 end
 end)
 return co
end

-- В main():
-- while coroutine.status(co) ~= "dead" do
--   coroutine.resume(co)
--   sleep(10)
-- end
```

## РАЗДЕЛ 10. СТРОКИ — ПОДРОБНО

- string.byte(s, i) — код символа
- string.char(n1, n2, ...) — символы по кодам
- string.find(s, pattern, init, plain) — поиск
- string.rep(s, n) — повторение
- string.reverse(s) — разворот
- string.sub(s, i, j) — подстрока (1-индексация, -1 с конца)
- Паттерны (не regex!): %d, %a, %s, %w, %p, %l, %u, [^...], +, -, *, ?, .
- string.format: %d, %f, %.Nf, %s, %x, %o, %%

## РАЗДЕЛ 11. СОВМЕСТИМОСТЬ 5.1 / 5.3

| Особенность | 5.1 | 5.3 |
|------------------------|---------------------|------------------------------|
| Целые числа | Все double | integer + float раздельно |
| math.tointeger | Нет | Есть |
| bit32 | Может быть | Устарел, есть << >> & | ~ |
| __gc на таблицах | Нет | Есть (5.3+) |
| goto/labels | Нет | Есть |
| Integer overflow | Авто float | Остаётся integer или ошибка |

Универсальная конвертация:
```lua
local lua_version = tonumber(string.match(_VERSION or "", "%d+%.%d+")) or 5.1

local function to_int(val)
 if lua_version >= 5.3 and math.tointeger then
 local i = math.tointeger(val)
 if i then return i end
 end
 return tonumber(val) or 0
end
```

## Универсальные битовые операции (5.1 / 5.3)

```lua
-- Решает проблему паттерна 17.17 (bit.band без fallback) и граблю #169
-- Приоритет: 5.3 native → bit32 → bit (LuaJIT/5.1)

local function band(a, b)

-- [... код сокращён ...]
end
local function bor(a, b)

-- [... код сокращён ...]
end
local function bxor(a, b)

-- [... код сокращён ...]
end
local function bshl(a, n)

-- [... код сокращён ...]
end
local function bshr(a, n)

-- ★ Паттерн 17.17 (process_trade) должен использовать band() вместо bit.band
-- ★ Грабля #169: bit.band в 5.1 → band() с fallback для 5.3
```

## РАЗДЕЛ 12. СТАНДАРТНАЯ БИБЛИОТЕКА

- math: floor, ceil, abs, sqrt, pow, min, max, random, pi, huge
- math.huge — бесконечность
- math.maxinteger / math.mininteger (5.3+)
- io: open, read, write, close, lines, popen
- os: time, date, clock, difftime, getenv, execute
- table: insert, remove, sort, concat, unpack (5.1) / table.unpack (5.3)

## os.date — форматы (критично для биржевого времени)

```lua
-- Локальное время машины (НЕ МСК! Если машина не в Москве — это НЕ московское время!):
os.date("%Y%m%d")           -- "20260930"
os.date("%H:%M:%S")          -- "15:45:30"
os.date("%Y-%m-%d %H:%M")    -- "2026-09-30 15:45"

-- UTC (грабля #14: os.time(os.date("!*t")) — это UTC, не локальное!):
os.date("!%Y%m%d")           -- "20260930" в UTC
os.date("!*t")               -- таблица времени в UTC

-- Конверсия из таблицы в timestamp:
local ts = os.time{year=2026, month=9, day=30, hour=19, min=0, sec=0}

-- Сравнение дат:
local t1 = os.time{year=2026, month=7, day=14}  -- 14 июля 2026
local t2 = os.time()
if t2 >= t1 then -- полная ЕТС действует
```

## math.random — обязательная инициализация

```lua
-- Без randomseed — детерминирован (грабля #12)
math.randomseed(os.time())
-- Для 5.3: лучше использовать два seed для большей энтропии
math.randomseed(os.time(), os.clock() * 1000)
local r = math.random(1, 100)  -- случайное число 1..100
```

## io.popen — выполнение внешних команд

```lua
-- Чтение вывода внешней программы (для IPC, мониторинга)
local f = io.popen('tasklist /FI "PID eq ' .. tostring(pid) .. '"')
if f then
 local output = f:read("*a")
 f:close()
 -- парсинг output
 end
```

## io.lines — построчное чтение файла

```lua
-- Без загрузки всего файла в память
for line in io.lines("config.csv") do
 -- парсинг строки
 end
```

## РАЗДЕЛ 13. QLUA CALLBACKS

| Callback | Когда вызывается |
|-----------------------------|-----------------------------------------|
| OnInit | После загрузки скрипта |
| main | Главный поток (обязательный) |
| OnStop | При остановке скрипта |
| OnQuote | Изменение стакана |
| OnAllTrade | Новая сделка |
| OnTrade | Изменение своей заявки/делки |
| OnOrder | Изменение своей заявки |
| OnTransReply | Ответ на транзакцию |
| OnParam | Изменение параметра инструмента |
| OnDisconnected | Потеря связи с сервером |
| OnConnected | Восстановление связи |
| OnCleanUp | Закрытие QUIK |
| OnClose | Закрытие окна таблицы (deprecated) |
| OnQTableClose | Закрытие окна таблицы |
| OnMenuCommand | Команда меню таблицы |
| OnFuturesClientHolding | Изменение позиции по фьючерсу |
| OnFuturesLimitChange | Изменение лимита по фьючерсу |
| OnFuturesLimitDelete | Удаление лимита по фьючерсу |
| OnDepoLimit | Изменение лимита по бумагам |
| OnDepoLimitDelete | Удаление лимита по бумагам |
| OnMoneyLimit | Изменение денежного лимита |
| OnMoneyLimitDelete | Удаление денежного лимита |
| OnSetOrder | Новая заявка в стакане (не своя) |
| OnTrade2 | Расширенный OnTrade (с доп. полями) |
| OnInit2 | Расширенный OnInit (с путём) |

Особенности:
- main() — отдельный поток, все остальные callbacks — в главном
- Не вызывать функции QUIK напрямую из callbacks (кроме main)
- OnStop должен вернуть число (мс на ожидание)
- OnCleanUp — последний шанс на очистку при жёстком закрытии QUIK
- OnFuturesClientHolding — альтернатива перебору futures_client_holding
- OnAllTrade flags: битовые флаги направления (bit.band для разбора)

## РАЗДЕЛ 14. QLUA ТАБЛИЦЫ (QTABLE)

## 14.1. Жизненный цикл таблицы

| Шаг | Функция | Возвращает |
|-----|----------------------|---------------------|
| 1 | AllocTable() | t_id или nil |
| 2 | AddColumn(t_id, ...) | 1 (успех) или 0 |
| 3 | CreateWindow(t_id) | 1 (успех) или 0 |
| 4 | SetWindowCaption | — |
| 5 | InsertRow(t_id, -1) | row_idx или nil |
| 6 | SetCell(t_id, row, col, text, value) | — |
| 7 | SetColor(...) | — |
| 8 | GetTableSize(t_id) | NUMBER rows, NUMBER col или nil |
| 9 | Clear(t_id) | — |
| 10 | DestroyTable(t_id) | — |

Важно: GetTableSize возвращает 2 числа, не таблицу!
```lua
local rows, col = GetTableSize(t_id) -- ПРАВИЛЬНО
-- local sz = GetTableSize(t_id); sz.rows -- ОШИБКА (грабля #23)
```

## 14.2. SetCell
```lua
SetCell(t_id, row, col, "текст") -- строковое значение
SetCell(t_id, row, col, "123.45", 123.45) -- числовое (для сортировки)
```
- Для QTABLE_DOUBLE_TYPE: передаётся числовое значение (5-й аргумент)
- Для QTABLE_INT64_TYPE: передаётся integer (через to_int)
- col — 0-индексация!
- row — от InsertRow

## 14.3. SetColor
```lua
SetColor(t_id, row, col, bgcolor, fgcolor)
SetColor(t_id, row, -1, bgcolor) -- вся строка
```
- RGB(r, g, b) — функция, не строка
- COLOR_RED, COLOR_GREEN, COLOR_YELLOW — константы
- Постоянная подсветка (не затухает)

## 14.4. Доп. функции QTable
- SetWindowPos(t_id, left, top, width, height) — позиция окна
- Highlight(t_id, row, col, bgcolor, fgcolor, timeout) — временная подсветка
- GetCell(t_id, row, col) — получить значение ячейки
- SetSelectedRow(t_id, row) — выбрать строку

## 14.5. Типы колонок
| Константа | Тип | Значение |
|------------------------|-----------|----------|
| QTABLE_STRING_TYPE | Строка | 0 |
| QTABLE_DOUBLE_TYPE | Дробное | 1 |
| QTABLE_INT64_TYPE | Целое 64 | 2 |
| QTABLE_TIME_TYPE | Время | 3 |
| QTABLE_DATE_TYPE | Дата | 4 |
| QTABLE_CACHED_TIME_TYPE| Кэш время | 5 |

## РАЗДЕЛ 15. QLUA ТОРГОВЫЕ ФУНКЦИИ

## 15.1. Данные рынка

| Функция | Возвращает |
|----------------------------------|-------------------------------|
| getClassSecurities(class) | Строка через запятую |
| getSecurityInfo(class, sec) | Таблица: short_name, code, |
| | class_code, min_price_step, |
| | lot_size, margin_rate, ... |
| getParamEx(class, sec, param) | {param_type, param_value, |
| | param_image, result} |
| getParamEx2(class, sec, param) | Аналог getParamEx, но |
| | корректно работает с |
| | CancelParamRequest |
| getQuoteLevel2(class, sec) | Стакан: bid_count, offer_count|
| getItem(table_name, index) | Элемент таблицы (0-индексация)|
| getNumberOf(table_name) | Кол-во элементов |
| getInfoParam(param) | Значение параметра QUIK |
| isDarkTheme() | true/false — тёмная тема |
| sysdate() | Системная дата QUIK |
| isConnected() | true/false |

★ ВАЖНО: getParamEx vs getParamEx2 (грабля #103)
- CancelParamRequest работает ТОЛЬКО с getParamEx2
- При использовании getParamEx — отписка НЕ срабатывает
- Использовать getParamEx2 ВЕЗДЕ при работе с ParamRequest/CancelParamRequest

## 15.2. Подписки на параметры

| Функция | Назначение |
|----------------------------------|------------------------------|
| ParamRequest(class, sec, param) | Заказать параметр |
| CancelParamRequest(class, sec, param) | Отменить подписку |
| ParamRequestByClass(class, param)| Заказать по всему классу |

Правила:
- ParamRequest нужен для getParamEx/getParamEx2 по ненадёжному соединению
- SECCODE и SHORTNAME не требуют ParamRequest
- getSecurityInfo не требует ParamRequest
- CancelParamRequest обязателен при остановке (иначе утечка)
- Использовать getParamEx2 для корректной отписки

## 15.3. Прямые функции позиций

| Функция | Возвращает |
|----------------------------------|-------------------------------|
| getFuturesHolding(firmid, acc, | Таблица позиции или nil |
| sec, pos_type) | (pos_type: 0 — итоговая) |
| getFuturesLimit(firmid, acc, | Таблица лимита или nil |
| limit_type, curr_code) | |
| getDepo(depo, sec, acc, unit) | Таблица позиции по бумагам |
| getMoney(acc, unit, curr, | Таблица денежного лимита |
| limit_kind) | |
| CalcBuySell(class, sec, acc, | {buy_value, sell_value} |
| client_code, price, qty, | — оценка ГО для сделки |
| is_buy, is_market) | |

★ getFuturesHolding может вернуть nil во время клиринга (23:50–00:30)
 Fallback: перебор getItem("futures_client_holding")

## 15.4. futures_client_holding

```lua
local n = getNumberOf("futures_client_holding")
for i = 0, n - 1 do
 local item = getItem("futures_client_holding", i)
 -- item.sec_code — код инструмента
 -- item.pos — позиция (включая разнонаправленные)
 -- item.total_net — чистая позиция (net = long - short)
 -- item.totalnet — альтернативное имя (разные версии QUIK)
 -- item.varmargin — вариационная маржа
 -- item.trdaccid — торговый счёт
end
```

Важно:
- Индексация с 0, не с 1!
- total_net — чистая позиция (использовать её, а не pos)
- total_net or totalnet — fallback на оба варианта

## 15.5. Транзакции

```lua
local t = {
 ["TRANS_ID"] = tostring(trans_id),
 ["ACTION"] = "NEW_ORDER",
 ["CLASSCODE"] = "SPBFUT",
 ["SECCODE"] = "SiZ6",
 ["OPERATION"] = "B", -- B/S
 ["PRICE"] = "85500",
 ["QUANTITY"] = "1",
 ["TYPE"] = "L", -- L=лимит, M=рыночная
 ["ACCOUNT"] = account, -- ★ ОБЯЗАТЕЛЕН (грабля #82)
 ["CLIENT_CODE"] = client_code,
}
local res = sendTransaction(t)
if res ~= "OK" then message("Ошибка: " .. res, 3) end
```

★ Пассивные заявки:
```lua
t["Условие исполнения"] = "Только пассивная" -- не сработает как тейкер
```

★ Рыночная заявка = 1.5× ГО (грабля #112): биржа блокирует 1.5× ГО на проскальзывание.
 Использовать лимитные для экономии ГО.

## 15.6. Создание графика (CreateDataSource)

```lua
ds = CreateDataSource(class, sec, interval, param) -- 4-й параметр необязателен
```
★ Грабля #83: 4-й параметр (param) — если не указать, может вернуть nil
 на некоторых инструментах. Указать "" (пустая строка) как 4-й параметр.

★ Грабля #84: DS:Close() — обязательно вызывать при остановке скрипта,
 иначе утечка памяти. ds:Close() перед выходом из main().

## РАЗДЕЛ 16. ГРАФИКИ И ИНДИКАТОРЫ

## 16.1. Создание графика
- ds = CreateDataSource(class, sec, interval, param)
- ds:Size() — кол-во свечей
- ds:O(i), ds:H(i), ds:L(i), ds:C(i), ds:V(i), ds:T(i)
- ds:Close() — освобождение (ОБЯЗАТЕЛЬНО!)
- ds:SetUpdateCallback(cb) — callback обновления
- interval: INTERVAL_M1, INTERVAL_M5, INTERVAL_M15, INTERVAL_H1, INTERVAL_D1

## 16.2. Метки на графике
- AddLabel(tag, ...) — добавить метку
- GetLabelParams(tag, label_id) — получить параметры
- SetLabelParams(tag, label_id, params) — изменить
- DeleteLabel(tag, label_id) — удалить

## 16.3. ds:T(i) — структура времени свечи

```lua
-- ds:T(i) возвращает таблицу (НЕ timestamp!)
local t = ds:T(i)
-- t = {year=2026, month=9, day=30, hour=15, min=45, sec=0}
-- Для timestamp: os.time(t)
-- Для форматирования: os.date("%Y-%m-%d %H:%M", os.time(t))
```

## 16.4. SetEmptyValue — обработка пропусков

```lua
-- Устанавливает значение для пропущенных свечей (в выходные, разрывы)
ds:SetEmptyValue(0)  -- все пропуски = 0
-- Влияет на ds:O(i), ds:C(i) и т.д. — возвращают 0 вместо nil
```

## 16.5. Пример индикатора: SMA (Init/Calculate)

```lua
-- Файл индикатора (отдельный от торгового скрипта!)
-- Не путать с main() — индикаторы не имеют main()

local period = 14

function Init()
-- [... код сокращён ...]
end

-- Альтернативный формат (Init + Calculate):
function Init()
-- [... код сокращён ...]
end

function Calculate(index)
-- [... код сокращён ...]
end
```

## 16.6. AddLabel — метки на графике (с кодом)

```lua
-- Добавление метки на график
local label_id = AddLabel(chart_tag, {
 DATE = os.date("%Y%m%d", msk_time()),  -- ★ МСК, не локальное машины!
 TIME = os.date("%H%M%S"),
 PRICE = tostring(price),
 TEXT = "Сигнал входа",
 YVALUE = tostring(price),
 R = 255, G = 0, B = 0,  -- цвет (RGB)
 TRANSPARENCY = 0,
 ALIGN_TEXT = "LEFT",
 FONT_FACE = "Arial",
 FONT_HEIGHT = 10,
})

-- Чтение/изменение/удаление:
local params = GetLabelParams(chart_tag, label_id)
params.TEXT = "Сигнал выхода"
SetLabelParams(chart_tag, label_id, params)
DeleteLabel(chart_tag, label_id)
```

## РАЗДЕЛ 17A. БАЗОВЫЕ ПАТТЕРНЫ QLUA API (17.1–17.30)

## 17.1. Получение позиций FORTS
```lua
local function get_positions()
 local pos = {}
 local n = getNumberOf("futures_client_holding")
 for i = 0, n - 1 do
 local item = getItem("futures_client_holding", i)
 if item and item.sec_code then
 pos[item.sec_code] = item.total_net or item.totalnet or 0
 end
 end
 return pos
end
```

## 17.2. Жизненный цикл подписок
```lua
-- Заказ (с getParamEx2!)
ParamRequest(CLASS_CODE, sec_code, "BID")
ParamRequest(CLASS_CODE, sec_code, "LAST")
-- ...
-- Отмена при удалении инструмента
CancelParamRequest(CLASS_CODE, sec_code, "BID")
CancelParamRequest(CLASS_CODE, sec_code, "LAST")
```

## 17.3. Синхронизация списка инструментов
```lua
local function sync_instruments()
 local class_secs = getClassSecurities(CLASS_CODE)
 for sec_code in string.gmatch(class_secs, "[^,]+") do
 sec_code = string.gsub(sec_code, "%s", "")
 if is_valid_instrument(sec_code) then
 -- обработка
 end
 end
end
```

## 17.4. Расчёт рублёвой маржи (ВМ, не ГО!)
```lua
local function calc_var_margin(last, clprice, min_step, step_price)
 if not last or not clprice or not min_step or not step_price then return nil end
 if min_step == 0 or step_price == 0 then return nil end
 return (last - clprice) / min_step * step_price
end
```
★ Это ВМ, а НЕ ГО. ГО считается по SPAN-модели (см. разделы 30–33).

## 17.5. Подсветка алертов
```lua
SetColor(t_id, row, -1, RGB(200, 255, 200)) -- зелёная
SetColor(t_id, row, -1, RGB(255, 200, 200)) -- красная
SetColor(t_id, row, -1, RGB(255, 255, 200)) -- жёлтая
```

## 17.6. Экспорт в CSV (ANSI, ; разделитель)
```lua
local f = io.open(filepath, "w")
f:write(table.concat({"col1", "col2"}, ";") .. "\n")
f:close()
```

## 17.7. Автоподбор ширины колонок
```lua
local function measure_widths(data, col_names)
 local widths = {}
 for i, name in ipairs(col_names) do
 widths[i] = string.len(name) + 4
 end
 for _, row in pairs(data) do
 for i, cell in ipairs(row) do
 local w = string.len(tostring(cell)) + 4
 if w > (widths[i] or 0) then widths[i] = w end
 end
 end
 for i = 1, #widths do
 widths[i] = math.max(20, math.min(80, widths[i]))
 end
 return widths
end
```

## 17.8. Ретрай создания таблицы
```lua
local function try_create_table(retries)
 for attempt = 1, retries do
 local tid = create_table()
 if tid then return tid end
 sleep(1000)
 end
 return nil
end
```

## 17.9. Флаг is_recreating
```lua
is_recreating = true
-- ... пересоздание таблицы ...
is_recreating = false

function OnQTableClose(tid)
 if is_recreating then return true end
 is_run = false
 return true
end
```

## 17.10. Пауза после ParamRequest
```lua
ParamRequest(...)
sleep(2000) -- ждём данные
```

## 17.11. Кэширование собранных данных
```lua
local last_all_rows = nil
-- В update_data_only:
local all_rows = collect_data(false)
last_all_rows = all_rows
-- В экспорте CSV:
if last_all_rows and #last_all_rows > 0 then
 export_csv(last_all_rows)
end
```

## 17.12. read_orderbook — безопасное чтение стакана
```lua
local function read_orderbook(class, sec)
 local ql = getQuoteLevel2(class, sec)
 if ql == nil or type(ql) ~= "table" then return nil end
 if ql.bid_count == nil or ql.bid_count == "" then return nil end
 local bid_count = tonumber(ql.bid_count) or 0
 local ask_count = tonumber(ql.offer_count) or 0
 if bid_count == 0 and ask_count == 0 then return nil end
 return ql
end
```

## 17.13. get_futures_position — getFuturesHolding + fallback
```lua
local function get_futures_position(firmid, account, sec_code)
 local h = getFuturesHolding(firmid, account, sec_code, 0)
 if h then
 return { net = to_int(h.total_net or h.totalnet or 0),
 varmargin = h.varmargin or 0 }
 end
 -- Fallback: перебор
 local n = getNumberOf("futures_client_holding")
 for i = 0, n - 1 do
 local item = getItem("futures_client_holding", i)
 if item and item.sec_code == sec_code then
 return { net = to_int(item.total_net or item.totalnet or 0),
 varmargin = item.varmargin or 0 }
 end
 end
 return { net = 0, varmargin = 0 }
end
```

## 17.14. send_order — с ACCOUNT и пассивными заявками
```lua
local function send_order(class, sec, account, client_code, op, price, qty, passive)
 local t = {
 ["TRANS_ID"] = tostring(os.time()),
 ["ACTION"] = "NEW_ORDER",
 ["CLASSCODE"] = class,
 ["SECCODE"] = sec,
 ["OPERATION"] = op, -- "B" or "S"
 ["PRICE"] = tostring(price),
 ["QUANTITY"] = tostring(math.abs(qty)),
 ["TYPE"] = "L",
 ["ACCOUNT"] = account, -- ОБЯЗАТЕЛЕН
 ["CLIENT_CODE"] = client_code,
 }
 if passive then
 t["Условие исполнения"] = "Только пассивная"
 end
 return sendTransaction(t)
end
```

## 17.14a. cancel_order — снятие заявки (KILL_ORDER)
```lua
-- ★ Снятие заявки по номеру биржи (ORDER_KEY) или по TRANS_ID
-- Для FORTS: ORDER_KEY — из OnOrder/OnTransReply
-- ВАЖНО: order_key берётся из поля order_num ответа OnOrder, НЕ из sendTransaction!
local function cancel_order(class, sec, account, client_code, order_key)
 local t = {
 ["TRANS_ID"] = tostring(os.time()),
 ["ACTION"] = "KILL_ORDER",
 ["CLASSCODE"] = class,
 ["SECCODE"] = sec,
 ["ACCOUNT"] = account,
 ["CLIENT_CODE"] = client_code,
 ["ORDER_KEY"] = tostring(order_key),
 }
 return sendTransaction(t)
end

-- Снятие всех заявок по инструменту (KILL_ALL_ORDERS)
local function cancel_all_orders(class, sec, account, client_code)
 local t = {
 ["TRANS_ID"] = tostring(os.time()),
 ["ACTION"] = "KILL_ALL_ORDERS",
 ["CLASSCODE"] = class,
 ["SECCODE"] = sec,
 ["ACCOUNT"] = account,
 ["CLIENT_CODE"] = client_code,
 }
 return sendTransaction(t)
end
```

★ Грабля #165: ORDER_KEY — это номер заявки на бирже, не TRANS_ID.
 TRANS_ID — ваш внутренний номер транзакции, ORDER_KEY — биржевый номер.
 TRANS_ID можно использовать для отмены через поле ["TRANS_ID"] = trans_id,
 но ORDER_KEY надёжнее (TRANS_ID может быть переиспользован при os.time()).

## 17.14b. move_order — перемещение заявки (MOVE_ORDER)
```lua
-- ★ Перемещение = снятие старой + постановка новой в одной транзакции
-- Для FORTS: MOVE_ORDER — атомарная операция, быстрее чем cancel+send
-- price — новая цена, qty — новое количество (можно уменьшить)
local function move_order(class, sec, account, client_code,
 order_key, new_price, new_qty)
 local t = {
 ["TRANS_ID"] = tostring(os.time()),
 ["ACTION"] = "MOVE_ORDER",
 ["CLASSCODE"] = class,
 ["SECCODE"] = sec,
 ["ACCOUNT"] = account,
 ["CLIENT_CODE"] = client_code,
 ["ORDER_KEY"] = tostring(order_key),
 ["PRICE"] = tostring(new_price),
 ["QUANTITY"] = tostring(math.abs(new_qty)),
 }
 return sendTransaction(t)
end
```

★ Перемещение сохраняет очередь в стакане при уменьшении количества.
★ При увеличении количества — заявка теряет очередь (становится новой).
★ Грабля #166: MOVE_ORDER возвращает "OK" даже если старая заявка уже исполнена.
 Проверяйте статус заявки через order_tracker перед перемещением.

## 17.14c. order_tracker — отслеживание через OnOrder и OnTransReply
```lua
-- ★ Жизненный цикл заявки: sendTransaction → OnTransReply → OnOrder
-- OnTransReply: ответ на транзакцию (принята/отклонена биржей)
-- OnOrder: изменение статуса заявки (активна/исполнена/снята)
-- ВАЖНО: OnOrder и OnTransReply вызываются в главном потоке, не в main()!

-- Реестр активных заявок (доступен из main() и callbacks)
local active_orders = {}  -- [order_key] = { trans_id, sec, op, price, qty, status, flags }

-- Обработка ответа на транзакцию (принята/отклонена)
function OnTransReply(trans_reply)
 -- trans_reply.trans_id — ваш TRANS_ID
 -- trans_reply.status — статус: 1=отправлена, 2=выполнена, 3=ошибка, ...
 -- trans_reply.result_msg — текст ошибки (если status=3)

 -- Транзакция отклонена — алерт

 -- Сохраняем привязку trans_id → order_key (если есть)
-- [... код сокращён ...]
end

-- Обработка изменения статуса заявки
function OnOrder(order)
 -- order.order_num — биржевый номер заявки (ORDER_KEY)
 -- order.flags — битовые флаги:
 --   бит 0 (1) — активна
 --   бит 1 (2) — снята
 --   бит 2 (4) — исполнена
 --   бит 4 (16) — лимитная
 --   бит 5 (32) — рыночная
 -- order.qty — заявленное количество
 -- order.balance — неисполненный остаток
 -- order.price — цена заявки

 -- Заявка снята или исполнена — убираем из реестра
 -- Заявка активна — обновляем реестр

-- Получение количества активных заявок (из main())
-- [... код сокращён ...]
end
local function count_active_orders()
-- [... код сокращён ...]
end

-- Проверка: есть ли активная заявка по инструменту (из main())
local function has_active_order(sec_code)
-- [... код сокращён ...]
end
```

★ Грабля #167: OnOrder может прийти несколько раз для одной заявки
 (активна → частично исполнена → исполнена). Обрабатывать по flags, не по факту вызова.
★ Грабля #168: OnTransReply приходит ДО OnOrder. Не считать заявку "активной"
 по OnTransReply — ждать OnOrder с флагом "активна".
★ Грабля #169: bit.band для разбора flags работает в Lua 5.1.
 В Lua 5.3 использовать order.flags & 1 (или to_int + bit32 fallback).
★ Для отмены заявки: взять order_key из active_orders, передать в cancel_order.
★ Для перемещения: проверить has_active_order(sec) перед move_order.

## 17.14d. hedge_stop_loss — хеджевый стоп-лосс на двух субсчетах
```lua
-- ★ Стратегия: позиция на счёте 1, встречная позиция на счёте 2 при касании стопа.
-- ★ Преимущество: нет налогового события (позиция не закрывается).
-- ★ Издержки: двойное ГО (полунеттинг), двойная комиссия.
-- ★ Грабли: #170 (двойное ГО), #171 (гэп мимо лимита), #172 (VM после 19:00), #173 (ACCOUNT = счёт 2)

local Hedge = {
  class = "SPBFUT",
  sec = "",          -- код инструмента
  firmid = "",       -- идентификатор фирмы
  account1 = "",     -- счёт основной позиции
  account2 = "",     -- счёт хеджа
  client_code1 = "",
  client_code2 = "",

-- 1. Отправка стоп-заявки на счёт 2
local function send_stop_order(h)
  -- Направление: лонг → шорт (стоп вниз), шорт → лонг (стоп вверх)

  -- Лимитная цена на 1 шаг хуже триггера (для гарантии заполнения)

-- [... код сокращён ...]
end

-- 2. Проверка двойного ГО (7 проверок)
local function check_hedge_go(h)
  -- Проверка 7: не во время клиринга (23:50–00:30)

  -- Проверка 1+2: ГО с ретраем (грабля #111, паттерн 17.25)

  -- Проверка 6: запас 20% на auto-shift (грабля #113)

  -- Проверка 3: money_amount, не actual_amount (грабля #127)

  -- Проверка 4: индикативная ВМ из getFuturesHolding (не клиринговая, грабля #44)

  -- Проверка 5: НПР1, не НПР2 (полное ГО для открытия)

-- [... код сокращён ...]
end

-- 3. Инициализация хеджевого стопа
local function init_hedge_stop(h)
-- [... код сокращён ...]
end

-- 4. Мониторинг хеджа в main()
local function monitor_hedge(h)

  -- 4a. Проверка срабатывания через order_tracker

  -- 4b. Auto-shift мониторинг (грабля #113)

  -- 4c. VM-парадокс после 19:00 (грабля #172)
    -- ВМ клиринга = (РЦ − цена_сделки) × поз, не (тек − цена_сделки) × поз
    -- Скрипт видит (тек − цена_сделки), но зачислится (РЦ − цена_сделки)
-- [... код сокращён ...]
end

-- 5. Снятие хеджа при развороте цены
local function remove_hedge(h)
  -- 5a. Если стоп-заявка ещё активна — снять
  -- 5b. Если хедж уже открыт — закрыть
-- [... код сокращён ...]
end

-- 6. Trailing hedge — подтягивание стопа за ценой
local function trail_hedge(h, new_stop_price)
  -- Снять старый стоп, поставить новый (MOVE_ORDER не работает для STOP_ORDER)
  -- Сначала поставить новый (двойное ГО на момент перекрытия)
    -- Снять старый стоп
-- [... код сокращён ...]
end

-- 7. Ролловер хеджа при экспирации
local function rollover_hedge(h, new_sec)
  -- Снять хедж по старому контракту
  -- Поставить хедж по новому контракту
  -- Поправка стопа на разницу цен контрактов (если нужно)
-- [... код сокращён ...]
end

-- 8. Суммарный риск по двум счетам
local function check_combined_risk(h)

-- [... код сокращён ...]
end
```

### Связка с паттернами
- `get_go_with_retry` — паттерн 17.25 (ретрай ГО)
- `calc_npr1` — паттерн 17.34 (свободные средства)
- `get_money_amount` — паттерн 17.33 (перебор money_limits)
- `get_futures_position` — паттерн 17.13 (getFuturesHolding + fallback)
- `vm_split` — раздел 24 (раздельный учёт ВМ)
- `order_tracker` / `has_active_order` — паттерн 17.14c
- `cancel_order` / `send_order` — паттерны 17.14a / 17.14
- `is_trading_session` — раздел 18.1

### Связка с граблями
- #170 — двойное ГО (полунеттинг)
- #171 — гэп мимо limit_price (альтернатива — рыночная, 1.5× ГО)
- #172 — VM-парадокс после 19:00 (vm_split)
- #173 — ACCOUNT = счёт 2
- #111 — getParamEx2 возвращает 0 при первом вызове (ретрай)
- #113 — auto-shift ГО внутри дня
- #127 — money_amount, не actual_amount

## 17.14e. recovery — восстановление состояния при перезапуске
```lua
-- ★ Скрипт перезапустился — а позиция уже открыта, стоп стоит.
-- ★ Без recovery скрипт «не знает» про свои заявки. order_tracker пустой.
-- ★ Вызывать в OnInit() после load_holidays().

local function recover_state(h)
  -- 1. Перечитать позиции на обоих счетах

  -- 2. Если позиция на счёте 2 — хедж уже сработал

  -- 3. Перечитать активные заявки через поиск по стоп-заявкам
  --    (StopOrder-и не видны в active_orders из OnOrder при перезапуске)

  -- 4. Восстановить _last_go для auto-shift мониторинга

-- [... код сокращён ...]
end
```

## 17.14f. reconnect — обработка OnDisconnected / OnConnected
```lua
-- ★ Связь упала — стакан устарел, цены заморожены.
-- ★ Восстановилась — переподписаться, перечитать позиции, проверить живые стопы.

local was_disconnected = false

function OnDisconnected()
  -- ★ НЕ отправлять транзакции! Цены устарели.
-- [... код сокращён ...]
end

function OnConnected()
  -- 1. Переподписаться на параметры
  -- 2. Перечитать позиции
  -- 3. Проверить живые стопы через recovery
  -- 4. Проверить ГО
-- [... код сокращён ...]
end
```

## 17.14g. double_send_guard — защита от двойной отправки
```lua
-- ★ main() цикл быстрее биржи. Если цена триггерит стоп на двух циклах подряд —
-- ★ две стоп-заявки. Нужен in_flight флаг + таймаут.

local in_flight = false
local in_flight_time = 0
local IN_FLIGHT_TIMEOUT = 5000  -- мс, ждать ответа биржи

local function guarded_send(tx_func)
  local msk = msk_time()
  local now = msk * 1000
  if in_flight and (now - in_flight_time) < IN_FLIGHT_TIMEOUT then
    return false, "in_flight — ждём ответа биржи"
  end
  in_flight = true
  in_flight_time = now
  local res = tx_func()
  -- Сброс in_flight в OnTransReply
  return res
end

-- Сброс в OnTransReply:
function OnTransReply(trans_reply)
  in_flight = false  -- ★ Сброс флага при любом ответе
  -- ... остальная обработка из паттерна 17.14c ...
end
```

## 17.14h. risk_per_trade — расчёт объёма от допустимого убытка
```lua
-- ★ «Готов потерять 5000 ₽, стоп на 50 пунктов» →
-- ★ qty = risk_amount / (stop_points × step_price)

local function calc_qty(risk_amount, stop_points, step_price)
  if stop_points == 0 or step_price == 0 then return 0 end
  local qty = math.floor(risk_amount / (stop_points * step_price))
  return math.max(qty, 0)  -- минимум 0
end

-- Пример: риск 5000 ₽, стоп 50 шагов, step_price = 1 ₽
-- qty = math.floor(5000 / (50 * 1)) = 100 контрактов

-- Для Si: step_price = 1, SEC_PRICE_STEP = 1 →
-- qty = math.floor(5000 / (50 * 1)) = 100

-- Для RTS: step_price = 0.2, SEC_PRICE_STEP = 10 →
-- Если стоп на 100 пунктов (10 шагов по 10):
-- qty = math.floor(5000 / (10 * 0.2)) = 2500  ← проверить лимит концентрации!
```

## 17.15. can_trade — сессия + клиринг + РЦ
```lua
local function can_trade(msk_now, sec_code)
 if not is_trading_session() then return false end
 local t = os.date("*t", msk_now)
 if t.hour == 23 and t.min >= 50 then return false end -- клиринг
 if t.hour == 0 and t.min <= 30 then return false end -- клиринг
 -- Проверка окон экспирации для конкретного инструмента
 if sec_code then
 local etype, etime = get_expiry_type(sec_code)
 if etime == "14:00" then
 -- Не торговать ±2 минуты вокруг 14:00 в день экспирации
 if t.hour == 13 and t.min >= 58 then return false end
 if t.hour == 14 and t.min <= 2 then return false end
 elseif etime == "19:00" then
 if t.hour == 18 and t.min >= 58 then return false end
 if t.hour == 19 and t.min <= 2 then return false end
 end
 end
 return true
end
```

## 17.16. orderbook_imbalance — дисбаланс стакана
```lua
local function orderbook_imbalance(ql)
 if not ql then return 0 end
 local bid_vol, ask_vol = 0, 0
 for i = 1, tonumber(ql.bid_count) or 0 do
 bid_vol = bid_vol + tonumber((ql.bid[i] or {}).quantity or 0)
 end
 for i = 1, tonumber(ql.offer_count) or 0 do
 ask_vol = ask_vol + tonumber((ql.offer[i] or {}).quantity or 0)
 end
 local total = bid_vol + ask_vol
 if total == 0 then return 0 end
 return (bid_vol - ask_vol) / total
end
```

## 17.17. sentiment — сентимент по ленте (volume-weighted, band())
```lua
-- ★ Volume-Weighted Sentiment (WVTS) — доля покупок по объёму, а не по количеству сделок
-- ★ WVTS = Σ(qty_buy) / (Σ(qty_buy) + Σ(qty_sell))
-- ★ 0.5 = нейтрально, >0.7 = давление вверх, <0.3 = давление вниз
-- ★ Грабля #180: bit.band без fallback — использовать band() из раздела 11
-- ★ Грабля #181: сентимент без объёма — 100 сделок по 1 лоту ≠ 1 сделка на 100 лотов
-- ★ Использует: band() из раздела 11, OnAllTrade из раздела 13
-- ★ Связка: 17.17d (дивергенция WVTS vs cum_delta), 17.17e (trade_speed)

local sentiment_state = {
  trades = {},       -- кольцевой буфер {flags, qty, price, time}

-- Вызывать из OnAllTrade (через флаг, не напрямую — грабля #95)
local function push_trade(trade)
-- [... код сокращён ...]
end

-- Volume-weighted sentiment за последние N сделок
-- Возвращает: wvts (0..1), buy_vol, sell_vol
local function calc_sentiment(n)

-- Volume-weighted sentiment за последние T секунд
-- Возвращает: wvts (0..1), buy_vol, sell_vol
-- [... код сокращён ...]
end
local function calc_sentiment_time(window_sec)
```
## 17.17a. order_flow_delta — кумулятивная дельта потока ордеров
```lua
-- ★ Кумулятивная дельта = Σ(qty × direction) по всем сделкам
-- ★ Дивергенция дельта/цена — классический разворотный сигнал:
--    цена растёт, дельта падает → покупатели исчерпаны → разворот вниз
--    цена падает, дельта растёт → продавцы исчерпаны → разворот вверх
-- ★ Грабля #174: OnAllTrade.flags через band() — НЕ bit.band (грабля #169)
-- ★ Грабля #175: сброс дельты в клиринг 23:50 — иначе копится мусор
-- ★ Использует: band() из раздела 11, OnAllTrade из раздела 13

local delta_state = {
  trades = {},        -- кольцевой буфер последних N сделок

-- Вызывать из OnAllTrade (через флаг, не напрямую — грабля #95)
local function update_delta(trade)
  -- Направление через band() (грабля #169: bit.band без fallback)
    -- Покупка (агрессор купил)
    -- Продажа (агрессор продал)
  -- Кольцевой буфер

-- Сброс дельты в клиринг (грабля #175)
-- [... код сокращён ...]
end
local function reset_delta()
-- [... код сокращён ...]
end

-- Детекция дивергенции дельта/цена
-- window — количество тиков для сравнения
-- Возвращает: "bullish_div" (цена вниз, дельта вверх → разворот вверх),
--            "bearish_div" (цена вверх, дельта вниз → разворот вниз),
--            nil (нет сигнала)
local function detect_divergence(window)
  -- Порог: минимальное движение цены (2 шага) и минимальное изменение дельты (10 контрактов)
  -- Дивергенция: цена и дельта в разные стороны

-- Дельта за период (N последних сделок)
-- [... код сокращён ...]
end
local function delta_over(n)
-- [... код сокращён ...]
end
```

## 17.17b. large_order_detector — стены и крупные заявки в стакане
```lua
-- ★ Детекция «стен» — аномально крупных заявок в стакане
-- ★ Появление/исчезновение стены — информативный сигнал:
--    стена на биде → поддержка (крупный игрок защищает уровень)
--    стена на аске → сопротивление (крупный игрок продаёт)
--    исчезновение стены за 1 тик до касания → крупный игрок снял
--      заявку (не хочет исполняться) → ложный уровень → пробой вероятен
-- ★ Грабля #176: getQuoteLevel2 возвращает объём в лотах, не в рублях
-- ★ Грабля #177: стена может быть айсбергом (часть видна, часть скрыта) —
--    QUIK не показывает айсберги, учитывать только видимую часть
-- ★ Использует: read_orderbook (17.12), OnQuote (флаг из 17.17 callbacks)

local wall_state = {
  prev_walls = {},    -- [{side, price, qty}] — стены предыдущего снимка

-- Расчёт среднего размера заявки
local function calc_avg_order_size(ql)
-- [... код сокращён ...]
end

-- Детекция стен — возвращает массив найденных стен
-- wall = {side="bid"/"ask", price=N, qty=N, level=N (глубина в стакане)}
local function detect_walls(ql)
  -- Скользящее среднее

  -- Сканируем биды
  -- Сканируем аски
-- [... код сокращён ...]
end

-- Сравнение со предыдущим снимком — детекция исчезновения стен
-- Возвращает: {removed = {...}, added = {...}}
local function compare_walls(new_walls)
-- [... код сокращён ...]
end

-- Полный анализ: стены + изменения
-- Возвращает: {walls=..., added=..., removed=..., signal=...}
-- signal: "wall_bid" (поддержка), "wall_ask" (сопротивление),
--         "wall_removed_bid" (поддержка снята → пробой вниз вероятен),
--         "wall_removed_ask" (сопротивление снято → пробой вверх вероятен)
local function analyze_walls(ql)
  -- Новая стена
  -- Исчезновение стены — более сильный сигнал
-- [... код сокращён ...]
end
```

## 17.17c. oi_pressure — давление открытого интереса
```lua
-- ★ Открытый интерес (ОИ) — количество открытых позиций по инструменту
-- ★ Рост ОИ + рост цены = новые лонги (быки открывают) → давление вверх
-- ★ Рост ОИ + падение цены = новые шорты (медведи открывают) → давление вниз
-- ★ Снижение ОИ = позиционники закрываются → тренд затухает
-- ★ Грабля #178: getParamEx2("OPENPOSITION") — это НЕ ОИ, это открытая
--    позиция клиента. ОИ = getParamEx2("NUMCONTRACTS") или getParamEx2("OPENPOSITION")
--    в зависимости от версии QUIK. Проверять оба параметра.
-- ★ Грабля #179: ОИ меняется дискретно (в клиринг) — внутри дня виден
--    только через NUMCONTRACTS, которая обновляется с задержкой
-- ★ Горизонт: часы-дни. Не для скальпинга.
-- ★ Использует: getParamEx2 (раздел 15.1), get_clprice (17.21)

local oi_state = {
  history = {},       -- [{oi, price, time}] — история замеров

-- Чтение ОИ (с fallback)
local function get_oi(class, sec)
  -- Попытка 1: NUMCONTRACTS (количество контрактов)
  -- Попытка 2: OPENPOSITION (открытая позиция)
-- [... код сокращён ...]
end

-- Замер ОИ + цены — вызывать периодически (не каждый тик!)
-- Интервал: 1–5 минут (ОИ меняется медленно)
local function sample_oi(class, sec)

  -- Сохранение в историю

  -- Расчёт сигнала
    -- Порог: изменение ОИ > 1% и движение цены

-- Накопленный сигнал за N замеров
-- Возвращает: "bullish" (больше new_longs + short_covering),
--             "bearish" (больше new_shorts + long_unwinding),
--             nil (нет сигнала)
-- [... код сокращён ...]
end
local function oi_trend(n)
```

## 17.17d. sentiment_delta_divergence — дивергенция WVTS vs cum_delta
```lua
-- ★ Самый сильный сигнал: отличие «толпы» от «крупняка»
-- ★ Сентимент бычий (>0.7), дельта медвежья (<0) → крупный игрок продаёт мелким → bearish
-- ★ Сентимент медвежий (<0.3), дельта бычья (>0) → крупный игрок покупает у мелких → bullish
-- ★ Грабля #181: сентимент без объёма — WVTS решает (patтерн 17.17)
-- ★ Использует: calc_sentiment (17.17), delta_state.cum_delta (17.17a)

local function detect_sentiment_delta_divergence(sentiment_window)

  -- Сентимент бычий, дельта медвежья → smart money selling
  -- Сентимент медвежий, дельта бычья → smart money buying

```

## 17.17e. trade_speed — скорость ленты как фильтр силы сигнала
```lua
-- ★ Скорость ленты = количество сделок в секунду
-- ★ Всплеск активности + WVTS > 0.8 = прорыв (сильный сигнал)
-- ★ Тихий рынок + WVTS > 0.8 = ложный сигнал (нечего двигать)
-- ★ Грабля #182: скорость без порога активности — ложные срабатывания в простое
-- ★ Использует: sentiment_state.trades (17.17)

local function calc_trade_speed(window_sec)
-- [... код сокращён ...]
end

-- Фильтр: подтверждение сентимента скоростью ленты
-- Возвращает: "breakout" (прорыв), "noise" (ложный), nil (недостаточно данных)
local function confirm_sentiment_by_speed(wvts, speed_threshold)

```
## 17.17f. signal_aggregator — агрегатор 5+ сигналов в один verdict

```lua
-- ★ Собирает 5+ сигналов (WVTS, delta, OI, smart money, speed) в один verdict
-- ★ Матрица 4×4: строки — сентимент (WVTS > 0.7 / < 0.3 / нейтрально / smart money div),
--   колонки — OI (растёт / падает / плоский / нет данных)
-- ★ Лента приоритетнее ОИ: при отсутствии или задержке ОИ решение принимается по ленте
-- ★ ОИ — подтверждение, не фильтр
-- ★ action: hold / buy / sell, strength: 1 (weak) / 2 (strong) / 3 (strongest)

local function aggregate_signals()
  -- Слой 1: OI контекст (медленный, раз в 1-5 мин)
  -- Слой 2: Sentiment (быстрый, каждый цикл)
  -- Слой 3: Delta divergence (быстрый)
  -- Слой 4: Large trade flow (быстрый, из ленты)
  -- Слой 5: Delta velocity (быстрый, из ленты)
  -- Слой 6: VWAP spread (быстрый, из ленты)

  -- OI контекст
    -- OI нейтральный — решаем по ленте

  -- Exit overlay

```

## 17.17g. position_sizer — масштабирование объёма по strength сигнала

```lua
-- ★ strength 1 = 1/3 риска, 2 = 2/3, 3 = полный
-- ★ Грабля #186: одинаковый объём на weak и strong = перериск на слабых сигналах

local function size_from_strength(strength, max_risk, stop_points, step_price)
  local fraction = strength / 3
  local adjusted_risk = max_risk * fraction
  return calc_qty(adjusted_risk, stop_points, step_price)  -- 17.14h
end
```

## 17.17h. delta_velocity — ускорение дельты из ленты

```lua
-- ★ Лидирующий сигнал: delta растёт, но замедляется → импульс затухает
-- ★ Грабля #188: на тонком рынке 2 сделки за 10 сек дадут шум. Фильтр: минимум N сделок

local function delta_velocity(window_sec)
  window_sec = window_sec or 10
  local total = #delta_state.trades
  if total < 2 then return 0 end
  local now = delta_state.trades[total]
  local cutoff_idx = math.max(1, total - 30)
  local past = delta_state.trades[cutoff_idx]
  local dt = (now.delta ~= nil and past.delta ~= nil)
    and (now.delta - past.delta) or 0
  return dt
end
```

## 17.17i. large_trade_flow — поток крупных сделок из ленты

```lua
-- ★ Замена ОИ в реал-тайме: ОИ с задержкой 5-15 мин не покажет,
--   что крупняк зашёл сейчас — лента покажет сразу
-- ★ Грабля #187: 50 лотов для RIM5 и SiZ5 — разные весовые категории.
--   Нужен динамический порог: медиана объёма × N

local large_flow_state = {

local function push_large_trade(trade)
-- [... код сокращён ...]
end

local function large_trade_sentiment(window_sec)
-- [... код сокращён ...]
end
```

## 17.17j. vwap_spread — VWAP покупок vs VWAP продаж из ленты

```lua
-- ★ Агрессивность по цене, не по объёму
-- ★ Если покупатели платят выше VWAP продаж — они агрессивнее
-- ★ Грабля #189: на инструменте со спредом 5 тиков vwap_spread 2 тика — шум.

--   Нормировать на спред

local function vwap_spread(window_sec)
-- [... код сокращён ...]
end
```

## 17.17k. time_filters — временные фильтры запрета входа

```lua
-- ★ Три окна, когда НЕ открывать новые позиции:
--   18:58-19:02 МСК — фиксация РЦ, VM-парадокс → не открывать, мониторить стопы
--   23:45-23:55 МСК — клиринг → сброс delta, sentiment, не торговать
--   Первые 5 мин после открытия — разгон стакана → только наблюдение

local function is_entry_blocked(hour, min, sec)
  local msk_min = hour * 60 + min  -- минуты от начала суток МСК
  -- 18:58-19:02
  if msk_min >= 18*60+58 and msk_min <= 19*60+2 then return true, "РЦ fixation" end
  -- 23:45-23:55
  if msk_min >= 23*60+45 and msk_min <= 23*60+55 then return true, "clearing" end
  -- Первые 5 мин после открытия (07:00-07:05)
  if msk_min >= 7*60 and msk_min <= 7*60+5 then return true, "warmup" end
  return false, nil
end
```

## 17.18. phantom_leverage — фантомное плечо
```lua
local function phantom_leverage(rub_margin, go_long, go_short)
 local go_min = math.min(go_long, go_short)
 if go_min <= 0 then return 0 end
 return math.floor(math.abs(rub_margin) / go_min)
end
```

## 17.19. phantom_vm_pos — фантомная ВМ для позиции
```lua
local function phantom_vm_pos(net, rub_margin)
 if net == 0 then return 0 end
 local long = net > 0
 local vm = math.abs(rub_margin) * math.abs(net)
 -- Лонг ниже РЦ → фантом положительный
 -- Шорт выше РЦ → фантом положительный
 if (long and rub_margin < 0) or (not long and rub_margin > 0) then
 return vm
 end
 return nil -- нет фантома (неправильное направление)
end
```

## 17.20. sort_by_phantom — сортировка по плечу
```lua
local function sort_by_phantom(sec_list, instruments, rc_forecasts)
 table.sort(sec_list, function(a, b)
 local pa = rc_forecasts[a] and math.abs(rc_forecasts[a])
 or 0
 local pb = rc_forecasts[b] and math.abs(rc_forecasts[b])
 or 0
 return pa > pb
 end)
end
```

## 17.21. get_clprice — через getParamEx2
```lua
local function get_clprice(class, sec)
 local pe = getParamEx2(class, sec, "CLPRICE")
 local clprice = nil
 if pe and tonumber(pe.result) == 1 then
 clprice = tonumber(pe.param_value)
 end
 if not clprice or clprice == 0 then
 local pe2 = getParamEx2(class, sec, "SETTLEPRICE")
 if pe2 and tonumber(pe2.result) == 1 then
 clprice = tonumber(pe2.param_value)
 end
 end
 return clprice
end
```

## 17.22. get_rc — РЦ текущего дня
```lua
local function get_rc(class, sec, msk_now)
 -- После 19:00: LASTCLOSED → last → CLPRICE
 local pe = getParamEx2(class, sec, "LASTCLOSED")
 if pe and tonumber(pe.result) == 1 then
 local v = tonumber(pe.param_value)
 if v and v > 0 then return v end
 end
 local t = os.date("*t", msk_now)
 if t.hour >= 19 then
 pe = getParamEx2(class, sec, "LAST")
 if pe and tonumber(pe.result) == 1 then
 return tonumber(pe.param_value)
 end
 end
 return get_clprice(class, sec)
end
```

## 17.23. rc_sampling — сэмплирование до 19:00:00
```lua
-- Окно: 18:58:00–19:00:00 (было до 18:58:55 — теряли 65 сек)
local RC_START_SEC = 68280 -- 18:58:00
local RC_END_SEC = 68400 -- 19:00:00

local function rc_sampling_tick(msk_now, sec_list, samples)
 local t = os.date("*t", msk_now)
 local time_sec = t.hour * 3600 + t.min * 60 + t.sec
 if time_sec >= RC_START_SEC and time_sec <= RC_END_SEC then
 -- сэмплирование bid/ask/last каждые RC_FREQ_SEC
 end
end
```

## 17.24. get_go — получение ГО (правильная интерпретация)
```lua
-- ★ BUYDEPO = ГО лонга (не путать с документацией QUIK!)
-- ★ SELLDEPO = ГО шорта
local function get_go(class, sec, is_long)
 local param = is_long and "BUYDEPO" or "SELLDEPO"
 local pe = getParamEx2(class, sec, param)
 if pe and tonumber(pe.result) == 1 then
 local v = tonumber(pe.param_value) or 0
 -- Округление до копеек (грабля #120/N18)
 return math.floor(v * 100 + 0.5) / 100
 end
 return 0
end
```

## 17.25. get_go_with_retry — ретрай при нулевом ГО
```lua
local function get_go_with_retry(class, sec, is_long, max_retries)
 max_retries = max_retries or 100
 local param = is_long and "BUYDEPO" or "SELLDEPO"
 for i = 1, max_retries do
 local pe = getParamEx2(class, sec, param)
 if pe and tonumber(pe.result) == 1 then
 local v = tonumber(pe.param_value) or 0
 if v > 0 then
 return math.floor(v * 100 + 0.5) / 100
 end
 end
 sleep(100)
 end
 return 0
end
```

## 17.26. auto_shift_monitor — мониторинг роста ГО
```lua
local function auto_shift_monitor(class, sec, prev_go, is_long)
 local go = get_go(class, sec, is_long)
 if prev_go and go > prev_go * 1.1 then
 -- ГО выросло >10% — возможно auto-shift
 return true, go
 end
 return false, go
end
```

## 17.27. get_go_min — минимальное ГО (для фантомного плеча)
```lua
local function get_go_min(class, sec)
 local go_long = get_go(class, sec, true)
 local go_short = get_go(class, sec, false)
 return math.min(go_long, go_short)
end
```

## 17.28. check_concentration — проверка лимитов концентрации
```lua
-- MR2/LK1, MR3/LK2: при превышении позиции — ГО выше, чем показывает QUIK
local function check_concentration(net, lk1, lk2)
 local abs_net = math.abs(net)
 if lk2 and abs_net > lk2 then
 return 3 -- MR3 — самое высокое ГО
 elseif lk1 and abs_net > lk1 then
 return 2 -- MR2 — повышенное ГО
 end
 return 1 -- MR1 — базовое ГО (то, что показывает QUIK)
end
```

## 17.29. check_nci — проверка NCI(БА) перед экспирацией
```lua
-- NCI(БА): за N расчётных периодов до экспирации включается Полунеттинг
-- ГО растёт, т.к. льгота по календарному спреду отключается
local function check_nci(days_to_expiry, nci_periods)
 if days_to_expiry <= nci_periods then
 return true -- Полунеттинг активен, ГО выше
 end
 return false
end
```

## 17.30. calc_net_option_value — NetOptionValue
```lua
-- NetOptionValue = сумма(vol × P_opt × MinStepPrice / MinStep)
-- Для маржируемых опционов = 0
-- Влияет на расчёт валютной надбавки R
local function calc_net_option_value(positions)
 local nov = 0
 for _, p in ipairs(positions) do
 if p.is_premium then
 local val = p.volume * p.opt_price * p.step_price / p.min_step
 nov = nov + val
 end
 end
 return nov
end
```

## РАЗДЕЛ 17B. FORTS-ПАТТЕРНЫ QLUA API (17.31–17.52)

## 17.31. check_ets_date — проверка даты начала полного расписания
```lua
-- Расписание 06:50–23:50 действует с 14 июля 2026
-- До 14 июля — переходный период (другое расписание)
local function check_ets_date()
 local now = msk_time()  -- НЕ os.time()! os.time() = локальное время машины, не МСК (грабля #14)
 local ets_full = os.time{year=2026, month=7, day=14, hour=0}
 return now >= ets_full
end

-- В is_trading_session:
-- if check_ets_date() then start = 06:50 else start = 07:00 end
```

## 17.32. get_param_fast — быстрое чтение параметров
```lua
-- getParamEx — архив терминала (медленнее, работает в OnParam)
-- getParamEx2 — Таблица текущих торгов (быстрее, для main())
local function get_param_fast(class, sec, param)
 -- В main() — getParamEx2 (быстро)
 -- В OnParam — getParamEx (архив, но работает в callback)
 local pe = getParamEx2(class, sec, param)
 if pe and tonumber(pe.result) == 1 then
 return tonumber(pe.param_value)
 end
 -- Fallback на getParamEx
 pe = getParamEx(class, sec, param)
 if pe and tonumber(pe.result) == 1 then
 return tonumber(pe.param_value)
 end
 return nil
end
```

## 17.33. get_money_amount — получение money_amount с MTM-регистрами
```lua
-- money_amount включает MTM-регистры (фантомная ВМ)
-- После клиринга 23:50 — фантомная ВМ уже в money_amount
-- НПР1 = money_amount + rmt_vm – rmt_im
local function get_money_amount()
 -- Перебор всех записей money_limits с фильтром
 -- Было: getItem("money_limits", 0) — может вернуть случайный лимит
 -- Фильтр: рубли (SUR), основной лимит (limit_kind=0)
 -- Fallback: getFuturesLimit (прямая функция QUIK, надёжнее, но может вернуть nil в клиринг)
 -- local fl = getFuturesLimit(firmid, account, 0, "SUR")
 -- if fl then return tonumber(fl.currentbal) or 0 end
-- [... код сокращён ...]
end

-- Расчёт доступного ГО с учётом фантома:
local function calc_available_go()
-- [... код сокращён ...]
end
```

## 17.34. calc_npr1 / calc_npr2 — претрейд-проверка
```lua
-- НПР1 — для открытия новых позиций (полное ГО)
-- НПР2 — для поддержания позиций (половинное ГО)
local function calc_npr1(money_amount, rmt_vm, rmt_im)
 return money_amount + rmt_vm - rmt_im
end

local function calc_npr2(money_amount, rmt_vm, rmt_im)
 return money_amount + rmt_vm - rmt_im / 2
end

-- Доп. контракты через фантом:
-- extra = floor(npr1 / go_per_contract)
-- Если npr1 > 0 — фантомная ВМ доступна как ГО ✅
```

## 17.35. get_expiry_time — определение времени экспирации
```lua
-- Экспирация: 14:00 или 19:00 (зависит от инструмента)
-- Расчётные фьючерсы — онлайн в торгах
-- Поставочные фьючерсы — в клиринге m-t-m (23:50)
local function get_expiry_type(sec_code)

 -- Уровень 1: SECTYPE через getParamEx2 (если биржа транслирует)
 -- Типы: 1=расчётный, 2=поставочный (зависит от спецификации)

 -- Уровень 2: проверка по списку известных поставочных фьючерсов
 -- Список ведётся вручную — обновлять при появлении новых инструментов
 -- Акции-поставочные: добавлять по мере появления

 -- Уровень 3: эвристика по типу инструмента
 -- Вечные фьючерсы → cash 19:00
 -- KEYRATE → cash 19:00 (экспирация в дни заседаний ЦБ)
 -- По умолчанию — расчётный фьючерс, экспирация 14:00
```

## 17.36. check_new_instruments — проверка новых фьючерсов
```lua
-- 20 вечных фьючерсов (сентябрь 2026): AMDF, TSLAF, APPF, COINF и др.
-- KEYRATE (KK): экспирация в дни заседаний ЦБ
-- Криптовечные: BTCUSDF, ETHUSDF, SOLUSDF, XRPUSDF, TRXUSDF
local function is_eternal_futures(sec_code)
 -- Универсальный фильтр: вечные фьючерсы имеют FUNDING_RATE
 local fr = getParamEx2(CLASS_CODE, sec_code, "FUNDING_RATE")
 return fr and fr.result and fr.param_value ~= "0" and fr.param_value ~= ""
end

local function is_keyrate(sec_code)
 -- KEYRATE: БА = индекс ключевой ставки
 -- Экспирация в дни заседаний ЦБ (не по стандартному календарю)
 return sec_code:match("^KK") ~= nil
end
```

## 17.37. check_weekend_session — выходные → следующий день
```lua
-- ДСВД (суббота): торги 10:00–19:00, относятся к СЛЕДУЮЩЕМУ рабочему дню
-- Исключение из ЕТС-правила «вечерняя = текущий день»
local function is_weekend_session()
 local trade_date = getInfoParam("TRADEDATE")
 if not trade_date then return false end
 -- Проверка: суббота (воскресенье — нет торгов)
  local y, m, d = string.match(trade_date, "(%d%d)%.(%d%d)%.(%d%d%d%d)")
  if not y then return false end
  local t = os.time{year=tonumber(y), month=tonumber(m), day=tonumber(d)}
  local wday = os.date("%w", t) -- 0=вс, 6=сб
  return wday == "6"
end
end
```

## 17.38. check_obosoblennie — проверка обособления
```lua
-- Обособленный клиент: переход к другому УК без согласия базового
-- Обособленная БФ: изоляция обеспечения
-- Проверка: отчёт EQM20 (соответствие Расчётного кода Обособленному клиенту)
local function is_obosoblenny_client(client_code)
 -- Универсальная проверка: наличие признака обособления
 -- В QUIK: проверка через getFuturesHolding (изолированный учёт)
 local holding = getFuturesHolding(firmid, account, sec_code, 0)
 if holding and holding.is_obosoblenny then -- QUIK 9.x+: поле is_obosoblenny
 return true
 end
 -- Fallback для старых версий: проверка через отчёт EQM20
 -- (соответствие Расчётного кода Обособленному клиенту)
 return false
end
```

## 17.39. calc_free_amount — формула свободных средств из отчётов
```lua
-- ★ Формула из спецификации клиринговых отчётов (CL_CSV_reports.pdf)
-- amount_end = amount_begin + in_out_netto + var_marg + prem + charges
-- amount_end_mtm = amount_end + var_marg_mtm + prem_mtm + charges_mtm
-- free = amount_end_mtm - go + nov
-- nov = NetOptionValue (оценочная стоимость опционов)
-- В Расчётную сессию (20:00): nov=0, go=0, free=0 в отчёте monsettlcl
local function calc_free(amount_begin, in_out_netto, var_marg, prem, charges,
 var_marg_mtm, prem_mtm, charges_mtm, go, nov)
 local amount_end = amount_begin + in_out_netto + var_marg + prem + charges
 local amount_end_mtm = amount_end + var_marg_mtm + prem_mtm + charges_mtm
 local free = amount_end_mtm - go + (nov or 0)
 return free, amount_end, amount_end_mtm
end
```

## 17.40. calc_vm_eternal — ВМ для вечного фьючерса
```lua
-- ★ Точная формула ВМ для вечного фьючерса (с moex.com)
-- ВМ = Переоценка_позиции - Фандинг × Лот × sign(pos) + Дивид.поправка × Лот × sign(pos)
-- Знак фандинга и дивидендной поправки зависит от направления позиции:
-- Фандинг: лонг платит (−), шорт получает (+)
-- Дивидендная поправка: лонг получает (+), шорт платит (−)
-- Дивидендная поправка: IMOEXF → IMOEXDIV (расчёт в 16:00), RGBIF → 0
-- Учитывается ТОЛЬКО по позиции на предыдущий клиринг (23:50)
local function calc_vm_eternal(pos, revaluation, funding, lot, div_adj)
 -- revaluation = (РЦ_тек - РЦ_пред) × pos -- стандартная переоценка
 -- funding = индекс_фандинга × цена × ставка -- фандинг (всегда >0)
 -- div_adj = значение IMOEXDIV (для IMOEXF) или 0 (всегда >0)
 -- ★ div_adj применяется только к позиции на пред. клиринг, не к новым сделкам
 -- ★ Знак фандинга и дивидендной поправки зависит от направления позиции
 -- Фандинг: лонг платит (−), шорт получает (+)
 -- Дивидендная поправка: лонг получает (+), шорт платит (−)
 -- IMOEXDIV всегда положительное — знак определяется направлением позиции
 local pos_sign = pos > 0 and 1 or (pos < 0 and -1 or 0)
 return revaluation - funding * lot * pos_sign + div_adj * lot * pos_sign
end
```

## 17.41. calc_vm_currency — ВМ для валютных фьючерсов
```lua
-- ★ ВМ для валютных фьючерсов: стоимость шага пересчитывается по индикативному курсу
-- ВМ = РЦ_тек × стоимость_шага_тек / шаг_цены − цена_сделки × стоимость_шага_тек / шаг_цены
-- Стоимость шага меняется при каждом клиринге (по индикативному курсу ЦБ)
local function calc_vm_currency(rc_curr, deal_price, step_price_curr, min_step)
 -- step_price_curr — стоимость шага по текущему индикативному курсу
 if not rc_curr or not deal_price or not step_price_curr or min_step == 0 then return nil end
 local vm_curr = (rc_curr - deal_price) / min_step * step_price_curr
 return vm_curr
end
```

## 17.42. check_removed_fields — проверка удалённых полей отчётов
```lua
-- ★ Удалённые поля (декомиссия): isrepo, account_forts, limit, pr_setll,
-- pr_settl_r, spot, base — старые парсеры сломаются
-- ★ Новые поля: buy_deposit_erc/hrc/lrc/mrc — 4 уровня ГО
-- client_risk_level — уровень риска клиента
-- base_im_buy/sell (заменило basegobuy)
local REMOVED_FIELDS = {
 ["isrepo"] = true, ["account_forts"] = true, ["limit"] = true,
 ["pr_setll"] = true, ["pr_settl_r"] = true, ["spot"] = true, ["base"] = true,
}

local function is_field_removed(field_name)
 return REMOVED_FIELDS[field_name] == true
end

-- Проверка перед парсингом:
-- if is_field_removed(field) then skip — поле больше не существует
```

## 17.43. load_holidays — загрузка календаря праздников Мосбиржи
```lua
-- Загружает даты нерабочих дней Мосбиржи из файла holidays.txt
-- Формат файла: одна дата YYYYMMDD на строку
-- Источник: moex.com/s205 (календарь торговых дней)
-- Вызывать в OnInit()
local holidays = {}
local function load_holidays(filepath)
 filepath = filepath or "holidays.txt"
 local f = io.open(filepath, "r")
 if not f then
 message("holidays.txt не найден — проверка праздников отключена", 1)
 return
 end
 for line in f:lines() do
 local date = string.match(line, "(%d%d%d%d%d%d%d%d)")
 if date then holidays[date] = true end
 end
 f:close()
end
```

## 17.44. get_money_amount_v2 — → см. 17.33
★ Дубликат 17.33. Используйте get_money_amount из паттерна 17.33.

## 17.45. calc_funding_arb_profit — доходность арбитража на фандинге
```lua
-- ★ Расчёт чистой доходности рыночно-нейтрального арбитража: лонг БА + шорт ВФ
-- NET = Фандинг_год − Стоимость_капитала − Комиссии − Спред − Проскальзывание
-- См. раздел 39 для полного описания стратегии
local function calc_funding_arb_profit(funding_annual, capital_cost, commission, spread, slippage)
 local net = funding_annual - capital_cost - commission - spread - slippage
 return net -- > 0 = стратегия прибыльна
end
```

## 17.46. check_funding_sign — проверка знака фандинга
```lua
-- ★ Смена знака фандинга = конструкция становится убыточной (грабля #156)
-- Положительный фандинг: шорт получает платёж, лонг платит
-- Отрицательный фандинг: лонг получает платёж, шорт платит
local function check_funding_sign(funding_rate, is_short)
 if funding_rate == nil or funding_rate == 0 then return nil end
 local positive = funding_rate > 0
 if is_short then
 return positive -- шорт в плюсе при положительном фандинге
 else
 return not positive -- лонг в плюсе при отрицательном фандинге
 end
end
```

## 17.47. calc_fair_spread — справедливый спред срочный vs вечный
```lua
-- ★ Справедливый спред между срочным и вечным фьючерсом
-- Для акций: Спот × Ставка × T × Лот − Дивиденды_нетто × Лот
-- Для валют: Спот × (r_RUB − r_FX) × T × Лот
-- T = дней_до_экспирации / 365
-- См. раздел 40
local function calc_fair_spread(spot, rate, days_to_exp, lot, divs_netto, is_currency, r_fx)
 local T = days_to_exp / 365
 if is_currency then
 return spot * (rate - (r_fx or 0)) * T * lot
 else
 return spot * rate * T * lot - (divs_netto or 0) * lot
 end
end
```

## 17.48. calc_spread_zscore — Z-score спреда
```lua
-- ★ Z-score спреда для входа в арбитраж
-- |Z-score| > 1.5–2 = сигнал на вход
-- Выход при Z-score → 0 или смене знака фандинга
-- См. раздел 40
local function calc_spread_zscore(current_spread, spread_history, window)
 window = window or 20
 if #spread_history < window then return nil end
 local sum, sum_sq = 0, 0
 for i = #spread_history - window + 1, #spread_history do
 sum = sum + spread_history[i]
 end
 local mean = sum / window
 for i = #spread_history - window + 1, #spread_history do
 local d = spread_history[i] - mean
 sum_sq = sum_sq + d * d
 end
 local std = math.sqrt(sum_sq / window)
 if std == 0 then return 0 end
 return (current_spread - mean) / std
end
```

## 17.49. calc_keyrate_vm — ВМ для KEYRATE
```lua
-- ★ ВМ для KEYRATE: ВМ = (РЦ_тек − Цена_входа) × W/R
-- W/R = 1000 ₽ за пункт
-- Изменение на 0,25 п.п. = 250 ₽ на контракт
-- См. раздел 41
local function calc_keyrate_vm(rc_curr, entry_price, wr)
 wr = wr or 1000
 return (rc_curr - entry_price) * wr
end
```

## 17.50. get_keyrate_direction — направление KEYRATE
```lua
-- ★ KEYRATE: цена = ставка напрямую (НЕ «100 минус ставка»)
-- Рост ставки → покупка, снижение → продажа
-- 13.86 = 13.86%, а не 86.14% (грабля #161)
-- См. раздел 41
local prev_keyrate = nil
local function get_keyrate_direction(price)
 -- price = текущая цена KEYRATE (= ожидаемая ставка в %)
 -- Сравнение с предыдущим значением: рост → "buy", снижение → "sell"
 if prev_keyrate == nil then
 prev_keyrate = price
 return "hold" -- недостаточно данных
 end
 local direction
 if price > prev_keyrate then
 direction = "buy" -- ожидание роста ставки
 elseif price < prev_keyrate then
 direction = "sell" -- ожидание снижения ставки
 else
 direction = "hold"
 end
 prev_keyrate = price
 return direction
end
```

## 17.51. check_keyrate_calendar — календарь заседаний ЦБ
```lua
-- ★ KEYRATE: экспирация в дни заседаний ЦБ (не по стандартному календарю)
-- Проверять календарь ЦБ перед торговлей
-- Внеплановое заседание — досрочного исполнения НЕТ (грабля #162)
-- См. раздел 41
local KEYRATE_DATES = {
 -- Обновлять по календарю ЦБ: cbr.ru
 -- ["20261023"] = "KKV6",
 -- ["20261218"] = "KKZ6",
}
local function check_keyrate_calendar(date_str)
 return KEYRATE_DATES[date_str] or nil
end
```

## 17.52. check_keyrate_limits — лимиты цен KEYRATE
```lua
-- ★ Лимиты цен KEYRATE: при достижении дневных лимитов торги останавливаются (грабля #164)
-- Проверять перед постановкой стопов
-- Актуальные лимиты: moex.com/ru/derivatives (ссылка, не конкретные значения)
-- См. раздел 41
local function check_keyrate_limits(price, lower_limit, upper_limit)
 if lower_limit and price <= lower_limit then return true, "lower" end
 if upper_limit and price >= upper_limit then return true, "upper" end
 return false, nil
end
```

## РАЗДЕЛ 18. ТОРГОВЫЙ КОНТЕКСТ FORTS

## 18.0. Расписание фондового рынка (TQBR)

 ★ Источник: moex.com/ru/stock-market/documents (официальные документы MOEX)
 ★ Данные актуальны на 30.09.2026. Проверять актуальность перед использованием.

### Параллельная таблица: TQBR (акции) vs SPBFUT (фьючерсы)

| Период | TQBR (акции) | SPBFUT (фьючерсы) |
|--------|-------------|-------------------|
| Техперерыв | 04:00–06:50 | 04:00–06:50 |
| Аукцион открытия (ликвидные) | 06:50–07:00 | 06:50–07:00 |
| Утренняя сессия | 07:00–09:00 (~101 бумага) | 07:00–09:00 |
| Аукцион открытия (остальные) | 09:00–09:10 | — |
| Основная сессия | 09:00–18:55 (все инструменты) | 09:00–19:00 |
| Аукцион закрытия | 18:55–19:00 (5 минут) | — |
| Фиксация РЦ | 19:00 (цена аукциона закрытия) | 19:00 (РЦ для MtM) |
| Вечерняя сессия | 19:00–23:50 (перечень акций) | 19:00–23:50 |
| Клиринг m-t-m | — | 23:50–00:30 |
| ДСВД (суббота) | 09:50–10:00 АО, 10:00–19:00 торги | 09:50–10:00 АО, 10:00–19:00 торги |

 ★ КЛЮЧЕВАЯ СВЯЗКА: цена закрытия TQBR (аукцион 18:55–19:00) = РЦ 19:00 для FORTS
 ★ Аукцион закрытия перенесён с 18:40–18:50 на 18:55–19:00 (с 23.03.2026)
 ★ Основная сессия TQBR заканчивается в 18:55, а не 19:00 (5 мин на аукцион закрытия)

### Аукцион открытия (TQBR)

| Параметр | Значение |
|----------|----------|
| Утренний (ликвидные) | 06:50–07:00 |
| Основной (остальные) | 09:00–09:10 |
| ДСВД | 09:50–10:00 |
| Алгоритм | Сбор заявок → цена максимального объёма → мэтчинг по единой цене |
| Случайное окончание | В последние 30 секунд (анти-манипуляция) |
| Ограничение дальности | ±10% от закрытия предыдущего дня |
| Типы заявок | Лимитные + рыночные |
| Неисполненные | Переносятся в торговый период |

### Аукцион закрытия (TQBR, с 23.03.2026)

| Параметр | Значение |
|----------|----------|
| Время | 18:55–19:00 (5 минут) |
| Call-фаза (сбор заявок) | 18:55:00–18:57:29 |
| Определение цены | 18:57:29 |
| Сделки по цене закрытия | 18:57:30–19:00 |
| Случайное окончание Call-фазы | Да (анти-манипуляция) |
| Статический диапазон | ±(0.5 × ставка рыночного риска), не более ±40% |
| Типы заявок в Call-фазе | Лимитные + рыночные + «лимитная/рыночная в аукцион» |
| Типы заявок в Фазе 2 | Только лимитные по цене аукциона закрытия |
| Цена закрытия = | Цена аукциона закрытия (официальная) |
| Назначение | Расчёт индексов, оценка СЧА, контроль маржинальных сделок, РЦ для FORTS |

### Планки (ценовые коридоры TQBR)

| Сессия | База для расчёта | Лимит | Расширяемость |
|--------|-----------------|-------|---------------|
| Утренняя | Закрытие предыдущего дня | 10% (акции), 5% (ОФЗ) | Нет |
| Основная | Закрытие предыдущего дня | 10–40% (по эшелону, устанавливает НКЦ) | Зависит (см. ниже) |
| Вечерняя | Закрытие текущего дня | 10% (все инструменты) | Нет (фиксированный) |
| ДСВД | Закрытие предыдущей основной | По решению биржи | Нет |

 Параметры в QUIK: PcH_Max (верхняя), PcH_Min (нижняя) — «Максимальная/минимальная возможная цена»

### Расширение планок в основной сессии

| Тип | Эшелон | Начальная планка | Расширяемость |
|-----|--------|-----------------|---------------|
| Расширяемые | 1-й (SBER, LKOH) | 10% | Да — биржа расширяет при касании |
| Нерасширяемые | 2-й, 3-й | 10%/20%/40% | Нет — фиксируются и не меняются |
| После 1-го дня в планке | Любой | — | Биржа может сузить до 10% |
| Асимметричные границы | Любой | — | Биржа может установить разные верх/низ |
| При отсутствии цены закрытия | — | — | Лимит считается от расчётной цены (решение биржи) |

### Дискретный аукцион

| Параметр | Значение |
|----------|----------|
| Триггер для IMOEX | Отклонение на 15% за 10 минут подряд |
| Триггер для акции | Отклонение на 20% за 10 минут подряд |
| Базовое значение (1-я серия) | Цена открытия сессии |
| Базовое значение (2-я серия) | Цена на момент начала 1-й серии ДА |
| Длительность серии | 30 минут = 3 аукциона по 10 минут |
| Максимум за сессию | 2 серии ДА |
| Типы заявок | Только лимитные (рыночные запрещены) |

### ДСВД (дополнительная сессия выходного дня)

| Параметр | Значение |
|----------|----------|
| Расписание | АО 09:50–10:00, торги 10:00–19:00 |
| Относится к | Следующему торговому дню (сделки субботы → T+1) |
| Инструменты (фондовый) | Ликвидные акции из перечня, БПИФы |
| Инструменты (срочный) | Все контракты, кроме опционов |
| Клиринг/расчёты | Не производятся в выходные |
| Планки | Не расширяются (при касании — торги на планке) |

## 18.1. Расписание торгов (Единая сессия с 23.03.2026)

 ★ Полное расписание ЕТС (с 14.07.2026) :

 06:50 — 07:00 МСК Аукцион открытия
 07:00 — 09:00 МСК Утренняя сессия
 09:00 — МСК Выставление МТ (маржинальных требований)
 09:00 — 14:00 МСК Основная сессия (часть 1)
 14:00 — МСК ★ Экспирация (онлайн, для части инструментов)
 14:00 — 17:30 МСК Основная сессия (часть 2)
 17:30 — МСК Исполнение МТ (довнести до 17:30)
 17:30 — 19:00 МСК Основная сессия (часть 3)
 19:00 — МСК Расчётная цена (РЦ) фиксируется + экспирация (19:00)
 19:00 — 23:50 МСК Вечерняя сессия
 23:50 — 00:30 МСК Клиринг m-t-m (mark-to-market)
 ~20:00 T+1 МСК Расчётная сессия — фактическое движение денег

 ★ ПРОМЕЖУТОЧНЫЙ КЛИРИНГ 14:00 ОТМЕНЁН (с 23.03.2026)
 ★ "УТРЕННЕГО КЛИРИНГА" НЕ СУЩЕСТВУЕТ
 ★ МТ — в 10:00 МСК (на уровне клиента) / 09:00 (на уровне УК)
 ★ Торги идут без остановок 07:00 — 23:50
 ★ ⚠ Расписание аукциона: основная страница MOEX — 06:50, FAQ — 08:50
 ★ ДСВД (суббота): 09:50–10:00 аукцион, 10:00–19:00 торги → относится к СЛЕДУЮЩЕМУ дню

ДСВД (суббота):
 Аукцион открытия: 09:50 — 10:00 МСК
 Торги: 10:00 — 19:00 МСК
 Клиринг: в понедельник (первый MtM 23:50)

 ★ МТ в ДСВД: если суббота — МТ в 10:00
 ★ ДСВД — НЕ каждая суббота! Даты публикуются в календаре MOEX.

Lua-функция msk_time():
```lua
local function msk_time()
 return os.time(os.date("!*t")) + 3 * 3600
end
```
★ Примечание : формула корректна — Россия не переходит на летнее время с 2014 года.
 Однако на некоторых сборках Lua под Windows os.date("!*t") может возвращать локальное
 время вместо UTC. Рекомендуется сверить результат с getInfoParam("SERVERTIME") при
 первом запуске. Если расхождение — использовать альтернативу:
 `tonumber(getInfoParam("SERVERTIME"))` или парсинг SERVERTIME через string.match.

Lua-функция is_trading_session():
```lua
-- Загрузка праздников из файла holidays.txt (даты YYYYMMDD, по одной на строку)
-- Файл берётся с календаря Мосбиржи: moex.com/s205
-- Вызывать load_holidays() в OnInit()
local holidays = {}
local function load_holidays(filepath)
-- [... код сокращён ...]
end

local function is_trading_session()

 -- Проверка праздников

 -- Runtime-валидация: если QUIK подключён и TRADEDATE не совпадает с
 -- текущей датой после 07:10 МСК — торгов нет (праздник/нерабочий день)

  -- Аукцион открытия: 06:50 с 14.07.2026, до этого — 07:00
-- [... код сокращён ...]
end
```

## 18.2. Механика клиринга

Ключевые параметры:
 SETTLEPRICE — расчётная цена текущего дня (РЦ 19:00, фиксируется в клиринге). В ISS history — ЗАПОЛНЕНО.
 SETTLEPRICEDAY — «теоретическая цена в дневном клиринге» — МЁРТВЫЙ параметр (null в ISS history).
   ПК 14:00 отменён с 23.03.2026, поле пустое. НЕ ИСПОЛЬЗОВАТЬ (грабля #199).
 CLPRICE — цена последнего клиринга (фиксированная до следующего MtM)

ВАЖНО: CLPRICE и SETTLEPRICE — РАЗНЫЕ параметры!
 - CLPRICE фиксируется в момент клиринга (23:50) и не меняется до следующего
 - SETTLEPRICE — РЦ 19:00, может обновляться в течение сессии до 23:50
 - SETTLEPRICEDAY — null в ISS history (грабля #199), не использовать
 - Для расчёта ВМ биржа использует CLPRICE как базу
 - Для дельты и маржи в скрипте → использовать CLPRICE с fallback на SETTLEPRICE
 - Для бэктеста через ISS → использовать SETTLEPRICE (заполнен), НЕ SETTLEPRICEDAY (null)

## 18.3. Методика ВМ (двухфазный клиринг НКЦ)

Биржа использует двухфазный клиринг:
 Фаза 1: m-t-m (mark-to-market) — пересчёт позиций по РЦ 19:00
 Фаза 2: Расчётная сессия — фактическое движение денег (на следующий день, ~20:00 МСК)

Три формулы ВМ:
 Новая позиция (открыта сегодня, не закрыта):
 ВМ = (РЦ_19:00 - Цена_сделки) × позиция
 Перенесённая позиция (открыта вчера+, не закрыта):
 ВМ = (РЦ_сегодня - РЦ_вчера) × позиция
 Закрытая позиция (сделка закрытия сегодня):
 ВМ = (Цена_закрытия - РЦ_пред) × позиция

Рублёвый пересчёт:
 ВМ_руб = ВМ_пункты / шаг_цены × стоимость_шага_цены

## 18.4. Расчётная цена (РЦ)

РЦ для MtM определяется в 19:00 МСК (фиксация цены закрытия).
Окно сэмплирования: 18:58:00–19:00:00 МСК.

## 18.5. ЕДП (Единый депозитарный счёт)

ЕДП — счёт, объединяющий позиции по всем брокерам.
В QUIK: getDepoEx — получение позиции по ЕДП.
Фьючерсы не торгуются через ЕДП — только через futures_client_holding.

## 18.6. Классы инструментов → см. раздел 26
★ Полная таблица классов — в разделе 26.

## 18.7. Сервисные функции → см. раздел 27
★ Полный список — в разделе 27.

## 18.8. bit.* функции (Lua 5.1) → см. раздел 11 и паттерн 17.17
★ Полный список bit.* функций — в разделе 11.

## РАЗДЕЛ 19. ГРАБЛИ (205 штук)

## Язык Lua (#1–20)

#1 nil + number → runtime error
#2 0 и "" — истина (не как C/Python)
#3 #t — длина только последовательного массива от 1
#4 string.format("%d", float_5.3) → ошибка в 5.3
#5 table.sort неустойчив (может менять порядок равных)
#6 Замыкания захватывают upvalues по ссылке, не по значению
#7 pcall ловит runtime, но не syntax errors
#8 math.floor(-1.5) = -2 (не -1!) — округление к -∞
#9 string.gsub возвращает 3 значения (нельзя в concat напрямую)
#10 tonumber("0x10") = nil в Lua 5.1 (нет hex)
#11 table.concat только для строк — числа нужно tostring
#12 math.random без math.randomseed — детерминирован
#13 Корутины не прерываются автоматически — только yield
#14 os.time(os.date("!*t")) — UTC, не локальное время
#15 setmetatable({}, {__gc=...}) — только в 5.3+
#16 goto/labels — только в 5.3+
#17 Integer overflow в 5.3 — остаётся integer (не auto-float)
#18 package.loaded кэширует require — dofile для перезагрузки
#19 xpcall handler получает traceback, а не ошибку напрямую
#20 string.find с pattern по умолчанию (не plain!) — экранировать %

## QLua API (#21–38)

#21 col в SetCell — 0-индексация, row — от InsertRow
#22 GetTableSize возвращает 2 числа, не таблицу
#23 AllocTable может вернуть nil — проверка обязательна
#24 CreateWindow может провалиться — ретрай
#25 SetCell для DOUBLE — нужно числовое значение (5-й аргумент)
#26 OnQTableClose vs OnClose — OnClose deprecated
#27 isConnected() — true/false, не 1/0
#28 sendTransaction возвращает строку "OK", не true
#29 getParamEx может вернуть nil — проверка result == 1
#30 OnDisconnected/OnConnected — без аргументов
#31 OnStop должен вернуть число (мс)
#32 main() — отдельный поток, callbacks — в главном
#33 OnCleanUp — не гарантирует выполнение
#34 Clear(t_id) — очищает таблицу, но не уничтожает
#35 SetColor — RGB(), не строка "#FF0000"
#36 getQuoteLevel2 может вернуть nil/""/table — проверка типа
#37 ParamRequest для STEPPRICE — не заказан → nil
#38 CreateDataSource 4-й параметр — может вернуть nil без него

## Файлы (#39–50)

#39 io.open в ANSI — кодировка Windows-1251
#40 file:write(table.concat{...}) — числа нужно tostring
#41 Не закрытый файл — утечка, особенно на Windows
#42 os.date("%Y%m%d") — локальное время, не МСК
#43 getScriptPath() может вернуть nil в индикаторах
#44 Чтение/запись файла в callback — опасно (главный поток)
#45 Append mode "a" — добавляет, не перезаписывает
#46 CSV с BOM — QUIK может не прочитать
#47 Пути с русскими буквами — могут не работать
#48 Временный файл — не забывать удалять
#49 Чтение больших файлов — построчно (io.lines)
#50 Файл лога — открывать/закрывать на каждую запись

## FORTS (#51–62)

#51 CLPRICE ≠ SETTLEPRICE — разные параметры
#52 CLPRICE фиксируется в клиринге, SETTLEPRICE обновляется
#53 total_net vs totalnet — разные имена в версиях QUIK
#54 futures_client_holding — индексация с 0
#55 pos ≠ total_net — pos может включать обе стороны
#56 varmargin — накопленная ВМ, не текущая
#57 MATDATE — формат YYYYMMDD (строка/число)
#58 exp_weight — параметр, не факт
#59 ДСВД — не каждая суббота
#60 Промежуточный клиринг 14:00 отменён (с 23.03.2026)
#61 РЦ фиксируется в 19:00, не в 23:50
#62 ВМ клиринга = (РЦ − база) × позиция, где база = цена сделки (новая) или РЦ вчера (перенесённая). Текущая цена после 19:00 в ВМ клиринга НЕ участвует
#197 CLPRICE (TQBR, акция) vs SETTLEPRICE (SPBFUT, фьючерс) в формуле гэпа: CLPRICE не несёт контанго, фьючерс несёт ~3-4% → B завышен → знак инвертируется. Использовать SETTLEPRICE фьючерса (раздел 44.6, v52)
#198 SETTLEPRICE в QUIK может обновляться на вечерней сессии (грабля #52). Для реал-тайм — сохранять снимок SETTLEPRICE в 19:00 в переменную, не читать в 23:50. Для бэктеста через ISS — SETTLEPRICE в history уже зафиксирован, обновляться не может (раздел 44.9, v54). ВНИМАНИЕ: в v53 рекомендовалось использовать SETTLEPRICEDAY — ОШИБКА, это поле null (грабля #199). Использовать SETTLEPRICE.
#199 SETTLEPRICEDAY — МЁТВЫЙ параметр в ISS history (null для всех дат). Описание: «Теоретическая цена в дневном клиринге» — поле из отменённого промежуточного клиринга 14:00 (отменён с 23.03.2026). В Go-библиотеке github.com/Ruvad39/go-moex-iss определён в структуре OptionHistory (для опционов), для фьючерсов всегда null. Использовать SETTLEPRICE (раздел 44.9, v54).
#200 ISS securities endpoint (/iss/engines/futures/markets/forts/securities) не возвращает истёкшие контракты — только активные. Для rolling-бэктеста нужно генерировать secid истёкших контрактов: префикс (SR, GZ, LK, MX...) + месяц (H/M/U/Z) + год. Затем загружать историю через ISS history endpoint (раздел 44.10, v54).

#201 15-min ISS candles — flat OHLC: 57.5% строк имеют одинаковые open/high/low/close (нет диапазона). Причина: ISS 15-min aggregation для ранних утренних свечей возвращает обобщённую свечу без реального диапазона. В 48 случаях 15-min HIGH ниже 1-min HIGH — математически невозможно, если 15-мин окно включает 1-мин. Решение: агрегировать из 1-мин свечей вручную, НЕ использовать ISS 15-min endpoint напрямую (раздел 44.11, v55).
#202 Порог |B| 0.3 — шум: при |B| >= 0.3 win rate V51 падает до 53.7%, avg P&L = -0.07%, cumulative = -6.32%. Лонги при 0.3 уже не работают (avg ~0, win rate < 50%). Реальная граница сигнала — |B| >= 0.5 (30 сделок, win rate 66.7%, profit factor 4.63). Использовать |B| >= 0.5 для торговли, |B| >= 0.3 только для анализа (раздел 44.11, v55).
#203 Выход по close 15 минут убивает прибыль: mean-reversion происходит внутри 15 минут, но к закрытию разворачивается обратно. V51 по close = -0.65% cumulative, по TP (best price) = +5.93% net. Выходить нужно внутри 15 минут при достижении РЦ, не ждать close (раздел 44.11, v55).
#204 Асимметрия лонг/шорт — структурная: утренний гэп на российском рынке асимметричен. Падение вечером → отскок утром (лонги работают). Рост вечером → продолжение роста утром (шорты по close не работают, 23.5% win rate). Но шорты по TP внутри 15 мин работают (82.4% favourable). Проблема не в направлении, а в точке выхода (раздел 44.11, v55).
#205 Смена режима по контрактам: 77% сильных сделок (|B| >= 0.5) из MXU6 (июнь-сентябрь). MXH6 (янв-март) не дал ни одной сделки с |B| >= 0.5. Исторический basеline: MXH6/MXM6 — low положительный (бычий режим), MXU6 — low резко отрицательный -526/-708 pts (медвежий). Результаты бэктеста могут быть артефактом одного волатильного периода (раздел 44.11, v55).

## Позиции и подписки (#63–75)

#63 Forward reference локальных функций — краш
#64 ParamRequest для STEPPRICE — не заказан → nil
#65 total_net vs totalnet — разные имена
#66 Двойной ParamRequest — параметр в PARAMS и отдельно
#67 CancelParamRequest работает только с getParamEx2 (не getParamEx!)
#68 SetUpdateCallback сломан в некоторых версиях QUIK
#69 getQuoteLevel2 nil/""/table — type() проверка обязательна
#70 CreateDataSource 4-й параметр — пустая строка "" для безопасности
#71 DS:Close() — обязательно, иначе утечка
#72 PrintDbgStr — отладочный вывод в лог QUIK
#73 OnAllTrade flags — bit.band для определения направления
#74 OnFuturesClientHolding — альтернатива перебору
#75 getFuturesHolding nil при клиринге — fallback на getItem

## Транзакции и QTable (#76–79)

#76 ACCOUNT обязателен в sendTransaction
#77 CalcBuySell — оценка ГО для сделки
#78 OnTransReply — ответ на транзакцию
#79 SetWindowPos, Highlight, GetCell, SetSelectedRow — доп. QTable

## ВМ и РЦ (#80–89)

#80 ВМ клиринга = (РЦ − цена_сделки) × позиция — цена сделки участвует, но текущая цена после 19:00 НЕ участвует
#81 Индикативная ВМ ≠ итоговая ВМ — расхождение после 19:00
#82 МТ (маржинальное требование) — в 10:00 МСК, не 09:00
#83 МТ в ДСВД — если суббота, МТ в 10:00
#84 НКЦ пересчитывает риск-параметры ежедневно (в клиринге m-t-m + внутри дня при auto-shift)
#85 Комиссия списывается единоразово (в клиринге), не при сделке
#86 Заявки ДСВД снимаются в конце сессии (19:00)
#87 Поставочные фьючерсы в клиринге — поставка базисного актива
#88 Стоп-лоссы без промежуточного клиринга — нет «перезагрузки»
#89 Период ВМ — 19:00→19:00, а не 23:50→23:50

## Битовые операции и callbacks (#90–95)

#90 bit.* функции — bit.band, bit.bor в Lua 5.1
#91 VM-парадокс: ВМ клиринга = (РЦ − база) × поз, не (тек − база) × поз. РЦ заменила текущую цену в клиринговой части
#92 VM split: ВМ_клиринга + ВМ_завтрашнего_дня
#93 Подписка на стакан асинхронна — OnQuote может прийти позже
#94 Отписка от стакана с ретраями — может не сработать с 1-й попытки
#95 Callback только sinsert — не InsertRow в OnQuote/OnAllTrade

## Пассивные заявки и ВМ-формулы (#96–102)

#96 Пассивные заявки — "Условие исполнения" = "Только пассивная"
#97 ВМ для новой позиции = (РЦ - цена_сделки) × позиция
#98 ВМ для перенесённой = (РЦ_сегодня - РЦ_вчера) × позиция
#99 ВМ для закрытой = (цена_закрытия - РЦ_пред) × позиция
#100 Прибыль после 19:00 делится: ВМ_клиринга = (РЦ − база) × поз зачислится, (тек − РЦ) × поз «зависнет» до завтра
#101 Убыток после 19:00 не списывается в этом клиринге — перенос на завтра
#102 Закрытие до 23:50 — ВМ от цены сделки, а не от РЦ

## ГО (#103–120)

#103 getParamEx vs getParamEx2 — CancelParamRequest работает только с getParamEx2
#104 Фантомная маржа — плечо, не прибыль. Списывается на следующий клиринг
#105 Мелкие позиции — фантом слишком мал. Нужно ≥10 контрактов + разрыв РЦ >0.5%
#106 Неправильное направление = нет фантома. Лонг при LAST > CLPRICE → фантом отрицательный
#107 RC-сэмплирование должно идти до 19:00:00 (было до 18:58:55 — теряли 65 сек)
#108 getParamEx2 при ParamRequest — использовать getParamEx2 везде при ParamRequest/CancelParamRequest
#109 BUYDEPO = ГО лонга, SELLDEPO = ГО шорта. Документация QUIK перепутана. Имя = смысл
#110 Формула ВМ ≠ формула ГО. ГО = SPAN-модель (сценарии), ВМ = простой P&L
#111 getParamEx2 BUYDEPO возвращает 0 при первом вызове — цикл с sleep(100), до 100 попыток
#112 Рыночная заявка блокирует 1.5× ГО — использовать лимитные для экономии
#113 ГО может вырасти внутри дня (auto-shift) — MR_new = MR_curr + 0.5 × FutShift × MR1
#114 Брокерское ГО ≠ биржевое — КПУР/КСУР/КНУР/КОУР, QUIK показывает биржевое
#115 4 категории риска (КНУР, КСУР, КОУР, КПУР), не 3. КОУР — «особый уровень»
#116 3 уровня ставок MR1/MR2/MR3 + лимиты концентрации LK1/LK2. Больше позиция → выше ГО
#117 BA_coeff_go — коэффициент-множитель ГО per БА (участник клиринга). По умолчанию = 1
#118 NCI(БА) — правило исполняющегося фьючерса: Полунеттинг перед экспирацией, ГО растёт
#119 Запрет скидки по фьючерсам — per-client: лонг ниже РЦ → цена=РЦ, шорт выше РЦ → цена=РЦ
#120 ВМ по закрытию опционов с валютным риском → рост ГО на |ВМ| × R

## Сессии и клиринг (#121–124)

#121 Вечерняя сессия = текущий торговый день (с 23.03.2026) — не следующий день
#122 Исполнение обязательств T+1 в 20:00 — движение денег, не торговля. ВМ доступна через MTM-регистры
#123 Индикативные ставки риска НКЦ (с 07.04.2026) — 2-дневный 99% VaR, не путать с биржевым ГО
#124 getParamEx (архив, медленно) vs getParamEx2 (текущая таблица, быстро) — архитектурное отличие

## ЕТС и MTM (#125–130)

#125 MTM-регистры — фантомная ВМ записывается в 23:50, доступна через money_amount УТРОМ, не в 20:00
#126 НПР1 / НПР2 — две формулы претрейд-проверки: НПР1 = money_amount + rmt_vm – rmt_im
#127 actual_amount ≠ money_amount — первая для вывода, вторая для ГО (с MTM-регистрами)
#128 vm_reserve — резерв ВМ при экспирации. ГО свободен, деньги в резерве до 20:00
#129 МТ в 10:00 — маржинальные требования ≠ ГО. Довнести до 17:30
#130 «Вывод в размере расчётной» — доступен в ЕТС. Величина требований известна утром

## Статические параметры и Единый пул (#131–134)

#131 Два документа НКЦ, не один: Принципы (ЧТО считать) + Методика (КАК). Оба обновляются независимо
#132 Обеспечение в валюте дешевле номинала: дисконт = MR1. 1000 USD при MR1=15% → 850 USD-эквивалента
#133 Принудительное закрытие при дефолте ЦК: 5-уровневая защита, распределение убытков по позициям
#134 CF (дивиденды) влияет на ГО: перед дивидендной датой РЦ и ГО пересчитываются. Скрипт должен алертить

## Новые инструменты и экспирация (#135–138)

#135 Экспирация в 14:00 — онлайн, без остановки торгов. Не только 19:00
#136 Онлайн-исполнение: ГО освобождается за минуты, финрезультат в той же сессии
#137 20 вечных фьючерсов (сентябрь 2026): AMDF, TSLAF, APPF, COINF — фиксинги Мосбиржи, K1=0%, K2=0.35%
#138 KEYRATE (KK): БА = индекс ключевой ставки. Экспирация в 19:00 в дни заседаний ЦБ. Старт 29.09.2026

## Обособленные клиенты и дефолт (#139–142)

#139 Инвалюта = «иное обеспечение» (балансовый счёт 47405), не индивидуальное. Меньшая защита при дефолте УК
#140 Обособленный клиент (Portability) — переход к другому УК за 2 дня без согласия базового УК
#141 Обособленная БФ — изоляция: обеспечение одной БФ нельзя использовать для закрытия позиций другой
#142 Выходные торги (ДСВД) относятся к СЛЕДУЮЩЕМУ дню — исключение из ЕТС-правила «вечерняя=текущий день»

## Формулы отчётов и экспирация (#143–148)

#143 free = amount_end_mtm – go + nov. nov (NetOptionValue) добавляется к свободным средствам. Скрипт без nov занижает остаток
#144 ВМ для вечного фьючерса ≠ простая переоценка. Фандинг и дивидендная поправка корректируют ВМ
#145 Дивидендная поправка IMOEXF — только по позиции на пред. клиринг (23:50), не по новым сделкам в течение дня
#146 Экспирация: расчётные — онлайн (14:00/19:00), поставочные — в клиринге. Скрипт экспирации должен различать тип
#147 Поля isrepo, account_forts, limit, pr_setll, pr_settl_r, spot, base — удалены из отчётов. Старые парсеры сломаются
#148 Параметры K1/K2 фандинга менялись неоднократно — дата «12.10.2026» НЕ подтверждается источниками

## Исправления паттернов (#149–150)

#149 is_trading_session не учитывает праздники — проверка wday недостаточна. 23 февраля, 8 марта и т.д. — торги не идут, но функция вернёт true. Решение: файл holidays.txt + runtime-валидация TRADEDATE
#150 getItem("money_limits", 0) — индекс 0 возвращает первую запись, но лимитов может быть несколько (рубли, валюта, разные типы). Нужен перебор с фильтром по currcode=="SUR" и limit_kind==0

## Актуализация данных и новые знания (#151–155)

#151 SPECTRA 9.6 — production-релиз 22.06.2026 подтверждён календарём релизов Мосбиржи . Фичи 9.6 можно использовать в production
#152 IMOEXF фандинг — уточнённые данные Мосбиржи. Скрипты расчёта ожидаемого фандинга IMOEXF должны использовать актуальные данные с moex.com/ru/derivatives
#153 Перенос основной сессии на 09:00 (с 14.09.2026) — расписание изменилось. Утренняя сессия теперь 06:50–09:00 (была 06:50–09:50). Фандинг по некоторым контрактам также сдвинут на 09:00. Скрипты с жёстко зашитым временем 10:00 — сломаются
#154 Выходные без торгов в 2026: 22–23 октября, 5–6 декабря, 31 декабря — holidays.txt должен включать эти даты. Не путать с ДСВД (субботние торги)
#155 РЕПО в специализированной валюте (с 06.07.2026) — новый режим, влияет на расчёт обеспечения в Едином пуле. Скрипты расчёта ГО должны учитывать возможное изменение доступного обеспечения

## Арбитражные стратегии (#156–160)

#156 Фандинг может сменить знак — конструкция long spot + short futures становится убыточной. Скрипт должен алертить при смене знака (паттерн 17.46). Решение: мониторинг FUNDING_RATE, автоматическое закрытие при смене знака
#157 Базис (отклонение цены ВФ от БА) не равен 0 — торговать отклонение от справедливого уровня, а не от нуля. Формула справедливого спреда (паттерн 17.47)
#158 Ликвидность дальних контрактов — проскальзывание может съесть весь результат арбитража. Проверять глубину стакана обеих ног перед входом
#159 IMOEXF нельзя купить напрямую — tracking error корзины/фонда. Использовать ETF (TMOS, SBMX) или фьючерс IMOEX, учитывать расхождение
#160 15% фандинга ≠ 15% доходности — считать NET (за вычетом стоимости капитала, комиссий, спреда, проскальзывания), не GROSS. Формула (паттерн 17.45)

## KEYRATE (#161-164)

#161 KEYRATE направление: цена фьючерса = ожидаемая ставка ПРЯМО (не «100 минус ставка»). 13.86 = 13.86%, а не 86.14%. Распространённая ошибка в статьях. Цена = ставка напрямую (moex.com/a8141)
#162 KEYRATE внеплановое заседание ЦБ — досрочного исполнения НЕТ. Индекс пересчитывается на следующий рабочий день. Скрипт не должен ждать экспирацию
#163 ГО KEYRATE ~3 000 ₽ — не путать с ГО обычных фьючерсов. Плечо ~4.7×, при движении 0.25 п.п. = 250 ₽/контракт
#164 Лимиты цен KEYRATE: при достижении дневных лимитов торги останавливаются. Скрипт должен проверять лимиты (актуальные: moex.com/ru/derivatives)

## Управление заявками (#165–169) — добавлено в v39

#165 ORDER_KEY — биржевый номер заявки (из OnOrder), не TRANS_ID (ваш внутренний). Для отмены использовать ORDER_KEY
#166 MOVE_ORDER возвращает "OK" даже если заявка уже исполнена — проверять статус через order_tracker перед перемещением
#167 OnOrder может прийти несколько раз для одной заявки (активна → частично исполнена → исполнена) — обрабатывать по flags
#168 OnTransReply приходит ДО OnOrder — не считать заявку "активной" по OnTransReply, ждать OnOrder
#169 bit.band для разбора flags в Lua 5.1; в Lua 5.3 — order.flags & 1 (или to_int + bit32 fallback)

## Хеджевый стоп-лосс (#170–173)

#170 Двойное ГО — полунеттинг на уровне раздела регистра. Два субсчёта = два раздела регистра. Считать на двойное ГО, пока брокер не подтвердит сальдирование
#171 STOP_ORDER с лимитной ценой не исполнится при гэпе мимо limit_price. Альтернатива — рыночная заявка по исполнении (1.5× ГО, грабля #112)
#172 Хедж после 19:00 — ВМ клиринга = (РЦ − цена_сделки) × поз, не (тек − цена_сделки) × поз. Скрипт врёт. Использовать vm_split()
#173 ACCOUNT = счёт 2 в STOP_ORDER. Если указать счёт 1 — неттинг закроет основную позицию, налоговое событие

#174 OnAllTrade.flags через band() — НЕ bit.band. bit.band без fallback в Lua 5.3 (грабля #169). Использовать band() из раздела 11
#175 Сброс кумулятивной дельты в клиринг 23:50 — иначе копится мусор за предыдущий период. reset_delta() в клиринг
#176 getQuoteLevel2 возвращает объём в лотах, не в рублях. Для рублёвого эквивалента × price × step_price
#177 Айсберги в стакане — QUIK показывает только видимую часть. Стена может быть больше, чем видно
#178 getParamEx2 OPENPOSITION ≠ ОИ в некоторых версиях QUIK. Проверять NUMCONTRACTS как fallback
#179 ОИ обновляется с задержкой — внутри дня NUMCONTRACTS может отставать. Не использовать для скальпинга
#180 bit.band в 17.17 без fallback — использовать band() из раздела 11 (грабля #169). 17.17a уже исправлена, 17.17 — переписана в v46
#181 Сентимент без объёма — 100 сделок по 1 лоту ≠ 1 сделка на 100 лотов. WVTS (volume-weighted) решает (паттерн 17.17, переписан в v46)
#182 Скорость ленты без порога — WVTS > 0.8 на тихом рынке = ложный сигнал. Фильтр: trade_speed ≥ 3 сделок/сек для подтверждения прорыва (паттерн 17.17e)
#183 Timeframe mismatch: WVTS (секунды) vs OI (часы) — нельзя напрямую комбинировать. Иерархия: OI = фильтр/контекст, WVTS = триггер. Не смешивать горизонты (паттерн 17.17f)
#184 OI delay в стратегии: OI обновляется с задержкой 5-15 мин. К моменту сигнала sentiment OI может отражать ситуацию 10 минут назад. Не использовать OI как entry trigger, только как context filter. Лента (OnAllTrade) приоритетнее — large_trade_flow заменяет ОИ в реал-тайме (паттерн 17.17i)
#185 Sentiment reversal без exit: WVTS > 0.7 → открыли long. WVTS упал до 0.5, но цена не упала. Если выходить только по WVTS, можно получить холдый сет. Нужен подтверждающий exit: delta divergence или OI unwinding (паттерн 17.17f exit overlay)
#186 Position sizing без strength: одинаковый объём на weak и strong signal = перериск на слабых сигналах. Scale by strength: 1/3, 2/3, full (паттерн 17.17g)
#187 Large trade threshold без адаптации: 50 лотов для RIM5 и для SiZ5 — разные весовые категории. Нужен динамический порог: медиана объёма × N (паттерн 17.17i)
#188 delta_velocity на тонком рынке: 2 сделки за 10 секунд дадут шум. Фильтр: минимум N сделок в окне, иначе return 0 (паттерн 17.17h)
#189 vwap_spread без учёта спреда: на инструменте со спредом 5 тиков vwap_spread 2 тика — это шум, не сигнал. Нормировать на спред (паттерн 17.17j)

## TQBR / фондовый рынок / IMOEX (#190-196)

#190 Расписание TQBR ≠ FORTS: основная сессия акций заканчивается в 18:55, а фьючерсов в 19:00. Аукцион закрытия 18:55–19:00 — только акции, фьючерсы торгуются
#191 Планки TQBR: база для утренней/основной = закрытие ПРЕДЫДУЩЕГО дня, для вечерней = закрытие ТЕКУЩЕГО дня. Разные базы — разные планки
#192 Нерасширяемые планки (2-й/3-й эшелон): фиксируются и не меняются в течение сессии. Скрипт, ждущий расширения при касании, зависнет
#193 Дискретный аукцион: триггер IMOEX 15% / акция 20% за 10 минут. Во время ДА — только лимитные заявки. Скрипт, отправляющий рыночные, получит отказ
#194 Аукцион открытия: ограничение ±10% от закрытия предыдущего дня. Заявки дальше 10% не принимаются. Скрипт, ставящий лимиты шире, получит отказ
#195 Call-фаза аукциона закрытия: 18:55:00–18:57:29 — сбор, 18:57:30–19:00 — сделки по цене аукциона. В Фазе 2 — только снятие/модификация, новых заявок нет
#196 Перечни ликвидных бумаг для утренней/вечерней сессий публикуются отдельным решением биржи. Не все акции TQBR торгуются на вечерней сессии

## РАЗДЕЛ 20. ЧЕКЛИСТ ПЕРЕД ЗАПУСКОМ (158 пунктов)

## Язык и совместимость
1. Проверка версии Lua (5.1 vs 5.3) через _VERSION
2. to_int() для 5.1/5.3 совместимости
3. bit.* для Lua 5.1, << >> для 5.3
4. math.floor(-1.5) = -2 (не -1) — округление к -∞

## Таблицы
5. AllocTable() — проверка на nil
6. AddColumn — проверка возврата
7. CreateWindow — ретрай
8. SetCell: числовое значение для DOUBLE
9. GetTableSize: 2 числа, не таблицу
10. Clear vs DestroyTable — не путать
11. SetColor: RGB(), не строка

## Подписки
12. ParamRequest для всех нужных параметров
13. CancelParamRequest при остановке/удалении
14. getParamEx2 вместо getParamEx (грабля #103/#108)
15. Пауза 2000 мс после ParamRequest
16. Ретрай getParamEx2 при нулевом значении

## Время и сессии
17. msk_time() — UTC + 3, не локальное время
18. is_trading_session() — проверка ДСВД, аукциона
19. Клиринг 23:50–00:30 — не торговать
20. МТ в 10:00 МСК (не 09:00)
21. МТ в ДСВД — если суббота, в 10:00
22. ГО обновляется ежедневно в клиринге + auto-shift внутри дня

## Фильтры
23. is_expired — MATDATE <= today
24. is_perpetual — PERP/EVERGREEN или MATDATE > 50000
25. has_min_trades — NUMTRADES > порога

## Данные
26. CLPRICE с fallback на SETTLEPRICE
27. STEPPRICE через отдельный getParamEx2
28. total_net or totalnet — fallback
29. getFuturesHolding с fallback на getItem
30. getParamEx2 для всех параметров при ParamRequest

## Позиции
31. futures_client_holding — индексация с 0
32. total_net — чистая позиция (не pos)
33. getFuturesHolding nil при клиринге — fallback
34. OnFuturesClientHolding — callback альтернатива

## РЦ-сэмплирование
35. Окно 18:58:00–19:00:00 МСК
36. Adaptive sleep (1000 мс) в окне сэмплирования
37. median3 для двухуровневой медианы
38. Fallback (bid+ask)/2 при отсутствии last

## Архитектура
39. pcall вокруг всех опасных вызовов
40. periodic collectgarbage каждые 5 минут
41. OnCleanUp — отмена подписок
42. is_recreating — флаг при пересоздании таблицы

## Клиринг и ВМ
43. ВМ по РЦ 19:00 для незакрытых позиций
44. Индикативная ВМ ≠ итоговая ВМ
45. Стоп-лоссы — без клиринга нет «перезагрузки»
46. Период ВМ — 19:00→19:00
47. Закрытие до 23:50 — ВМ от цены сделки
48. VM split: ВМ_клиринга + ВМ_завтра

## Транзакции
49. ACCOUNT обязателен в sendTransaction
50. Пассивные заявки — "Условие исполнения"
51. OnTransReply — обработка ответа

## Стакан
52. Subscribe — подписка на стакан
53. Флаг в OnQuote — проверка типа getQuoteLevel2
54. Чтение стакана в main, не в callback

## Фантом
55. PHANTOM_LEVERAGE = floor(|RUB_MARGIN| / min(BUYDEPO, SELLDEPO))
56. Сортировка по фантомному плечу
57. Фантомная ВМ — плечо, не прибыль

## ГО
58. BUYDEPO = ГО лонга, SELLDEPO = ГО шорта (имя = смысл)
59. Формула ВМ ≠ формула ГО (ГО = SPAN, ВМ = P&L)
60. getParamEx2 BUYDEPO с ретраем (может вернуть 0)

## ЕТС и расписание
61. Вечерняя сессия относится к текущему торговому дню (с 23.03.2026)
62. Исполнение обязательств по ВМ — 20:00 T+1, не в клиринге
63. Индикативные ставки риска НКЦ — 2-дневный 99% VaR (с 07.04.2026)
64. getParamEx (архив, медленно) vs getParamEx2 (текущая таблица, быстро)

## MTM-регистры и стратегия S2
65. MTM-регистры — фантомная ВМ в money_amount, доступна для ГО утром
66. НПР1 = money_amount + rmt_vm – rmt_im — претрейд-проверка с фантомом
67. actual_amount ≠ money_amount — первая для вывода, вторая для ГО
68. vm_reserve — резерв ВМ при экспирации, деньги до 20:00
69. МТ в 10:00 T+1 — маржинальные требования ≠ ГО, довнести до 17:30
70. «Вывод в размере расчётной» — доступен в ЕТС

## Статические параметры и Единый пул
71. Два документа НКЦ: Принципы (ЧТО) + Методика (КАК) — проверять обе версии
72. Обеспечение в валюте дешевле номинала: дисконт = MR1
73. 5-уровневая защита ЦК — при дефолте возможно принудительное закрытие
74. CF (дивиденды) влияет на ГО — перед дивидендной датой РЦ пересчитывается

## Новые инструменты и экспирация

75. Экспирация в 14:00 — проверять время экспирации (14:00 или 19:00) по инструменту
76. Онлайн-исполнение: ГО освобождается за минуты — не ждать клиринга
77. 20 вечных фьючерсов: фиксинги Мосбиржи, K1=0%, K2=0.35% — универсальный фильтр
78. KEYRATE (KK): экспирация в дни заседаний ЦБ — проверять календарь ЦБ
79. Криптовечные фьючерсы: только квалифицированные инвесторы
80. Утренний час 09:00–10:00 — расширенная сессия, HFT-активность

## Обособленные клиенты и дефолт

81. Инвалюта = «иное обеспечение» — меньшая защита при дефолте УК
82. Обособленный клиент может уйти без согласия брокера — Portability
83. Обособленная БФ — изоляция от кросс-дефолта внутри одного УК
84. Выходные торги → следующий день (исключение из ЕТС)

## Формулы отчётов и исправления

85. free = amount_end_mtm – go + nov — nov (NetOptionValue) обязателен
86. ВМ вечного фьючерса: Переоценка − Фандинг×Лот×sign(pos) + Дивид.поправка×Лот×sign(pos)
87. Дивидендная поправка — только по позиции на пред. клиринг, не по новым сделкам
88. Экспирация: различать тип — расчётные (онлайн), поставочные (клиринг)
89. Удалённые поля отчётов: isrepo, account_forts — обновить парсеры
90. Параметры K1/K2 — проверять актуальные значения, не полагаться на старые даты

## Исправления паттернов
91. is_trading_session — проверять праздники через holidays.txt + runtime-валидацию TRADEDATE
92. get_money_amount — перебор money_limits с фильтром (currcode=SUR, limit_kind=0), не getItem(0)

## Актуализация данных
93. SPECTRA 9.6 — production 22.06.2026 подтверждён, фичи доступны
94. IMOEXF фандинг — использовать ~14.1%, а не ~12%
95. Расписание 09:00 (с 14.09.2026) — обновить is_trading_session, проверять время начала основной сессии
96. Выходные без торгов 2026: 22–23 октября, 5–6 декабря, 31 декабря — добавить в holidays.txt
97. РЕПО в специализированной валюте (с 06.07.2026) — учитывать при расчёте обеспечения
98. Вечных фьючерсов 20+ (сентябрь 2026, количество растёт) — не хардкодить список, использовать FUNDING_RATE

## Арбитражные стратегии
99. Проверять знак фандинга перед входом в арбитраж — если отрицательный, конструкция убыточна
100. Считать NET доходность (за вычетом стоимости капитала, комиссий, спреда, проскальзывания), не GROSS
101. Проверять ликвидность обеих ног арбитража (срочный + вечный контракт) перед входом
102. Учитывать tracking error IMOEXF (нельзя купить индекс напрямую, нужен ETF/корзина)
103. Проверять справедливый спред (формула 17.47) перед входом в арбитраж срочный vs вечный
104. Backtesting арбитражных стратегий — учитывать комиссии, спред, проскальзывание, смену знака фандинга

## KEYRATE
105. KEYRATE: цена = ставка напрямую, НЕ «100 минус ставка» — проверить логику скрипта
106. KEYRATE: календарь заседаний ЦБ определяет дату экспирации — проверять перед торговлей
107. KEYRATE: формула ВМ = (РЦ − Ц) × 1000 ₽/пункт — скрипт должен использовать W/R = 1000
108. KEYRATE: ГО ~3 000 ₽ на LK1, ~6 700 ₽ с категорией — учитывать при расчёте свободных средств
109. KEYRATE: направление — рост ставки → покупка, снижение → продажа
110. KEYRATE: лимиты цен — проверять перед постановкой стопов (актуальные: moex.com/ru/derivatives)
111. KEYRATE: комиссии — 2,28 ₽ регистрация + 0,76 ₽ адресная + 0,76 ₽ клиринг — учитывать в NET

## Управление заявками — добавлено в v39

112. cancel_order: ORDER_KEY из OnOrder, не TRANS_ID (грабля #165)
113. move_order: проверять статус заявки перед перемещением (грабля #166)
114. OnOrder: обрабатывать по flags, не по факту вызова (грабля #167)
115. OnTransReply приходит ДО OnOrder — не считать активной по OnTransReply (грабля #168)
116. bit.band для flags в 5.1, & для 5.3 — универсальный разбор (грабля #169)
117. Реестр active_orders: обновлять в OnOrder, читать из main()
118. Отмена всех заявок при остановке скрипта (KILL_ALL_ORDERS)
119. Проверка has_active_order(sec) перед новой заявкой — не плодить дубли

## Хеджевый стоп-лосс
120. STOP_ORDER (не NEW_ORDER) — ACTION="STOP_ORDER" с STOPPRICE (триггер) и PRICE (лимитная цена исполнения)
121. Двойное ГО: go_main + go_hedge через get_go_with_retry + calc_npr1 перед установкой стопа. Запас 20% на auto-shift
122. VM-парадокс после 19:00: использовать vm_split() для корректного учёта ВМ клиринга
123. ACCOUNT = счёт 2 в STOP_ORDER — не счёт 1! Иначе неттинг закроет основную позицию
124. Recovery при перезапуске: перечитать позиции (getFuturesHolding), активные заявки (OnOrder), восстановить state
125. Reconnect: при OnDisconnected — остановить торговлю, при OnConnected — переподписаться, перечитать позиции
126. Double-send guard: in_flight флаг + таймаут перед sendTransaction — не отправить дубль
127. Risk-per-trade: qty = risk_amount / (stop_points × step_price) — расчёт объёма от допустимого убытка
128. order_flow_delta: band() для разбора flags (грабля #174), reset_delta() в клиринг (грабля #175)
129. large_order_detector: стены в лотах (грабля #176), айсберги невидимы (грабля #177)
130. oi_pressure: NUMCONTRACTS + OPENPOSITION fallback (грабля #178), ОИ с задержкой (грабля #179)
131. Дивергенция дельта/цена — разворотный сигнал: цена растёт, дельта падает → разворот вниз
132. ОИ + цена: рост ОИ + рост цены = новые лонги, рост ОИ + падение = новые шорты, снижение ОИ = затухание
133. sentiment (WVTS): band() вместо bit.band (грабля #180), volume-weighted (грабля #181), кольцевой буфер
134. Дивергенция WVTS/delta: сентимент бычий + дельта медвежья = smart money selling (паттерн 17.17d)
135. trade_speed: скорость ленты как фильтр — WVTS > 0.7 + speed ≥ 3 = прорыв, WVTS > 0.7 + speed < 3 = noise (грабля #182)
136. signal_aggregator: 5+ сигналов в один verdict (action + strength) (паттерн 17.17f)
137. OI = фильтр, WVTS = триггер, delta = exit — не смешивать горизонты (грабля #183)
138. Position sizing по strength: weak = 1/3, strong = 2/3, strongest = full (грабля #186, паттерн 17.17g)
139. Временные фильтры: нет входа 18:58-19:02, 23:45-23:55, первые 5 мин сессии (паттерн 17.17k)
140. Exit по WVTS reversal + delta divergence + OI unwinding — не по одному сигналу (грабля #185)
141. delta_velocity: ускорение дельты из ленты — лидирующий сигнал (грабля #188, паттерн 17.17h)
142. large_trade_flow: крупные сделки из ленты — замена ОИ в реал-тайме (грабля #187, паттерн 17.17i)
143. vwap_spread: VWAP покупок vs продаж — агрессивность по цене, не по объёму (грабля #189, паттерн 17.17j)
144. Иерархия: слои 1-3 из ленты (мс), ОИ — слой 4 (контекст, 5-15 мин). ОИ не блокирует решение

## TQBR / IMOEX / фондовый рынок

145. Расписание TQBR: основная 09:00–18:55, аукцион закрытия 18:55–19:00, вечерняя 19:00–23:50. Не путать с FORTS (19:00 = конец основной, но 18:55 = конец акций)
146. Планки TQBR: утренняя/основная = от закрытия ПРЕДЫДУЩЕГО дня, вечерняя = от закрытия ТЕКУЩЕГО дня. Разные базы для разных сессий
147. Аукцион закрытия: Call-фаза 18:55:00–18:57:29, сделки 18:57:30–19:00. Цена аукциона = РЦ для FORTS. Не торговать в Call-фазе без понимания фазы
148. Дискретный аукцион: триггер IMOEX 15% / акция 20% за 10 мин. 2 серии по 30 мин. Только лимитные заявки. Проверять статус ДА перед отправкой
149. ДСВД: планки не расширяются. При касании — торги на планке, пересмотра нет. Клиринг — в понедельник
150. IMOEX состав: единственный источник — moex.com/ru/index/IMOEX/constituents (официальный). НЕ использовать сторонние агрегаторы, Википедию, блоги
151. Фьючерс-маппинг: SBER→SBRF, SBERP→SBRP, SNGS/SNGSP→SNGS (один контракт), TRNFP→TRNF. Остальные = тикер + суффикс экспирации
152. Веса IMOEX: рыночные, пересчитываются ежедневно. Состав (тикеры) меняется на ребалансировке (3-я пятница марта/июня/сентября/декабря). Ограничение: одна бумага ≤15%, топ-5 ≤55%
153. Бэктест гэпа через ISS: SETTLEPRICE (РЦ 19:00, заполнен) — НЕ SETTLEPRICEDAY (null, грабля #199). Проверять пагинацию (start=0,100,200...) и лимит 100 запросов/мин
154. Качество 15-min aggregated candles: проверять flat OHLC (open==high==low==close) — признак обобщённой свечи без диапазона. Если 15-min HIGH < 1-min HIGH — данные битые (грабля #201). Агрегировать из 1-мин свечей вручную
155. Порог сигнала: |B| >= 0.5 для торговли (30 сделок, profit factor 4.63). |B| >= 0.3 — шум, win rate < 50% (грабля #202). Для прогноза направления порога нет (раздел 44.6), для торговли — 0.5
156. Точка выхода: TP по best price внутри 15 мин, НЕ по close. Mean-reversion разворачивается к закрытию (грабля #203). V51 по close = -0.65%, по TP = +5.93% net
157. Асимметрия лонг/шорт: шорты по close 15 мин — 23.5% win rate, лонги — 53.8%. Но по TP внутри 15 мин: шорты 82.4% favourable, лонги 69.2%. Структурное свойство рынка, не специфика сигнала (грабля #204)
158. Комиссия и slippage: round-trip 0.2% (0.1% за сторону) + slippage 0.05% = 0.25%. При avg favourable +0.35-0.50% — остаётся 0.10-0.25% на сделку. 30 сделок × 0.15% avg net = +4.5% за период. Проверять что gross > 0.25% перед входом

## РАЗДЕЛ 21. КЛИРИНГ: МЕТОДИКА ВМ

## Двухфазный клиринг НКЦ

Фаза 1: m-t-m (mark-to-market) — 23:50–00:30
 - Пересчёт позиций по РЦ 19:00
 - Зачисление/списание ВМ
 - Обновление ГО

Фаза 2: Расчётная сессия — ~20:00 МСК следующего дня
 - Фактическое движение денег

## Три формулы ВМ

| Состояние позиции | Формула ВМ | База |
|---|---|---|
| Новая (открыта сегодня, не закрыта) | ВМ = (РЦ - цена_сделки) × позиция | Цена сделки |
| Перенесённая (открыта вчера+, не закрыта) | ВМ = (РЦ_сегодня - РЦ_вчера) × позиция | РЦ вчера |
| Закрытая (сделка закрытия сегодня) | ВМ = (цена_закрытия - РЦ_пред) × позиция | РЦ пред. клиринга |

## VM-парадокс

ВМ клиринга = (РЦ − база) × позиция — РЦ заменила текущую цену. Это НЕ (текущая − база) × позиция.
- Положительная ВМ при убыточной позиции — нормально
- Отрицательная ВМ при прибыльной позиции — нормально
- Сумма всех ВМ = реальный P&L (сходится при закрытии)

## Стратегии работы с парадоксом

S1: Закрыть раньше — закрыть до 23:50, если цена после 19:00 пошла в плюс
S2: Фантомная маржа — использовать ВМ как однодневное плечо
S3: Перенос убытка — не закрывать убыточную позицию, ВМ от РЦ «мягче»

## РАЗДЕЛ 22. КЛИРИНГ: РАСПИСАНИЕ T/T+1

- Экспирация: последний торговый день → поставка/расчёт
 ★ Время экспирации: 14:00 или 19:00 (зависит от инструмента)
 Вариант 1: экспирация в торгах (14:00 или 19:00) — онлайн, без остановки
 Вариант 2: экспирация в клиринге m-t-m (23:50) — для поставочных фьючерсов
 ★ Типы экспирации :
 - Расчётные фьючерсы и премиальные опционы → онлайн в торгах (14:00/19:00)
 - Маржируемые опционы → онлайн + поставка фьючерса в торгах
 - Поставочные фьючерсы → в клиринговой сессии m-t-m (НЕ онлайн)
 ★ Онлайн-исполнение : ГО освобождается за минуты, финрезультат доступен
 в той же сессии. Ключевое изменение ЕТС.

- Поставка: для поставочных фьючерсов в клиринге m-t-m
- ГО обновляется: ежедневно в клиринге m-t-m + auto-shift внутри дня при резких движениях

## РАЗДЕЛ 23. ФАНДИНГ ВЕЧНЫХ ФЬЮЧЕРСОВ

- K1/K2 — коэффициенты фандинга для вечных фьючерсов
- ★ История параметров K1/K2 :
 USDRUBF/EURRUBF: K1=0.1%, K2=0.15% (с 21.04.2025)
 CNYRUBF: K1=0%, K2=0.35% (с 19.01.2026)
 Новые фьючерсы (акции США, крипта): K1=0%, K2=0.35%
 ⚠ Дата «12.10.2026» НЕ подтверждается источниками
- ★ Точная формула ВМ для вечного фьючерса :
 ВМ = Переоценка_позиции − Фандинг × Лот × sign(pos) + Дивид.поправка × Лот × sign(pos)
 ★ Знак фандинга и дивидендной поправки зависит от направления позиции
 Фандинг: лонг платит (−), шорт получает (+). Дивидендная поправка: лонг получает (+), шорт платит (−)
 Дивидендная поправка: IMOEXF → IMOEXDIV (расчёт в 16:00), RGBIF → 0
 ★ Дивидендная поправка учитывается ТОЛЬКО по позиции на пред. клиринг (23:50)
 По новым сделкам в течение дня — НЕ учитывается [грабля #145]
- Статистика фандинга 2026 (качественная оценка):
 SBERF, GAZPF — стабильно положительный фандинг (высокий годовой эквивалент)
 IMOEXF — стабильно положительный, умеренный
 USDRUBF, GLDRUBF — положительный, умеренно высокий
 EURRUBF, CNYRUBF — положительный, умеренный
 RGBIF — низкий фандинг
 ★ Помесячная динамика фандинга доступна на сайте Мосбиржи (moex.com/derivatives)
 ★ Расчёт фандинга по некоторым контрактам сдвинут на 09:00 (с 14.09.2026)
- В QUIK: параметр FUNDING_RATE
- ★ Точная формула фандинга (moex.com/a8141):
 Фандинг = MIN(L2; MAX(−L2; MIN(−L1, D) + MAX(L1, D)))
 где D — отклонение цен ВФ и БА, L1 = K1 × Цена_спот, L2 = K2 × Цена_спот
 Три режима: |D| ≤ L1 → линейный; L1 < |D| ≤ L2 → зона нечувствительности; |D| > L2 → максимальный фандинг
- ★ Знаки в формуле ВМ:
 Фандинг — со знаком «минус» (вычитается из ВМ)
 Дивидендная поправка — со знаком «плюс» (прибавляется к ВМ)
 Знак по направлению позиции: лонг → фандинг платит (−), шорт → получает (+)
- ★ USDRUBF/EURRUBF — особый режим фандинга:
 Индикативный фандинг в течение дня НЕ рассчитывается (особенности курса ЦБ).
 Публикуется итоговое значение после 18:00 МСК.
 Для остальных контрактов (SBERF, GAZPF, IMOEXF и др.) — индикативный фандинг каждую минуту.
 ★ Скрипты мониторинга фандинга должны учитывать: для USDRUBF/EURRUBF getParamEx2 FUNDING_RATE
 в течение дня может возвращать 0 или устаревшее значение.

## Вечные фьючерсы — сводка (перенесено из раздела 36)

- Универсальный фильтр: наличие FUNDING_RATE через getParamEx2 (паттерн 17.36)
- K1=0%, K2=0.35% — параметры фандинга для новых фьючерсов
- Экспирация: 19:00 (расчётные, онлайн) — грабля #135
- 20 вечных фьючерсов (сентябрь 2026): AMDF, TSLAF, APPF, COINF и др. — грабля #137
- Криптовечные: BTCUSDF, ETHUSDF, SOLUSDF, XRPUSDF, TRXUSDF — только квалифицированные инвесторы

## KEYRATE (KK) — сводка (перенесено из раздела 36)

- БА = индекс ключевой ставки
- Экспирация в дни заседаний ЦБ (грабля #138)
- Старт торгов: 29.09.2026
- Полная спецификация — раздел 41

## РАЗДЕЛ 24. VM-ПАРАДОКС — ПРАВИЛО ДЛЯ СКРИПТА

После 19:00 общая прибыль = ВМ_клиринга + ВМ_завтрашнего_дня
- ВМ_клиринга = (РЦ - база) × позиция — зачислится сегодня
- ВМ_завтра = (текущая_цена - РЦ) × позиция — «зависнет» до завтра

Скрипт, показывающий «прибыль» по текущей цене, врёт после 19:00.
Раздельный учёт: vm_this_clearing + vm_next_clearing.

## Числовой пример

```
Позиция: +10 контрактов Si
Цена входа: 84 500
РЦ (фиксация в 19:00): 85 000
Текущая цена после 19:00: 85 500

ВМ_клиринга = (РЦ - цена_входа) × позиция = (85 000 - 84 500) × 10 = +5 000 ₽
  → зачислится в клиринг 23:50, доступно утром как ГО

ВМ_завтра = (текущая - РЦ) × позиция = (85 500 - 85 000) × 10 = +5 000 ₽
  → «зависнет» до следующего клиринга, НЕ зачислится сегодня

Скрипт, показывающий «прибыль» = (85 500 - 84 500) × 10 = +10 000 ₽ — ВРЁТ.
Реально зачислится только 5 000 ₽. Остальные 5 000 ₽ — завтра.
```

## Связка со стратегиями (раздел 21)

- **S1: Закрыть раньше** — закрыть до 23:50, если цена после 19:00 пошла в плюс → ВМ от цены сделки
- **S2: Фантомная маржа** — использовать ВМ_клиринга как однодневное плечо (раздел 29)
- **S3: Перенос убытка** — не закрывать убыточную позицию, ВМ от РЦ «мягче» (раздел 21)

## vm_split — код разделения ВМ

```lua
-- Разделяет отображаемую «прибыль» на ВМ_клиринга и ВМ_завтра
-- Использует getFuturesHolding (паттерн 17.1) и getParamEx2 (паттерн 17.21)
local function vm_split(class, sec, account, firmid, entry_price)

 -- РЦ = CLPRICE (фиксированная после клиринга)

 -- Текущая цена

 -- ВМ клиринга = (РЦ - база) × позиция
 -- ВМ завтра = (текущая - РЦ) × позиция

-- [... код сокращён ...]
end

-- Использование:
-- local vm_cl, vm_next = vm_split("SPBFUT", sec, account, firmid, entry_price)
-- message(string.format("ВМ клиринга: %.2f, ВМ завтра: %.2f", vm_cl, vm_next))
```

## РАЗДЕЛ 25. СКАЛЬПЕРСКИЕ ПАТТЕРНЫ

## Архитектура скальперского скрипта

1. main() — основной цикл с adaptive sleep
2. OnQuote — флаг изменения стакана (не чтение!)
3. OnAllTrade — флаг новой сделки (не обработка!)
4. Чтение/обработка — только в main()
5. sinsert — безопасное добавление в таблицу из callbacks

## Флаги callbacks — только сигнал, не обработка

```lua
-- Глобальные флаги (доступны из main() и callbacks)
local quote_changed = false   -- стакан изменился
local trade_arrived = false    -- новая сделка в ленте
local last_trade_price = 0     -- цена последней сделки (для OnAllTrade)

-- OnQuote: только флаг — НЕ вызывать getQuoteLevel2 здесь!
-- Грабля #93: подписка асинхронна, OnQuote может прийти позже
-- Грабля #95: НЕ InsertRow в OnQuote — только sinsert (главный поток)
function OnQuote(class, sec)
 if class == CLASS_CODE and sec == SEC_CODE then
 quote_changed = true
 end
end

-- OnAllTrade: только флаг и цену — НЕ обрабатывать!
function OnAllTrade(alltrade)
 if alltrade.sec_code == SEC_CODE then
 trade_arrived = true
 last_trade_price = tonumber(alltrade.price) or 0
 end
end
```

## adaptive_sleep — адаптивная пауза основного цикла

```lua
-- ★ Adaptive sleep: меньше пауза = быстрее реакция, но больше CPU
-- При активности (флаги) — минимальная пауза (10 мс)
-- При простое (нет флагов) — плавный рост до 200 мс
-- Сброс при появлении флага
local sleep_ms = 50
local SLEEP_MIN = 10    -- минимальная пауза при активности
local SLEEP_MAX = 200   -- максимальная пауза при простое
local SLEEP_STEP = 10   -- шаг увеличения

local function adaptive_sleep(has_activity)
 if has_activity then
 sleep_ms = SLEEP_MIN  -- мгновенный сброс
 else
 sleep_ms = math.min(sleep_ms + SLEEP_STEP, SLEEP_MAX)  -- плавный рост
 end
 sleep(sleep_ms)
 return sleep_ms
end
```

## sinsert — безопасное добавление в таблицу из callbacks

```lua
-- ★ Грабля #95: InsertRow/SetCell в OnQuote/OnAllTrade — опасно (главный поток)
-- sinsert накапливает данные в буфер, main() читает и вставляет
local insert_queue = {}  -- очередь строк для вставки

-- Вызывать из callbacks (OnQuote, OnAllTrade) — безопасно
local function sinsert(row_data)
 table.insert(insert_queue, row_data)
end

-- Вызывать из main() — обработка очереди
local function process_insert_queue(t_id)
 while #insert_queue > 0 do
 local row = table.remove(insert_queue, 1)
 local row_idx = InsertRow(t_id, -1)
 if row_idx then
 SetCell(t_id, row_idx, 0, tostring(row.time or ""))
 SetCell(t_id, row_idx, 1, tostring(row.price or ""))
 SetCell(t_id, row_idx, 2, tostring(row.qty or ""))
 -- ... дополнительные колонки
 end
 end
end
```

## Цикл main() — обработка только в главном потоке

```lua
function main()

 -- Обработка изменения стакана
 -- Логика скальпера: вход/выход по дисбалансу
 -- Сильный дисбаланс bid → покупка
 -- send_order(CLASS_CODE, SEC_CODE, ...)  -- паттерн 17.14
 -- Сильный дисбаланс ask → продажа

 -- Обработка новой сделки
 -- Обновление сентимента (паттерн 17.17)
 -- sinsert({time=os.date("%H:%M:%S"), price=last_trade_price, qty=1})

 -- Обработка очереди вставки в таблицу

 -- Проверка стоп-лосса
 -- ... проверка позиции и цены

 -- Adaptive sleep

 -- Очистка
```

## Риск-менеджмент

- Стоп-лосс — обязательно (нет промежуточного клиринга)
- Расчёт ГО перед открытием — CalcBuySell (паттерн 15.3)
- Мониторинг свободных средств — getMoney (паттерн 15.3)
- Лимит одновременных заявок — проверять через count_active_orders() (паттерн 17.14c)
- Максимальная позиция — ограничение в контрактах (например, 10)
- После клиринга (23:50–00:30) — пауза, getFuturesHolding может вернуть nil (грабля #33)
- Уведомление при auto-shift ГО (паттерн 17.26) — ГО мог вырасти внутри дня

## Производительность

- getQuoteLevel2: ~202K тактов на вызов (раздел 28)
- Прямое чтение через подписку: ~6.5K тактов — в 31× быстрее
- Для скальпера: кэшировать результат getQuoteLevel2 в main(), не вызывать повторно
- adaptive_sleep экономит CPU в простое, мгновенно реагирует на активность
- sinsert гарантирует: callbacks не блокируют главный поток QUIK

## РАЗДЕЛ 26. КЛАССЫ ИНСТРУМЕНТОВ

| Класс | Описание | ParamRequest | getQuoteLevel2 | Особенности QLua |
|-----------|---------------------------------|--------------|----------------|------------------|
| SPBFUT | Фьючерсы FORTS | Да (BUYDEPO, SELLDEPO, CLPRICE, STEPPRICE) | Да | futures_client_holding, getFuturesHolding, getFuturesLimit |
| SPBOPT | Опционы FORTS | Да (STEPPRICE, THEORYPRICE) | Да | NetOptionValue, volatility, Greeks через getParamEx2 |
| TQBR | Акции (основной режим) | Да (LAST, BID, ASK) | Да | getDepo, getDepoEx (ЕДП), lot_size, margin_rate |
| TQOB | Облигации | Да (LAST, YIELD) | Да | НКД через getParamEx2, погашение через MATDATE |
| CETS | Валютный рынок | Да (LAST, BID) | Да | Режимы: TOD, TOM, SWS. getParamEx2 для RATE |
| TQTF | ETF и ПИФы | Да (LAST, BID) | Да | Аналогично TQBR, но лотность может отличаться |
| SPBXM | Иностранные бумаги (деп. расписки) | Да (LAST, BID, ASK) | Да | Аналогично TQBR, getDepo, getDepoEx |
| TQBD | Переговорные сделки (крупные лоты) | Да (LAST) | Нет | Вне стакана, режим переговорных сделок |

★ Особенности:
- SPBFUT/SPBOPT: getItem("futures_client_holding") — основной способ чтения позиций
- TQBR/TQOB/TQTF: getDepo() — позиции по бумагам, getDepoEx() — по ЕДП
- CETS: отдельный класс, не путать с SPBFUT для валютных фьючерсов (USDRUBF)
- ParamRequest нужен для всех параметров кроме SECCODE и SHORTNAME
- getSecurityInfo не требует ParamRequest и работает для всех классов
- SPBXM: иностранные ценные бумаги (депозитарные расписки), аналог TQBR по API
- TQBD: режим переговорных сделок (крупные лоты, вне стакана)

## РАЗДЕЛ 27. СЕРВИСНЫЕ ФУНКЦИИ

## getInfoParam — полный список параметров QUIK

| Параметр | Описание |
|----------|----------|
| SERVERTIME | Время сервера (HH:MM:SS) |
| TRADEDATE | Дата торгов (DD.MM.YYYY) |
| CLEARING | Состояние клиринга |
| TRADENAME | Имя торгового сервера |
| USERID | ID пользователя |
| VERSION | Версия QUIK |
| CONNECT_TIMEOUT | Таймаут подключения (мс) |
| RECONNECT_TIMEOUT | Таймаут переподключения (мс) |
| LAST_SEND_TIME | Время последней отправки |
| LAST_RECV_TIME | Время последнего приёма |
| SERVER_ADDR | Адрес сервера |
| SERVER_PORT | Порт сервера |
| CLIENT | Тип клиента |
| SESSION_STATE | Состояние сессии |
| ARGUMENTS | Аргументы командной строки |

## Прочие сервисные функции

```lua
-- sleep(ms) — единственный способ паузы в main()
-- НЕ использовать в callbacks (главный поток заблокируется!)

-- message(msg, level) — всплывающее окно в QUIK
-- Level: 1 = info, 2 = warning, 3 = error

-- isConnected() — true/false (не 1/0)
 -- торговля

-- sysdate() — системная дата QUIK (таблица)
local d = sysdate()
-- d = {year, month, day, hour, min, sec, wday, yday}

-- getScriptPath() — путь к скрипту (для относительных путей)
local path = getScriptPath()
local config_path = path .. "\\config.ini"

-- PrintDbgStr(msg) — вывод в лог QUIK (qlic.log), не отображается

-- isDarkTheme() — true/false (тёмная тема QUIK)
 -- тёмные цвета для QTable
```

## SearchItems — поиск по таблице QUIK

```lua
-- Поиск элементов в таблице по фильтру
-- Возвращает индексы найденных элементов
local function find_positions(sec_code)
 local result = SearchItems(
 "futures_client_holding",  -- имя таблицы
 0,                         -- начальный индекс
 getNumberOf("futures_client_holding") - 1,  -- конечный
 function(item)
 return item.sec_code == sec_code
 end,
 true                       -- возвращать все совпадения
 )
 return result  -- массив индексов или nil
end

-- Использование:
local indices = find_positions("SiZ6")
if indices then
 for _, idx in ipairs(indices) do
 local item = getItem("futures_client_holding", idx)
 -- обработка
 end
end
```

## Метки на графике (AddLabel / DeleteLabel)

```lua
-- См. раздел 16.6 для полного примера AddLabel
-- AddLabel(tag, params) — добавить метку
-- GetLabelParams(tag, label_id) — получить
-- SetLabelParams(tag, label_id, params) — изменить
-- DeleteLabel(tag, label_id) — удалить
-- DeleteAllLabels(tag) — удалить все метки на графике
```

★ Грабля: message() блокирует главный поток до закрытия окна.
 Для некритичных уведомлений — использовать QTable (SetCell) вместо message().

## РАЗДЕЛ 28. ПОДПИСКА НА СТАКАН

## Программная подписка

```lua
Subscribe_Level_II_Quotes(class, sec) -- подписка
Unsubscribe_Level_II_Quotes(class, sec) -- отписка
IsSubscribed_Level_II_Quotes(class, sec) -- проверка
```

## subscribe_with_retry — подписка с ретраями

```lua
-- ★ Грабля #93: подписка асинхронна, может не сработать с 1-й попытки
-- ★ Грабля #94: отписка с ретраями — может не сработать с 1-й попытки
local function subscribe_with_retry(class, sec, max_retries)
 max_retries = max_retries or 5
 for i = 1, max_retries do
 Subscribe_Level_II_Quotes(class, sec)
 sleep(500)  -- ждём подтверждения
 if IsSubscribed_Level_II_Quotes(class, sec) then
 return true
 end
 end
 message("Не удалось подписаться на стакан " .. sec, 2)
 return false
end

local function unsubscribe_with_retry(class, sec, max_retries)
 max_retries = max_retries or 5
 for i = 1, max_retries do
 Unsubscribe_Level_II_Quotes(class, sec)
 sleep(200)
 if not IsSubscribed_Level_II_Quotes(class, sec) then
 return true
 end
 end
 return false
end
```

Грабли:
- Подписка асинхронна — OnQuote может прийти позже (грабля #93)
- Отписка с ретраями — может не сработать с 1-й попытки (грабля #94)
- OnQuote только флаг — чтение getQuoteLevel2 в main() (грабля #95)
- При остановке скрипта — обязательно отписаться от всех инструментов

## Производительность

- getQuoteLevel2: ~202K тактов на вызов
- Прямое чтение через subscribed: ~6.5K тактов
- Разница: ~31× — для скальпера критично

## РАЗДЕЛ 29. СТРАТЕГИЯ «ФАНТОМНАЯ МАРЖА» (S2)

## Механика

После 19:00 РЦ заморожена. Если открыть позицию «ниже РЦ» (лонг) или
«выше РЦ» (шорт), в клиринге 23:50 зачислится положительная ВМ.
Эти деньги доступны как ГО на следующее утро. На следующий клиринг
фантомная ВМ списывается обратно.

## Формула плеча

```
Фантомная_ВМ = |RUB_MARGIN| × позиция
Доп_контракты = floor(Фантомная_ВМ / min(ГО_лонга, ГО_шорта))
```

## ★ T+1 и MTM-регистры

Фантомная ВМ доступна через MTM-регистры в money_amount УТРОМ
 (ранее считалось, что до 20:00 T+1 — это неверно).

После клиринга m-t-m в 23:50 фантомная ВМ записывается в MTM-регистры.
Утром следующего дня money_amount уже содержит фантомную ВМ.

НПР1 = money_amount + rmt_vm – rmt_im
 = (баланс + фантом) – ГО
 = фантом доступен как ГО для новых позиций ✅

T+1 в 20:00 — это бухгалтерская операция (фактическое движение денег),
а не торговая. Для открытия позиций фантом доступен с утра.
Ограничение T+1 касается только ВЫВОДА средств, не торговли.

Аналогия со старой моделью: промежуточный клиринг 14:00 → вечерний 18:50
= m-t-m 23:50 → расчётная сессия 20:00 T+1. Та же логика.

## Три уровня

1. Buffer — не открывать новые позиции, просто buffer против маржин-колла
2. Плечо — открыть доп. позиции на фантомные деньги
3. Арбитраж — фантом на нескольких инструментах + межрыночный арбитраж

## Условия прибыльности

- Позиция ≥10 контрактов + разрыв РЦ >0.5%
- Фантомная_ВМ > ГО × N (для N доп. контрактов)
- Крупная позиция (>30) + существенный разрыв

## Риски

- Цена не отскочила → фантом списан + доп. позиции в убытке
- ГО изменилось → фантомных денег не хватило
- Ликвидность после 19:00 — тонкий стакан
- Маржин-колл при большом расхождении

## Фантом-сканер

## Колонки

| Колонка | Что показывает |
|---------|----------------|
| PHANTOM_LEVERAGE | floor(|RUB_MARGIN| / min(BUYDEPO, SELLDEPO)) |
| PHANTOM_VM_POS | Фантомная ВМ для текущей позиции |
| SHORTNAME | Краткое имя (для сортировки) |

## Сортировка

По убыванию PHANTOM_LEVERAGE — инструменты с наибольшим плечом наверху.

## Алерты

1. PHANTOM_LEVERAGE ≥ 1 → жёлтый (фантом-кандидат)
2. |DELTA_PCT| ≥ 3% → зелёный/красный (большой разрыв)
3. NUMTRADES 50–100 → оранжевый (низкая ликвидность)

## РАЗДЕЛ 30. МЕТОДИКА РАСЧЁТА ГО (SPAN-МОДЕЛЬ)

★ Источник: документ НКЦ-П-2026-221 от 11.09.2026

## Сценарный подход

Основа алгоритма — сценарный подход:
Для каждой Группы Инструментов рассматривается набор сценариев:
- цена базисного актива
- кривая процентных ставок
- подразумеваемая волатильность

Для каждого сценария рассчитывается финансовый результат закрытия
всех позиций. Берётся наихудший результат.

## 4 категории риска

| Категория | Расшифровка | Уровень |
|-----------|-------------|--------|
| КНУР | Начальный уровень риска | Базовый |
| КСУР | Стандартный уровень риска | Повышенный |
| КОУР | Особый уровень риска | Высокий |
| КПУР | Повышенный уровень риска | Максимальный |

У каждой категории свои MR1/MR2/MR3 (см. ниже).

## 3 уровня ставок обеспечения

| Уровень | Когда применяется | Диапазон сценариев |
|---------|-------------------|--------------------|
| MR1 | Базовый (позиция ≤ LK1) | [P - MR1×Spot; P + MR1×Spot] |
| MR2 | Превышение LK1 (позиция > LK1) | [P - MR2×Spot; P + MR2×Spot] в части превышения |
| MR3 | Превышение LK2 (позиция > LK2) | [P - MR3×Spot; P + MR3×Spot] в части превышения |

LK1, LK2 — лимиты концентрации (по позициям).
Больше позиция → шире сценарии → выше ГО.
★ QUIK показывает только MR1 (базовое ГО). При превышении LK1/LK2
 фактическое ГО выше, чем показывает QUIK!

## 3 группы совместных сценариев

Группа 1: Базовые сценарии (цена, ставки, волатильность)
Группа 2: Сценарии с надбавками MRaddonUp/MRaddonDown + дивиденды
Группа 3: Расширенные сценарии (сценарии экспирации)
Берётся наихудший результат из всех групп.

## Базовое ГО — алгоритм (упрощённый)

Шаг 1: Сценарий падения цены: S = P - MR1 × NormalizedSpot
Шаг 2: Переоценка в сценарии: переоценка = S - P = -MR1 × Spot
Шаг 3: Сценарий процентных ставок: Δ = S × (exp(t × -IR) - 1)
Шаг 4: Суммарный результат: Σ = переоценка_цены + переоценка_ставок
Шаг 5: Перевод в рубли: Σ_руб = Σ × MinStepPrice / MinStep
Шаг 6: ГО с валютной надбавкой: БГО = ABS(Σ_руб × (1 + R))
Округление до 2 знаков (копеек).

★ Это упрощение. Реальный алгоритм — 3 группы сценариев, неттинг/полунеттинг,
 агрегация по группам, залимитные сценарии.

## Валютная надбавка R

R применяется к (финансовый результат + NetOptionValue).
- Положительная при сдвиге курса вверх
- Отрицательная при сдвиге вниз
- Берётся абсолютный минимум из двух значений
- Для USD/RUB: R = ставка MR1 по Si
- Для JPY/RUB: R = 8%

## BA_coeff_go

Коэффициент-множитель ГО, устанавливается участником клиринга per БА.
По умолчанию = 1. Участник может увеличить ГО через этот коэффициент.
Для межконтрактного спреда — максимум из всех БА в спреде.

## КГО — коэффициент клиентского ГО

Применяется ТОЛЬКО на уровне раздела регистра учёта позиции.
Не на уровне Брокерской фирмы или Расчётного кода.
Брокер может установить КГО > 1 — клиентское ГО выше биржевого.

## ReserveCoeff

Коэффициент ограничения выставления заявок, устанавливается
Клиринговым центром. При невыполнении условия — заявки блокируются.

## Auto-shift

При достижении ценового лимита и удержании на нём FutMonTime минут:
 MR_new = MR_curr + 0.5 × FutShift × MR1
ГО растёт прямо в сессии, без клиринга.

## РАЗДЕЛ 31. ПОРТФЕЛЬНОЕ МАРЖИРОВАНИЕ

★ Источник: документ НКЦ-П-2026-221

## Неттинг vs Полунеттинг

| Уровень | Агрегация | Календарный спред | Межконтрактный спред |
|---------|-----------|-------------------|---------------------|
| Расчётный код | Неттинг | Неттинг | Неттинг |
| Брокерская фирма | Выбирает участник | Выбирает участник | Выбирает участник |
| Раздел регистра | Полунеттинг | Полунеттинг | Полунеттинг |

★ Раздел регистра (уровень клиента) — ВСЕГДА Полунеттинг.
 ГО при Полунеттинге выше, чем при Неттинге.

## NCI(БА) — правило исполняющегося фьючерса

За NCI(БА) расчётных периодов до экспирации фьючерса:
- Включается Полунеттинг даже при Неттинге
- Льгота по календарному спреду отключается
- ГО растёт
- NCI(БА) устанавливается Клиринговым центром

Аналогично NCIOpt(БА) — для опционов.

## Запрет скидки по фьючерсам

Признак per-client (раздел регистра):
- Лонг ниже РЦ → цена = РЦ в сценариях
- Шорт выше РЦ → цена = РЦ в сценариях
- Убирает льготу по календарному спреду
- ГО выше

## Межмесячные (календарные) спреды

Противоположные позиции в разных сериях одного БА.
При Неттинге: льгота — блокируется большее из двух ГО (или процентный риск).
При Полунеттинге: ГО суммируется (хуже).

## Межконтрактные спреды

Противоположные позиции в разных БА (например, Ri и IMOEX).
Блокируется большее из двух ГО.
window_size(БА) — полуширина диапазона сценариев.

## ГО для опционов

Покупатель: ГО = премия (риск ограничен)
Продавец: ГО ≈ ГО фьючерса (риск неограничен)
Голый шорт опциона: SOMC + надбавка SOMC(БА,7kk) от 0 до 5

## РАЗДЕЛ 32. GO В QUIK

## BUYDEPO / SELLDEPO — правильная интерпретация

★ ГРАБЛЯ #109: Документация QUIK перепутана!

| Параметр | В документации QUIK | Реальное значение |
|----------|---------------------|-------------------|
| BUYDEPO | «ГО продавца» | **ГО лонга** (покупка) |
| SELLDEPO | «ГО покупателя» | **ГО шорта** (продажа) |

Имя параметра = его смысл. BUYDEPO = обеспечение для покупки (лонг).
SELLDEPO = обеспечение для продажи (шорт).

## Задержка при чтении

getParamEx2 BUYDEPO может вернуть 0 при первом вызове — QUIK не успел загрузить.
Решение: цикл с sleep(100), до 100 попыток (паттерн 22.25).

## Рыночная заявка = 1.5× ГО

Биржа блокирует 1.5× ГО при рыночной заявке — запас на проскальзывание.
Использовать лимитные заявки для экономии ГО.

## Auto-shift в QUIK

ГО может вырасти внутри дня (при auto-shift).
Мониторить BUYDEPO/SELLDEPO в реальном времени, не только после клиринга.

## Брокерское vs биржевое ГО

QUIK показывает БИРЖЕВОЕ ГО (с учётом MR1 выбранной категории).
Брокер может установить:
- BA_coeff_go > 1 (per БА)
- КГО > 1 (per раздел регистра)
- Категорию риска выше (КСУР/КОУР/КПУР вместо КНУР)

Фактическое ГО клиента = биржевое × BA_coeff_go × КГО (приблизительно).

## Округление ГО

Итоговое значение ГО округляется до 2 знаков после запятой (копеек).
В скрипте: math.floor(go * 100 + 0.5) / 100

## РАЗДЕЛ 33. ОПЦИОНЫ В ГО

★ Источник: документ НКЦ-П-2026-221 от 11.09.2026

## Типы опционов

| Параметр | Значения |
|----------|----------|
| ExerciseStyle | Американский, Европейский |
| MarginStyle | Маржируемый, Премиальный |
| SettlementType | Поставочный, Расчётный |
| OptionModel | Модель Блэка, Модель Башелье |

## NetOptionValue

NetOptionValue = Σ (volume × P_opt × MinStepPrice / MinStep)

- Для маржируемых опционов: NetOptionValue = 0
- Для премиальных опционов: учитывается в валютной надбавке
- При признаке «Маржирование премиальных опционов без учёта ГО и NOV»:
 NOV = 0, блокируется премия

## SOMC — непокрытая продажа опциона

SOMC(БА) — минимальное требование за «непокрытую продажу»
SOMC(БА,7kk) — надбавка, устанавливается участником, 0–5

Для спот-опционов — с коэффициентом Lot_Coeff(OSnum,БА).

## ГО синтетической позиции

Рассчитывается отдельно для:
- Проданный Call + купленный фьючерс (покрытый Call)
- Проданный Put + проданный фьючерс (покрытый Put)

ГО синтетической позиции < ГО голого шорта опциона.
Транслируется в QUIK и на сайт Биржи.

## Сценарии экспирации

Только для поставочных опционов с несовпадающей датой экспирации.
Начинаются за NclrToDelivery расчётных периодов (участник) /
ExpClearingSA(расчётный код, Клиринговый центр).

Диапазон: [P - 0.5×MR1×NormalizedSpot; P + 0.5×MR1×NormalizedSpot]

Call: Strike < P_fut → фин. результат = закрытие фьючерса по Strike
Put: Strike > P_fut → фин. результат = закрытие фьючерса по Strike

## W.cl / W.br — веса учёта рисков экспирации

W.cl — для раздела регистра учёта позиции (участник)
W.br — для Брокерской фирмы (участник)

## Модель ценообразования

OptionModel(БА) = Модель Блэка или Модель Башелье
Выбор зависит от базисного актива.
Теоретическая цена опциона = Call или Put, рассчитывается на основании:
- цены базисного актива
- подразумеваемой волатильности
- модели ценообразования

## NullVolat — сценарий «нулевой» волатильности

Признак NullVolat(OSnum,БА):
- Снижение подразумеваемой волатильности до минимально допустимого
- Применяется для оценки рисков опционов
- Стресс-сценарий

## Сценарии волатильности

VR(БА) — ставка риска роста/падения IV (маржируемые, БА = фьючерс)
VRspot(БА) — для премиальных (БА = спот или фьючерс)
VVR(БА) — ставка риска поворота (twist) поверхности IV
VVRspot(БА) — то же для премиальных

## Дивидендный риск

CFRisk(БА) — ставка риска изменения дивидендных выплат
Применяется для опционов на ценные бумаги
CF(БА, t_cf, type) — приведённая стоимость дивидендов

## РАЗДЕЛ 34. ЕДИНАЯ ТОРГОВАЯ СЕССИЯ (ЕТС)

★ Источник: fondium.ru, moex.com (презентация ETS на SR 03.12.2025)

## Ключевое изменение с 23.03.2026

Вечерняя сессия относится к **текущему** торговому дню (ранее — к следующему).
Позиция живёт весь календарный день.

## Расписание

| Период | Расписание | Дата начала |
|--------|-----------|-------------|
| Переходный | 07:00–23:50 | с 23.03.2026 |
| Полное | **06:50–23:50** | с **14.07.2026** |

★ Грабля #121: скрипты, рассчитывающие «торговый день», должны учитывать:
 вечерняя сессия = текущий день, не следующий.

## Клиринг и движение денег

| Фаза | Время | Что происходит |
|------|-------|----------------|
| m-t-m (mark-to-market) | 23:50–00:30 | Переоценка по РЦ 19:00, зачисление ВМ, обновление ГО |
| Расчётная сессия | ~20:00 T+1 | **Фактическое движение денег** (ВМ, премии, комиссии) |

★ Грабля #122: ВМ зачисляется в клиринге 23:50 (в MTM-регистры),
 но движение денег — в 20:00 T+1. Для торговли ВМ доступна утром через
 money_amount. Для вывода — только после 20:00.

## Индикативные ставки риска НКЦ (с 07.04.2026)

- Оценка изменения цены за 2 торговых дня с вероятностью 99%
- Отдельные ставки для падения и роста
- Публикуются на сайте НКЦ
- Брокеры используют для плеча по акциям
- ★ Не путать с биржевым ГО (грабля #123)

## Гарантийный фонд НКЦ

Для участников с частичным обеспечением:
- Срочный рынок: 10 млн ₽
- Фондовый рынок: 10 млн ₽
- Валютный рынок: 10 млн ₽
- При 100% обеспечении — взнос не нужен

## 5-уровневая система защиты ЦК

1. Обеспечение дефолтного участника
2. Взнос в ГФ дефолтного участника
3. Выделенный капитал ЦК
4. Взносы других участников в ГФ
5. Распределение убытков по противоположным позициям

★ НКЦ может инициировать п.5 после исчерпания ГФ.
 При дефолте контрагента позиция может быть закрыта принудительно.

## Драгметаллы в Едином пуле (с 23.03.2026)

Драгоценные металлы можно зачислять на Расчётный код Единого пула —
как рубли и валюту. Расширяет доступное обеспечение.
Кодовое слово: UVRUPXXXXX (где XXXXX — номер Расчётного кода).

## Версионность документа НКЦ

★ Актуальные номера и даты документов НКЦ: nationalclearingcentre.ru
★ Документы обновляются каждые ~6 месяцев. Проверять обе версии.
★ Принципы (ЧТО считать) и Методика (КАК) — разные документы.
★ Не хранить конкретные номера — устаревают при каждом обновлении.

## РАЗДЕЛ 35. СТАТИЧЕСКИЕ РИСК-ПАРАМЕТРЫ И ЕДИНЫЙ ПУЛ

★ Источник: НКЦ-П-2026-161 (Методика), moex.com (параметры),
 nationalclearingcentre.ru (статические параметры)

## Методика определения риск-параметров

Отдельный документ от Принципов ГО:
- **Принципы** (НКЦ-П-2026-221) — ЧТО считать (алгоритм, формулы)
- **Методика** (НКЦ-П-2026-161) — КАК определяются ставки MR1/MR2/MR3,
 кривые, лимиты концентрации

★ Грабля #131: два документа обновляются независимо. Проверять обе версии.
 Методика обновлялась 3 раза за 2026 (20.03, 17.04, 13.07).

## Статические риск-параметры

Публикуются на сайте НКЦ (nationalclearingcentre.ru/rates/derivativesStaticParams)
и Мосбиржи (moex.com/ru/derivatives/parameters.aspx):

| Параметр | Описание |
|----------|----------|
| RangeFut | Диапазон ценового коридора фьючерса |
| RangeCS | Диапазон для календарных спредов |
| MDRule | Правило маржинального требования |
| AutoShift | Признак авто-сдвига коридора |
| NumMREvg | Кол-во МТ в вечернюю сессию |
| FutMonTimeDay | Время мониторинга планки (день), сек |
| FutMonTimeEvg | Время мониторинга планки (вечер), сек |
| FutMonNum | Кол-во мониторингов до сдвига |
| FutShift | Величина сдвига коридора (доля от MR1) |
| CSShift | Сдвиг для спредов |
| Scen_UP | Сценарий роста для ОПС |
| Scen_DOWN | Сценарий падения для ОПС |
| ncl | Кол-во клирингов для NCI(БА) (полунеттинг) |

★ Полная формула auto-shift: MR_new = MR_curr + 0.5 × FutShift × MR1
 Параметры мониторинга: FutMonTimeDay/Evg (сек удержания на планке),
 FutMonNum (кол-во раз до сдвига).

## Реальные значения MR — см. moex.com/ru/derivatives/parameters.aspx
★ Конкретные значения MR (Si, IMOEX, Brent, ASTR, ETHAA и др.) обновляются регулярно.
★ Актуальные данные: moex.com/ru/derivatives/parameters.aspx
★ Не хранить конкретные значения в шпаргалке — устаревают при каждом пересмотре НКЦ.

Полуширина диапазона сценариев для межконтрактных спредов.
Публикуется на Мосбирже.
Для расчёта ГО по спреду между разными БА (например, Ri и IMOEX):
ГО спреда = max(GO_BA1, GO_BA2) в пределах window_size.

## ETHAA — лимиты концентрации

| Уровень | LK1 | LK2 |
|---------|-----|-----|
| MR2 | 29 | 266 |
| MR3 | 146 | 333 |

★ Актуальные лимиты: nationalclearingcentre.ru/rates/derivativesStaticParams

## Обособленные клиенты (Portability) — перенесено из раздела 37

- Переход к другому УК за 2 дня без согласия базового УК
- Проверка обособления: паттерн 17.38 (check_obosoblennie)
- Отчёт EQM20 — соответствие Расчётного кода Обособленному клиенту
- Грабля #140: обособленный клиент может уйти без согласия брокера
- Грабля #141: обособленная БФ — изоляция обеспечения одной БФ от другой
- Защита от кросс-дефолта внутри одного УК

## Инвалюта как обеспечение — перенесено из раздела 37

- «Иное обеспечение» (балансовый счёт 47405) — грабля #139
- Меньшая защита при дефолте УК (в отличие от рублей в Едином пуле)
- Дисконт = MR1 (грабля #132): 1000 USD при MR1=15% → 850 USD-эквивалента
- Драгметаллы в Едином пуле — с 23.03.2026 (см. раздел 34)

## РАЗДЕЛ 36. → см. 23, 41 [ЯКОРЬ: РАЗДЕЛ 36]
## РАЗДЕЛ 37. → см. 35 [ЯКОРЬ: РАЗДЕЛ 37]
## РАЗДЕЛ 38. ФОРМУЛЫ КЛИРИНГОВЫХ ОТЧЁТОВ

★ Контент распределён по файлу:
- Паттерн 17.39 (calc_free_amount) — формула свободных средств
- Паттерн 17.42 (check_removed_fields) — удалённые поля отчётов
- Грабли #143-148 — формулы отчётов, экспирация, поля

## Основная формула
amount_end = amount_begin + in_out_netto + var_marg + prem + charges
amount_end_mtm = amount_end + var_marg_mtm + prem_mtm + charges_mtm
free = amount_end_mtm - go + nov

## Полная таблица полей клирингового отчёта (monsettlcl)

| Поле | Статус | Описание |
|------|--------|----------|
| amount_begin | Актуально | Начальный остаток |
| in_out_netto | Актуально | Ввод/вывод нетто |
| var_marg | Актуально | Вариационная маржа |
| prem | Актуально | Премия опционов |
| charges | Актуально | Комиссии |
| var_marg_mtm | Актуально | ВМ по MTM-регистрам |
| prem_mtm | Актуально | Премия по MTM |
| charges_mtm | Актуально | Комиссии по MTM |
| go | Актуально | Гарантийное обеспечение |
| nov | Актуально | NetOptionValue |
| free | Актуально | Свободные средства |
| buy_deposit_erc | Новое | ГО лонга, уровень ERC |
| buy_deposit_hrc | Новое | ГО лонга, уровень HRC |
| buy_deposit_lrc | Новое | ГО лонга, уровень LRC |
| buy_deposit_mrc | Новое | ГО лонга, уровень MRC |
| client_risk_level | Новое | Уровень риска клиента |
| base_im_buy | Новое | Базовое ГО лонга (заменило basegobuy) |
| base_im_sell | Новое | Базовое ГО шорта (заменило basegosell) |
| isrepo | Удалено | (декомиссия — обновить парсеры) |
| account_forts | Удалено | (декомиссия) |
| limit | Удалено | (декомиссия) |
| pr_setll | Удалено | (декомиссия) |
| pr_settl_r | Удалено | (декомиссия) |
| spot | Удалено | (декомиссия) |
| base | Удалено | (декомиссия) |

## parse_clearing_report — парсинг CSV-отчёта

```lua
-- Парсинг клирингового отчёта monsettlcl (CSV)
-- Проверка: is_field_removed() перед чтением (паттерн 17.42)
local REMOVED = {

local function parse_clearing_report(filepath)

 -- Парсинг CSV (разделитель — запятая)

 -- Заголовки
 -- Строка данных

 -- Расчёт свободных средств (паттерн 17.39)

-- [... код сокращён ...]
end

-- Использование:
-- local rows, free = parse_clearing_report(getScriptPath() .. "\\monsettlcl.csv")
-- if rows then message("Свободно: " .. tostring(free), 1) end
```

## РАЗДЕЛ 39. РЫНОЧНО-НЕЙТРАЛЬНЫЙ АРБИТРАЖ НА ФАНДИНГЕ

★ Источник: rbc.ru (27.09.2026), spread-i.online, finam.ru, habr.com

## Механика стратегии

1. Покупаете базовый актив (например, 100 акций Сбербанка на споте)
2. Продаёте эквивалентный вечный фьючерс (1 контракт SBERF)
3. Пока фандинг положительный — шорт получает платёж каждый день
4. Позиция рыночно-нейтральная: движение цены не влияет (дельта ≈ 0)

## Формула чистой доходности

 NET = Фандинг_год − Стоимость_капитала − Комиссии − Спред − Проскальзывание

| Параметр | SBERF | GAZPF | IMOEXF |
|----------|-------|-------|--------|
| Фандинг | 15.1% | 15.0% | 14.1% |
| Ставка ЦБ (капитал) | 14.0% | 14.0% | 14.0% |
| Комиссии | 0.1% | 0.1% | 0.1% |
| Спред | 0.05% | 0.05% | 0.10% |
| Проскальзывание | 0.05% | 0.05% | 0.10% |
| **NET** | **0.9%** | **0.8%** | **−0.1%** |

★ SBERF и GAZPF — самые устойчивые, положительный фандинг все 8 месяцев 2026.
★ USDRUBF — волатильный: от +30% (янв) до −4% (мар). Не подходит для стабильного арбитража.
★ IMOEXF — NET отрицательный при ставке ЦБ 14%. При снижении ставки ЦБ до 12% → NET ~2%.

## Дивидендная поправка

Для IMOEXF: дивидендная поправка считается через IMOEXDIV (расчёт в 16:00).
Учитывается ТОЛЬКО по позиции на пред. клиринг (23:50) — грабля #145.
Для SBERF, GAZPF: дивиденды на споте компенсируются дивидендной поправкой на фьючерсе.

## Риски

1. **Смена знака фандинга** — конструкция становится убыточной (грабля #156)
2. **Basis risk** — цена ВФ отклоняется от БА (грабля #157)
3. **Tracking error** — IMOEXF нельзя купить напрямую (грабля #159)
4. **Liquidity** — тонкий стакан на дальней ноге (грабля #158)
5. **Стоимость капитала** — при ставке ЦБ 14% NET может быть отрицательным (грабля #160)

★ Паттерны: calc_funding_arb_profit (17.45), check_funding_sign (17.46)

## calc_hedge_ratio — расчёт хедж-отношения

```lua
-- Сколько единиц БА нужно на 1 контракт вечного фьючерса
-- lot_size_futures — размер контракта фьючерса (из getSecurityInfo)
-- lot_size_spot — размер лота на спотовом рынке (из getSecurityInfo)
local function calc_hedge_ratio(class_fut, sec_fut, class_spot, sec_spot)
 local info_fut = getSecurityInfo(class_fut, sec_fut)
 local info_spot = getSecurityInfo(class_spot, sec_spot)
 if not info_fut or not info_spot then return nil end

 local fut_lot = tonumber(info_fut.lot_size) or 1
 local spot_lot = tonumber(info_spot.lot_size) or 1

 -- Хедж-отношение = размер контракта фьючерса / размер лота спота
 return fut_lot / spot_lot
end

-- Пример: SBERF lot_size=100, SBER lot_size=10 → ratio=10
-- Покупаем 10 акций SBER на каждый 1 контракт SBERF (шорт)
```

## arb_enter — вход в арбитраж

```lua
-- Полный цикл входа: проверка фандинга → ГО → покупка спота → продажа фьючерса
local function arb_enter(class_fut, sec_fut, class_spot, sec_spot,
 -- 1. Проверка фандинга

 -- 2. Расчёт хедж-отношения

 -- 3. Проверка ГО перед входом

 -- 4. Проверка свободных средств

 -- 5. Вход: покупка спота, продажа фьючерса

-- [... код сокращён ...]
end
```

## arb_monitor — мониторинг позиции

```lua
-- Проверка знака фандинга каждую минуту в main()
local function arb_monitor(class_fut, sec_fut, is_short)
 local pe = getParamEx2(class_fut, sec_fut, "FUNDING_RATE")
 if not pe or tonumber(pe.result) ~= 1 then return "no_data" end
 local funding = tonumber(pe.param_value) or 0

 -- Проверка смены знака (грабля #156)
 local profitable = check_funding_sign(funding, is_short)  -- паттерн 17.46
 if profitable == false then
 return "exit_signal"  -- фандинг сменил знак — закрывать!
 elseif profitable == true then
 return "hold"
 else
 return "neutral"
 end
end

-- В main():
-- local signal = arb_monitor("SPBFUT", sec_fut, true)
-- if signal == "exit_signal" then
--   -- Закрыть позицию: продать спот, купить фьючерс
-- end
```

## РАЗДЕЛ 40. АРБИТРАЖ СРОЧНЫЙ VS ВЕЧНЫЙ ФЬЮЧЕРС

★ Источник: spread-i.online, broker.finam.ru, habr.com

## Формула справедливого спреда

 Для акций: Справедливый_спред = Спот × Ставка × T × Лот − Дивиденды_нетто × Лот
 Для валют: Справедливый_спред = Спот × (r_RUB − r_FX) × T × Лот

 где T = дней_до_экспирации / 365

Пример: SBER спот 300 ₽, ставка 14%, 90 дней до экспирации, лот 100, див 0
 Справедливый спред = 300 × 0.14 × (90/365) × 100 = 1 036 ₽

## Метод анализа

1. Регрессионный канал: строим канал спреда за 100+ дней
2. Z-score: отклонение текущего спреда от среднего (паттерн 17.48)
3. Зоны входа: Z-score > 1.5–2 сигмы → широкий спред → продать
4. Зоны выхода: Z-score возвращается к 0 → закрыть

## Учёт фандинга в арбитраже

| Сценарий | Влияние |
|----------|---------|
| Фандинг > 0 (шорт ВФ получает) | Доп. доход к арбитражу |
| Фандинг < 0 (шорт ВФ платит) | Доп. расход |
| Фандинг = 0 | Не влияет |

★ Для SBERF (фандинг 15%): шорт вечного → доп. доход ~15% годовых
★ Для USDRUBF (фандинг переменный): может быть как доход, так и расход

## Алгоритм

1. Выбрать БА с срочным и вечным фьючерсом (SBER, GAZP, IMOEX)
2. Рассчитать справедливый спред (паттерн 17.47)
3. Собрать историю спреда, рассчитать Z-score (паттерн 17.48)
4. При |Z-score| > 1.5–2 — вход в арбитраж
5. Проверить ликвидность обеих ног (грабля #158)
6. Учесть фандинг в расчёте NET
7. Выход при Z-score → 0 или смене знака фандинга

★ Паттерны: calc_fair_spread (17.47), calc_spread_zscore (17.48)

## РАЗДЕЛ 41. KEYRATE — ПОЛНАЯ СПЕЦИФИКАЦИЯ

★ Источник: moex.com/ru/derivatives/futures-key-indicators, finam.ru (29.09.2026),
 nationalclearingcentre.ru, rbc.ru

## Базовые параметры

| Параметр | Значение |
|----------|----------|
| Код | KEYRATE, короткий — KK |
| Тип | Расчётный фьючерс (денежный расчёт, без поставки) |
| Базовый актив | Индекс ключевой ставки Мосбиржи |
| Котировка | В пунктах (1 пункт = 1% ставки) |
| Формула индекса | I = r × 100. 14% → 14.00 |
| Лот | 1 |
| Шаг цены | 0,01 пункта |
| Стоимость шага | 10 ₽ |
| Стоимость пункта | 1 000 ₽ (W/R = 10/0,01) |
| Объём контракта | Индекс × 1 000 ₽. При 14.00 → 14 000 ₽ |
| Контрактов одновременно | 2 (ближайший + следующий) |
| Экспирация | 19:00 МСК в плановые даты заседаний ЦБ |
| Индекс публикуется | Каждый рабочий день до 17:00 МСК (с 24.08.2026) |
| Внеплановое заседание | Досрочного исполнения НЕТ, индекс пересчитывается на след. рабочий день |

## Текущие контракты (на 29.09.2026)

★ Конкретные параметры KKV6/KKZ6 (цены, ГО, лимиты) — см. moex.com/ru/derivatives
★ Не хранить конкретные значения — устаревают при каждом заседании ЦБ.
★ Контрактные параметры KEYRATE: W/R = 1000 ₽/пункт, ГО ~3 000 ₽ (LK1), ~6 700 ₽ (с категорией).

★ Плечо: ~3 000 ₽ ГО при ~14 000 ₽ контракте = ~4,7×

## Направление торговли

| Ожидание | Действие | Прибыль |
|----------|----------|---------|
| Ставка ВЫШЕ ожиданий рынка | Покупка | (факт − цена) × 1 000 ₽ |
| Ставка НИЖЕ ожиданий рынка | Продажа | (цена − факт) × 1 000 ₽ |
| Ставка = ожиданиям | Нет сделки | ~0 |

★ Цена = ожидаемая ставка ПРЯМО (13.86 = 13.86%, НЕ 86.14%)
★ Цена KEYRATE = ожидаемая ставка напрямую (пример: 13.86 = 13.86%, не 86.14%). Рынок ожидает снижение с 14% до ~13,86%)

## Формула ВМ

 ВМ_открытие = (РЦ_тек − Цена_входа) × W/R
 ВМ_удержание = (РЦ_тек − РЦ_пред) × W/R

 W/R = 1 000 ₽ за пункт
 Изменение на 0,25 п.п. = 250 ₽ на контракт

## Стратегии

1. **Хеджирование**: компания с кредитом КС+3% покупает KEYRATE — компенсация роста ставки
2. **Спекуляция**: покупка/продажа перед заседанием при расхождении прогноза с рынком
3. **Календарный спред**: KKV6 vs KKZ6 — разница ожиданий между заседаниями
4. **Термометр**: цена = консенсус-прогноз ставки (KKV6 13.86 → рынок ждёт снижение)

## Ключевые даты

| Событие | Дата |
|---------|------|
| Старт торгов | 29.09.2026 |
| Заседание ЦБ (ближайшее) | 23.10.2026 |
| Экспирация KKV6 | 23.10.2026 19:00 |
| Заседание ЦБ (следующее) | 18.12.2026 |
| Экспирация KKZ6 | 18.12.2026 19:00 |

★ Паттерны: calc_keyrate_vm (17.49), get_keyrate_direction (17.50), check_keyrate_calendar (17.51), check_keyrate_limits (17.52)

## РАЗДЕЛ 42. ТЕСТИРОВАНИЕ И ОТЛАДКА

## Шаблон минимального торгового скрипта

```lua
-- minimal_trading_script.lua
-- Скелет: OnInit / main / OnStop / OnQuote / OnAllTrade
-- Копировать как основу для нового скрипта

local is_run = true
local is_connected = false
local t_id = nil
local ds = nil
local CLASS_CODE = "SPBFUT"
local SEC_CODE = ""  -- заполнить при инициализации

function OnInit()
 -- Создание таблицы, подписки, загрузка конфига
 
 -- Подписки
-- [... код сокращён ...]
end

function OnQuote(class, sec)
 -- Только флаг! Не читать getQuoteLevel2 здесь
 -- quote_changed = true
-- [... код сокращён ...]
end

function OnAllTrade(alltrade)
 -- Только флаг! Не обрабатывать здесь
 -- trade_received = true
-- [... код сокращён ...]
end

function OnConnected()
-- [... код сокращён ...]
end

function OnDisconnected()
-- [... код сокращён ...]
end

function OnStop()
-- [... код сокращён ...]
end

function OnCleanUp()
 -- Последний шанс при жёстком закрытии QUIK
-- [... код сокращён ...]
end

function main()
 -- Основной цикл: чтение данных, обработка, отображение
 -- ...
 -- Очистка
-- [... код сокращён ...]
end
```

## Отладка

- `PrintDbgStr(msg)` — вывод в лог QUIK (файл qlic.log). Не отображается в терминале.
- `message(msg, level)` — всплывающее окно. Level: 1=info, 2=warning, 3=error.
- Для интерактивной отладки — QTable с выводом переменных в ячейки.
- `os.time()` и `os.date()` — для временных меток в логе.

## Логирование в файл с ротацией

```lua
local log_file = nil
local log_path = "C:\QUIK_logs\"
local log_name = "script.log"
local log_max_size = 1048576 -- 1 MB
local log_count = 0

local function log_msg(msg)
 if not log_file then
 log_file = io.open(log_path .. log_name, "a")
 end
 if log_file then
 local ts = os.date("%Y-%m-%d %H:%M:%S")
 log_file:write(ts .. " | " .. msg .. "\n")
 log_file:flush()
 log_count = log_count + 1
 -- Ротация: проверка размера каждые 100 записей
 if log_count % 100 == 0 then
 log_file:close()
 log_file = io.open(log_path .. log_name, "a")
 local size = log_file:seek("end")
 if size > log_max_size then
 log_file:close()
 os.rename(log_path .. log_name, log_path .. "script_" .. os.date("%Y%m%d_%H%M%S") .. ".log")
 log_file = io.open(log_path .. log_name, "w")
 end
 end
 end
end
```

## Моки QUIK-функций для тестов без терминала

```lua
-- mock_quik.lua
-- Загружать ДО основного скрипта при тестировании вне QUIK
-- Использование: lua -e "require('mock_quik'); dofile('my_script.lua')"

local M = {}

-- Мок getParamEx2
M.params = {}
function getParamEx2(class, sec, param)
-- [... код сокращён ...]
end

-- Мок getItem / getNumberOf
M.tables = {}
function getNumberOf(name) return #M.tables[name] or 0 end
end
function getItem(name, idx)
-- [... код сокращён ...]
end

-- Мок sendTransaction
function sendTransaction(t)
-- [... код сокращён ...]
end

-- Мок message
function message(msg, level)
-- [... код сокращён ...]
end

-- Мок sleep
function sleep(ms)
 -- no-op в тестах
-- [... код сокращён ...]
end

-- Мок isConnected
function isConnected() return true end

-- Мок getInfoParam
-- [... код сокращён ...]
end
function getInfoParam(param)
-- [... код сокращён ...]
end

return M
```

★ Преимущества моков:
- Тестирование логики без QUIK (CI/CD, unit-тесты)
- Воспроизводимость: одинаковые данные → одинаковый результат
- Скорость: нет задержек сети/биржи
- Изоляция: проверка edge cases (nil, 0, пустой стакан)

## РАЗДЕЛ 43. QUIK IPC И ТОРГОВЫЕ ТАБЛИЦЫ

## Управление подпиской на стакан

★ Подписка/отписка с ретраями — см. раздел 28 (subscribe_with_retry, unsubscribe_with_retry).
★ Грабли #93-95 — в разделе 28. При остановке скрипта — обязательно отписаться.

## Создание дашборда через QTable

```lua
-- Дашборд: мониторинг позиций, ГО, ВМ в реальном времени
local function create_dashboard()
-- [... код сокращён ...]
end

local function update_dashboard(tid, positions, vm_map, go_map, free_amount)
 -- Подсветка: отрицательная ВМ — красная
-- [... код сокращён ...]
end
```

## OnQTableClose — корректная обработка

```lua
local is_recreating = false

function OnQTableClose(tid)
 if is_recreating then
 return true -- разрешить закрытие при пересоздании
 end
 is_run = false
 return true -- разрешить закрытие, остановить скрипт
end
```

## OnMenuCommand — команды из меню таблицы

```lua
-- Добавление пункта меню
-- В QUIK: правый клик на таблице → Редактировать меню
function OnMenuCommand(tid, menu_id)
 if menu_id == 1 then
 -- Экспорт в CSV
 elseif menu_id == 2 then
 -- Обновить данные
 elseif menu_id == 3 then
 -- Закрыть позицию
 end
end
```

## IPC между скриптами

Способы обмена данными между QLua-скриптами:
1. **Файлы** — самый надёжный. Скрипт A пишет, скрипт B читает. Использовать блокировки (rename atomic).
2. **Общая таблица QUIK** — скрипт A пишет в QTable, скрипт B читает через GetCell.
3. **Socket (luasocket)** — если доступен. TCP/UDP для реального времени.
4. **Внешний процесс** — pipe или os.execute для командной строки.

★ Рекомендация: файлы с atomic rename для конфигурации, QTable для реального времени.

## IPC через файлы с atomic rename

```lua
-- Атомарная запись: пишем во временный файл, затем переименовываем
-- os.rename — атомарная операция на уровне ОС
-- Скрипт A (писатель):
local function ipc_write(filepath, data)
-- [... код сокращён ...]
end

-- Скрипт B (читатель):
local function ipc_read(filepath)
-- [... код сокращён ...]
end

-- Использование:
-- Скрипт A: ipc_write("C:\\QUIK_ipc\\signal.txt", {"BUY", "SiZ6", "10", "85000"})
-- Скрипт B: local msg = ipc_read("C:\\QUIK_ipc\\signal.txt")
```

## IPC через QTable (SetCell / GetCell)

```lua
-- Скрипт A (писатель) создаёт QTable и пишет сигнал:
local ipc_tid = nil
function OnInit()
 ipc_tid = AllocTable()
 AddColumn(ipc_tid, 0, "Signal", true, QTABLE_STRING_TYPE, 20)
 AddColumn(ipc_tid, 1, "Sec", true, QTABLE_STRING_TYPE, 15)
 AddColumn(ipc_tid, 2, "Qty", true, QTABLE_INT64_TYPE, 10)
 CreateWindow(ipc_tid)
 SetWindowCaption(ipc_tid, "IPC Signal")
 InsertRow(ipc_tid, -1)
end

-- Запись сигнала:
function send_ipc_signal(signal, sec, qty)
 if not ipc_tid then return end
 SetCell(ipc_tid, 0, 0, signal)
 SetCell(ipc_tid, 0, 1, sec)
 SetCell(ipc_tid, 0, 2, tostring(qty), to_int(qty))
end

-- Скрипт B (читатель) читает через GetCell:
local function read_ipc_signal(tid)
 local sig = GetCell(tid, 0, 0)  -- col 0, row 0
 local sec = GetCell(tid, 0, 1)  -- col 1, row 0
 local qty = GetCell(tid, 0, 2)  -- col 2, row 0
 return sig, sec, qty
end
```

## IPC через luasocket (если доступен)

```lua
-- luasocket может быть доступен в QUIK (зависит от версии)
-- Скрипт A (сервер): слушает порт, отправляет сигналы
-- Скрипт B (клиент): подключается, получает сигналы в реальном времени

-- Сервер (упрощённо):
-- local socket = require("socket")
-- local server = socket.bind("127.0.0.1", 12345)
-- local client = server:accept()
-- client:send("BUY,SiZ6,10,85000\n")

-- Клиент:
-- local socket = require("socket")
-- local conn = socket.connect("127.0.0.1", 12345)
-- local line = conn:receive("*l")
-- -- парсинг line
```

★ Внимание: luasocket может отсутствовать в вашей версии QUIK.
 Проверка: `local ok, socket = pcall(require, "socket")`.

## РАЗДЕЛ 44. IMOEX + БЛИЖАЙШИЕ ФЬЮЧЕРСЫ: ЛОГИКА МАППИНГА

 ★ Источник: moex.com/ru/index/IMOEX/constituents (ЕДИНСТВЕННЫЙ официальный источник)
 ★ НЕ использовать сторонние агрегаторы, Википедию, блоги (грабля #150)
 ★ Состав IMOEX (тикеры) меняется на ребалансировке (3-я пятница марта/июня/сентября/декабря)
 ★ Веса пересчитываются ежедневно по рыночной капитализации с учётом free-float
 ★ Ограничения индекса: одна бумага ≤15%, топ-5 ≤55%

## 44.1. Источники данных

| Данные | Источник | Endpoint |
|--------|----------|----------|
| Состав IMOEX (тикеры, веса) | MOEX ISS API | iss.moex.com/iss/statistics/engines/stock/markets/index/analytics/IMOEX/tickers.json |
| Спецификации фьючерсов | MOEX FORTS | moex.com/ru/derivatives |
| Лотность фьючерсов | QUIK getSecurityInfo | getSecurityInfo("SPBFUT", sec_code).lot_size |
| История фьючерсов (OHLC + РЦ) | MOEX ISS API | iss.moex.com/iss/history/engines/futures/markets/forts/securities/{contract} |
| История акций (OHLC) | MOEX ISS API | iss.moex.com/iss/history/engines/stock/markets/shares/securities/{ticker} |
| История IMOEX (индекс) | MOEX ISS API | iss.moex.com/iss/history/engines/stock/markets/index/securities/IMOEX |

 ★ Если MOEX ISS недоступен — страница moex.com/ru/index/IMOEX/constituents
 ★ Требует регистрации для XML/CSV. ISS API — публичный, без регистрации.
 ★ История фьючерсов: endpoint возвращает SETTLEPRICE (РЦ 19:00, заполнен), CLOSE, OPEN, HIGH, LOW, WAPRICE, VOLUME, VALUE. SETTLEPRICEDAY присутствует, но null (грабля #199)
 ★ Лимит ISS: 100 запросов/мин. Пауза 0.7 сек между запросами — достаточно.
 ★ Пагинация: start=0, start=100, start=200... (по 100 записей на страницу).

## 44.2. Правила маппинга: тикер акции → тикер фьючерса

### Базовое правило
```
FUT_ticker = EQUITY_ticker + "-" + <EXP_SUFFIX>
```
где EXP_SUFFIX = ближайший ликвидный контракт (MM.GY, например "12.26" = декабрь 2026)

### Исключения (ручной маппинг)

| Тикер акции | Тикер фьючерса | Причина |
|------------|---------------|---------|
| SBER | SBRF | Историческое сокращение |
| SBERP | SBRP | Историческое сокращение (прив.) |
| SNGS | SNGS | Совпадает (но один контракт на оба) |
| SNGSP | SNGS | Один контракт на оба класса (ао + ап) |
| TRNFP | TRNF | Усечённое название |
| X5 | FIVE | Тикер фьючерса отличается (FIVE = X5 Group) |
| HEAD | HHRU | Историческое сокращение (HeadHunter → HHRU) |
| VKCO | VKCO | Совпадает (но проверять при ребалансировке) |

### Псевдокод маппинга

```lua
-- Словарь исключений (акция → фьючерс без суффикса)
local fut_exceptions = {
  SBER  = "SBRF",
  SBERP = "SBRP",
  SNGSP = "SNGS",  -- один контракт на SNGS + SNGSP
  TRNFP = "TRNF",
  X5    = "FIVE",
  HEAD  = "HHRU",
}

-- Текущий суффикс экспирации (обновлять при роллировке)
local CURRENT_EXP_SUFFIX = "12.26"  -- декабрь 2026

local function map_equity_to_future(equity_ticker)
  -- Проверяем исключения
  if fut_exceptions[equity_ticker] then
    return fut_exceptions[equity_ticker] .. "-" .. CURRENT_EXP_SUFFIX
  end
  -- Базовое правило
  return equity_ticker .. "-" .. CURRENT_EXP_SUFFIX
end
```

## 44.3. Лотность и тип контрактов

| Параметр | Правило | Источник |
|----------|---------|----------|
| Лот фьючерса | getSecurityInfo("SPBFUT", fut_ticker).lot_size | QUIK / FORTS specs |
| Тип контракта | Расчётный (без поставки) — для всех IMOEX-эмитентов | FORTS specs |
| Базовый актив | Соответствующая акция (TQBR) | FORTS specs |

 ★ Лотность может меняться при роллировке контрактов — проверять через getSecurityInfo
 ★ Все фьючерсы на акции IMOEX-эмитентов — расчётные (без поставки)

## 44.4. Алгоритм построения сводной таблицы

```lua
-- Входные данные: IMOEX_composition (с MOEX ISS API)
-- Выходные данные: сводная таблица {тикер, название, вес, спот, фьючерс, лот, тип}

local function build_imoex_futures_table(imoex_composition, forts_specs)

    -- Получаем лотность из FORTS specs
    -- Fallback на словарь (если QUIK недоступен)

-- [... код сокращён ...]
end
```

## 44.5. Обновление при ребалансировке

| Событие | Что обновлять | Как |
|---------|--------------|-----|
| Ребалансировка IMOEX (раз в квартал) | IMOEX_composition | Скачать с MOEX ISS API |
| Роллировка фьючерсов (раз в квартал) | CURRENT_EXP_SUFFIX | Заменить суффикс (12.26 → 03.27) |
| Изменение лотности (редко) | forts_specs | getSecurityInfo в QUIK |
| Новые исключения маппинга | fut_exceptions | Проверить тикеры новых бумаг в IMOEX |

 ★ Перед использованием таблицы — проверить актуальность состава на moex.com
 ★ Скрипт должен хранить дату последнего обновления и предупреждать если устарела

## 44.6. Механика гэпа на открытии (взвешенный базис фьючерсов)

★ Суть: сравнение взвешенного индекса фьючерсов с взвешенным РЦ → прогноз направления утреннего открытия
★ Время съёма: 23:50 (закрытие вечерней сессии) — НЕ 19:01, к 23:50 отсеян шум за ~5 часов торгов
★ Нормировка: по сумме весов бумаг с фьючерсами (НЕ по 100% IMOEX)
★ Порог нечувствительности: для прогноза НЕТ (знак = направление), для торговли |B| >= 0.5 (раздел 44.11)
★ MX/IMOEXF: используется как референс (согласованность усиливает сигнал)

### Формулы

```
Для каждой бумаги i с фьючерсом:
  b_i = (F_i(23:50) - SETTLEPRICE_i(19:00)) / SETTLEPRICE_i(19:00) × 100%
  где SETTLEPRICE_i — расчётная цена фьючерса (фиксируется в 19:00, раздел 18.2)
  обе цены — фьючерсные → контанго сокращается в разности

Взвешенный базис:
  B = Σ(w_i × b_i) / Σ(w_i)                   — нормировка по бумагам с фьючерсами

Альтернативная запись (абсолютные величины):
  IMOEX_SETTLE = Σ(w_i × SETTLEPRICE_i)        — взвешенная расчётная цена фьючерсов (19:00)
  IMOEX_ФЬЮЧ   = Σ(w_i × F_i(23:50))           — взвешенная цена фьючерсов (23:50)
  B = (IMOEX_ФЬЮЧ - IMOEX_SETTLE) / IMOEX_SETTLE × 100%

Сигнал:
  B > 0 → гэп ВВЕРХ на открытии
  B < 0 → гэп ВНИЗ на открытии
```

### Параметры

| Параметр | Значение | Обоснование |
|----------|----------|-------------|
| SETTLEPRICE фиксация | 19:00 МСК (клиринг FORTS, раздел 18.2) | SETTLEPRICE через getParamEx2("SPBFUT", fut, "SETTLEPRICE") |
| Снимок фьючерсов | 23:50 МСК (закрытие вечерней сессии) | 5 часов торговли отсеивают шум |
| Нормировка | Σ(w_i) по бумагам с фьючерсами | Не разбавлять сигнал нулевым вкладом бумаг без фьючерсов |
| Порог | Для прогноза — нет. Для торговли — \|B\| >= 0.5 | Знак B = направление гэпа. \|B\| >= 0.3 — шум (грабля #202) |
| Референс | MX/IMOEXF — базис индексного фьючерса | Согласованность с B усиливает сигнал |
| Бумаги без фьючерсов | LENT, RENI, UGLD, MSNG, RAGR (~1.5% веса) | Вклад минимален, исключаются из расчёта |

### Учётные факторы (малы, но знать)

| Фактор | Влияние | Компенсация |
|--------|---------|-------------|
| Контанго/бэквордация | Систематическое завышение B | СОКРАЩАЕТСЯ в формуле: обе цены (SETTLEPRICE и LAST) — фьючерсные, контанго в обеих. MX — доп. референс направления |
| Дивидендные гэпы | Ложный «гэп вниз» по бумаге с экс-дивидендной датой | Ручной фильтр: проверить календарь дивидендов |
| Низкая ликвидность к 23:50 | Спреды расширяются, последние сделки нерепрезентативны | Мониторить спред, при широком — исключить из расчёта |

### QLua: calc_gap_signal — расчёт сигнала гэпа в реальном времени

```lua
-- ★ Расчёт взвешенного базиса фьючерсов на акции IMOEX
-- ★ Снимок в 23:50 МСК (закрытие вечерней сессии)
-- ★ Нормировка по бумагам с фьючерсами
-- ★ Референс: MX (индексный фьючерс)
-- ★ Использует: map_equity_to_future() из 44.2, getParamEx2 (раздел 15)

local function calc_gap_signal(imoex_composition, firmid, account)
  -- imoex_composition: массив {ticker, name, weight_pct} с MOEX ISS API
  -- Возвращает: B (взвешенный базис, %), IMOEX_РЦ, IMOEX_ФЬЮЧ, mx_basis (референс)

    -- SETTLEPRICE фьючерса (расчётная цена, зафиксирована в 19:00)
    -- ★ НЕ CLPRICE акции! Обе цены должны быть фьючерсными (контанго сокращается)

    -- Цена фьючерса (LAST, снимок 23:50)

    -- Базис фьючерса: (цена 23:50 - расчётная цена 19:00) / расчётная цена 19:00
    -- ★ Обе цены — фьючерсные, контанго сокращается

    -- Накопление

  -- Взвешенный базис

  -- Референс: базис индексного фьючерса (MX)
  -- SETTLEPRICE индексного фьючерса (расчётная цена MX в 19:00)
  -- ★ Не сравниваем с IMOEX index! Обе цены должны быть фьючерсными

  -- Сигнал

  -- Согласованность с MX

-- [... код сокращён ...]
end

-- Использование (в main(), снимок в 23:50):
-- local result = calc_gap_signal(imoex_composition, firmid, account)
-- message(string.format("Сигнал: %s, B=%.3f%%, MX: %.3f%%, confirmed=%s, покрытие=%.1f%%",
--   result.signal, result.B, result.mx_basis,
--   tostring(result.mx_confirmed), result.coverage))
-- ★ v52: SETTLEPRICE вместо CLPRICE — контанго сокращается в формуле
```

### Логика работы

1. **19:00** — клиринг FORTS фиксирует SETTLEPRICE для каждого фьючерса (раздел 18.2)
2. **19:00–23:50** — вечерняя сессия, фьючерсы торгуются, каждый со своим базисом к SETTLEPRICE
3. **23:50** — снимок: для каждого фьючерса вычисляется b_i = (F_i − SETTLEPRICE_i) / SETTLEPRICE_i
4. Взвешивание: B = Σ(w_i × b_i) / Σ(w_i) — нормировка только по бумагам с фьючерсами
5. Сравнение с MX: mx_basis = (MX_LAST − MX_SETTLEPRICE) / MX_SETTLEPRICE — если знак совпадает с B — сигнал подтверждён
6. **B > 0 → открытие вверх, B < 0 → открытие вниз** — без порога

★ КЛЮЧЕВОЕ: обе цены (SETTLEPRICE в 19:00 и LAST в 23:50) — фьючерсные. Контанго есть в обеих
  и сокращается в разности. Остаток — чистый направленный сдвиг за вечернюю сессию.

### Почему 23:50, а не 19:01

- В 19:01 базис — шум: SETTLEPRICE только что зафиксирована, фьючерсы не «переварили» цену
- К 23:50 отфильтрованы: импульсные движения, низколиквидные скачки, информационный поток
- Базис на 23:50 — это накопленное ожидание рынка к завтрашнему открытию, а не реакция на SETTLEPRICE

### Почему SETTLEPRICE, а не CLPRICE акции

- CLPRICE (TQBR) — цена закрытия **акции**, не несёт контанго
- Фьючерс (SPBFUT) несёт контанго ~3–4% (ставка × дней до экспирации)
- Сравнение F_i с CLPRICE_i даёт B завышенный на контанго → знак может инвертироваться
- SETTLEPRICE (SPBFUT) — расчётная цена **фьючерса** в 19:00, контанго уже встроен
- Разность (F_i(23:50) − SETTLEPRICE_i(19:00)) — обе цены фьючерсные, контанго сокращается
- Остаток = чистый направленный сдвиг за вечернюю сессию

### Связка с другими разделами

| Связь | Раздел | Описание |
|-------|--------|----------|
| Расписание TQBR | 18.0 | РЦ фиксируется в аукционе закрытия 18:55–19:00 |
| ВМ и клиринг | 21 | РЦ заменяет текущую цену в ВМ клиринга |
| VM-парадокс | 24 | После 19:00 ВМ делится на клиринговую и «зависшую» |
| Арбитраж спот↔фьючерс | 39 | Базис отдельного фьючерса — элемент агрегата B |
| Справедливый спред | 40 | Контанго/бэквордация в базисе — учёт через MX |
| Маппинг IMOEX→фьючерс | 44.2 | map_equity_to_future() для каждой бумаги |

## 44.7. Связка с другими разделами

| Связь | Раздел | Описание |
|-------|--------|----------|
| Расписание TQBR | 18.0 | Аукцион закрытия 18:55–19:00 → РЦ для FORTS |
| Арбитраж спот ↔ фьючерс | 39 | calc_hedge_ratio использует lot_size спота и фьючерса |
| Справедливый спред | 40 | calc_fair_spread: спот × ставка × T × лот |
| Классы инструментов | 26 | TQBR (акции) + SPBFUT (фьючерсы) |
| Планки | 18.0 | Коридоры TQBR влияют на доступность спота для арбитража |

## 44.9. Бэктест гэпа через ISS API (исторические данные)

★ Источник: ISS MOEX API — iss.moex.com/iss/history/engines/futures/markets/forts/securities/{contract}
★ Публичный, без регистрации. Лимит: 100 запросов/мин.
★ Пагинация: start=0, start=100, start=200... (100 записей на страницу)

### Поля ISS для бэктеста

| Поле ISS | Что это | Время фиксации | Роль в формуле гэпа |
|----------|---------|----------------|---------------------|
| `SETTLEPRICE` | Расчётная цена текущего дня (РЦ) | 19:00 МСК | **SETTLEPRICE_i(19:00)** — база ✅ ЗАПОЛНЕНО |
| `SETTLEPRICEDAY` | «Теоретическая цена в дневном клиринге» | — | ❌ МЁРТВЫЙ — null в ISS history (грабля #199) |
| `CLOSE` | Цена закрытия (последняя сделка) | ~23:50 МСК | **F_i(23:50)** — снимок |
| `OPEN` | Цена открытия | 09:50 МСК | Гэп открытия (факт) |
| `HIGH` / `LOW` | Экстремумы дня | — | Контекст |
| `WAPRICE` | Средневзвешенная цена | — | Фильтр ликвидности |
| `VOLUME` | Объём (контракты) | — | Фильтр ликвидности |
| `VALUE` | Оборот (рубли) | — | Фильтр ликвидности |

 ★ КЛЮЧЕВОЕ: для бэктеста использовать SETTLEPRICE (19:00), НЕ SETTLEPRICEDAY (null)
 ★ SETTLEPRICE в ISS = «Расчётная цена текущего дня» — РЦ, фиксируемая в 19:00 — ЗАПОЛНЕНО
 ★ SETTLEPRICEDAY = «Теоретическая цена в дневном клиринге» — МЁРТВЫЙ (null в ISS history)
   Источник: github.com/Ruvad39/go-moex-iss/options.go — SETTLEPRICEDAY определён для опционов,
   для фьючерсов в ISS history всегда null. ПК 14:00 отменён с 23.03.2026.
 ★ Аналогично для акций: iss.moex.com/iss/history/engines/stock/markets/shares/securities/{ticker}
   даёт OPEN, CLOSE, HIGH, LOW, VOLUME, VALUE — для проверки фактического гэпа

### Формула бэктеста (через ISS)

```
Для каждого дня D и каждого фьючерса i:
  b_i(D) = (CLOSE_i(D) - SETTLEPRICE_i(D)) / SETTLEPRICE_i(D) × 100%

Взвешенный базис:
  B(D) = Σ(w_i × b_i(D)) / Σ(w_i)

Фактический гэп:
  gap(D) = (OPEN_i(D+1) - CLOSE_i(D)) / CLOSE_i(D) × 100%  — по акциям
  gap_mx(D) = (OPEN_MX(D+1) - CLOSE_MX(D)) / CLOSE_MX(D) × 100%  — по MX

Сравнение:
  sign(B(D)) == sign(gap_mx(D+1)) → hit
  sign(B(D)) != sign(gap_mx(D+1)) → miss
```

★ Формула v54: SETTLEPRICE (не SETTLEPRICEDAY). SETTLEPRICEDAY = null в ISS history (грабля #199).

### Логика бэктеста

1. Скачать историю ~30 фьючерсов + MX + акции за N дней (через ISS, пауза 0.7 сек)
2. Для каждого дня: B(D) = взвешенный базис (CLOSE vs SETTLEPRICE)
3. Для следующего дня: gap(D+1) = открытие MX vs закрытие MX
4. Сравнить знак B(D) с знаком gap(D+1) → hit rate
5. Посчитать P&L: если B > 0 → покупка MX на открытии, B < 0 → продажа
6. Вычесть комиссии (~0,05% на круг)
7. Отчёт: hit rate, confusion matrix, распределение |B|, P&L, сравнение с MX-alone

### Важные отличия от реал-тайм (44.6)

| Параметр | Реал-тайм (44.6) | Бэктест (44.9) |
|----------|-------------------|----------------|
| Источник РЦ 19:00 | QUIK getParamEx2 SETTLEPRICE | ISS SETTLEPRICE (заполнен) |
| Время базиса | 19:00 (клиринг FORTS) | 19:00 (SETTLEPRICE) |
| Время снимка | 23:50 (LAST в QUIK) | 23:50 (CLOSE в ISS) |
| Риск обновления | SETTLEPRICE может обновиться (грабля #198) | SETTLEPRICE зафиксирован в history |
| Проверка | MX через getParamEx2 | MX через ISS OPEN/CLOSE |
| Истёкшие контракты | Неактуально (текущие) | Генерировать secid (раздел 44.10) |

 ★ Грабля #198: в QUIK SETTLEPRICE может обновляться на вечерней сессии (грабля #52).
   Для реал-тайм: сохранять снимок в 19:00 в переменную.
   Для бэктеста: ISS SETTLEPRICE в history — зафиксирован, не обновляется (в отличие от QUIK).

### Скрипт iss_gap_data.py (загрузка данных)

```python
# iss.moex.com/iss/history/engines/futures/markets/forts/securities/{contract}
# ?start=0&from=2026-06-01&till=2026-09-30&iss.meta=off
# Поля: TRADEDATE, SECID, OPEN, HIGH, LOW, CLOSE,
#   SETTLEPRICE, WAPRICE, VOLUME, VALUE
#   SETTLEPRICEDAY — присутствует в схеме, но всегда null (грабля #199)
#
# Для акций: /iss/history/engines/stock/markets/shares/securities/{ticker}
# Для IMOEX: /iss/history/engines/stock/markets/index/securities/IMOEX
# Для MX: /iss/history/engines/futures/markets/forts/securities/MX-9.26 (или текущий)
#
# Пауза: 0.7 сек между запросами (лимит 100/мин)
# Пагинация: start=0, 100, 200...
#
# ★ Использовать SETTLEPRICE (заполнен), НЕ SETTLEPRICEDAY (null — грабля #199)
# Проверка: SETTLEPRICE > 0 (если 0/null — данные битые или нет торгов)
# Проверка: CLOSE > 0 (если 0 — нет вечерней сессии)
# Для истёкших контрактов: генерировать secid (раздел 44.10)
```

### Связка с другими разделами

| Связь | Раздел | Описание |
|-------|--------|----------|
| Механика гэпа | 44.6 | Формула B — та же, источник данных другой |
| Источники данных | 44.1 | ISS endpoint для истории фьючерсов |
| SETTLEPRICE vs SETTLEPRICEDAY | 18.2 | SETTLEPRICE = РЦ 19:00 (заполнен). SETTLEPRICEDAY = мёртвый (null) |
| Грабля #198 | 19 | SETTLEPRICE обновляется в QUIK — для реал-тайм сохранять снимок 19:00 |
| Грабля #199 | 19 | SETTLEPRICEDAY — мёртвый параметр (null в ISS history) |
| Грабля #200 | 19 | ISS securities не возвращает истёкшие контракты |
| Генерация контрактов | 44.10 | rolling front-month: генерация secid истёкших контрактов |
| Тестирование | 42 | Моки QUIK, логирование, edge cases |

## 44.8. Важные замечания

1. НЕ хранить жёсткий список тикеров в шпаргалке — состав меняется на ребалансировке
2. НЕ использовать сторонние источники (Википедия, блоги, агрегаторы) — только MOEX
3. Веса IMOEX — рыночные, пересчитываются ежедневно. Использовать для относительной значимости, не для точных расчётов
4. Топ-10 бумаг ~70% индекса — основная динамика задаётся ими
5. При анализе гэпа: РЦ по всем 44 бумагам IMOEX даёт прогноз направления открытия (см. раздел 18.0 + 18.4)
6. Бэктест гэпа: через ISS API (раздел 44.9) — SETTLEPRICE как база (РЦ 19:00), CLOSE как снимок (~23:50), OPEN следующего дня как факт
7. Грабля #198: SETTLEPRICE в QUIK обновляется на вечерней сессии — для реал-тайм сохранять снимок в 19:00. Для бэктеста SETTLEPRICE в history зафиксирован.
8. Грабля #199: SETTLEPRICEDAY — мёртвый параметр (null в ISS history). НЕ ИСПОЛЬЗОВАТЬ. Использовать SETTLEPRICE.
9. Грабля #200: ISS securities не возвращает истёкшие контракты — генерировать secid (раздел 44.10).
10. Раздел 44.10: генерация истёкших контрактов для rolling-бэктеста (front-month).

## 44.10. Генерация истёкших контрактов для rolling-бэктеста

★ Суть: ISS securities endpoint возвращает только АКТИВНЫЕ контракты (грабля #200).
  Для rolling-бэктеста нужны истёкшие (H6, M6, U6 - март, июнь, сентябрь 2026).
★ Решение: генерировать secid из префикса + месяца + года, загружать через ISS history.

### Проблема

```
ISS /iss/engines/futures/markets/forts/securities.json?limit=9999
  -> только активные контракты (Z6, H7, M7, U7, Z7 - на октябрь 2026)
  -> истёкшие SRH6, SRM6, SRU6 - УДАЛЕНЫ из списка
  -> rolling-бэктест видит только Z6 -> components = 1 (только SBER) в январе-мае
```

### Решение: генерация secid

```python
MONTH_CODES = {'H': 3, 'M': 6, 'U': 9, 'Z': 12}

    prefixes = {}

    generated = []

    unique = []
    return unique
```

### Front-month rolling

```python
def secid_to_expiration_month(secid):
    # Парсинг экспирации из secid: SRH6 -> 2026*12+3, SRZ6 -> 2026*12+12
    if len(secid) < 3: return 0
    month_code = secid[-2]
    year_digit = int(secid[-1])
    year = 2020 + year_digit  # 6 -> 2026, 7 -> 2027
    month = MONTH_CODES.get(month_code, 0)
    return year * 12 + month

def get_front_month_contract(contracts_with_data, current_date):
    # Для данной даты выбрать ближайший к экспирации контракт с данными
    sorted_contracts = sorted(contracts_with_data,
                             key=lambda x: secid_to_expiration_month(x[0]))
    for secid, data in sorted_contracts:
        if current_date in data:
            return secid, data[current_date]
    return None, None
```

### Пример: SBER rolling (январь-сентябрь 2026)

| Период | Контракт | Экспирация | Покрытие |
|--------|----------|-----------|----------|
| 01.01-18.03 | SRH6 | 19.03.2026 | Front-month |
| 19.03-17.06 | SRM6 | 18.06.2026 | Front-month |
| 18.06-16.09 | SRU6 | 17.09.2026 | Front-month |
| 17.09-17.12 | SRZ6 | 17.12.2026 | Front-month |

### Логирование

```
  SBER: 187 days [SRH6(42d), SRM6(42d), SRU6(42d), SRZ6(61d)]
  GAZP: 180 days [GZH6(38d), GZM6(42d), GZU6(40d), GZZ6(60d)]
  MX:   187 days [MXH6(42d), MXM6(42d), MXU6(42d), MXZ6(61d)]
```

### Режим Z6-only vs rolling

| Параметр | Z6-only | Rolling (front-month) |
|----------|---------|----------------------|
| Контракт | Фиксированный (SRZ6) | Меняется по экспирации |
| Ликвидность | Низкая в начале (январь) | Высокая (front-month) |
| components в начале | 1 (только SBER) | 20-30 (все ликвидные) |
| Покрытие IMOEX | 16% в январе | 50-60% с января |

★ Rolling-режим - правильный способ тестирования стратегии: front-month контракт
  всегда наиболее ликвидный, даёт реалистичные цены CLOSE и SETTLEPRICE.
★ Z6-only - только для проверки: дальний контракт может не торговаться в начале периода.

## 44.11. Результаты бэктеста гэп-стратегии (rolling, 186 дней, янв-сен 2026)

★ Период: 2026-01-05 → 2026-09-28, 186 дат (rolling front-month: MXH6 → MXM6 → MXU6 → MXZ6)
★ Источник: gap_results_rolling_20261001_022426.csv (база), _first_minute_v6.csv (1 мин), _first_15min_v13.csv (15 мин)
★ Комиссия: 0.1% за сторону (0.2% round-trip) + slippage 0.05%
★ Корреляция B ↔ gap: -0.28 (слабая, объясняет ~8% дисперсии)

### Торговые версии

| Версия | Логика | Направление |
|--------|--------|-------------|
| **V52** (natural) | B>0 → LONG, B<0 → SHORT | Momentum (продолжение) |
| **V51** (inverted) | B>0 → SHORT, B<0 → LONG | Mean-reversion (откат) |

### Порог |B| >= 0.5: 30 сделок

**Выход по close (1 мин vs 15 мин):**

| Метрика | 1 мин (v6) | 15 мин (v13) |
|---|---|---|
| V51 win rate | 50.0% (15/30) | 66.7% (20/30) |
| V51 cumulative | +4.34% | -0.65% |
| V52 win rate | 50.0% (15/30) | 33.3% (10/30) |
| V52 cumulative | -4.34% | -11.35% |

**LONG (B<0) vs SHORT (B>0), выход по close 15 мин:**

| | n | avg gap_close | win rate |
|---|---|---|---|
| LONG (B<0) | 13 | +0.085% | 53.8% |
| SHORT (B>0) | 17 | -0.249% | 23.5% |

**Выход по TP (best price внутри 15 мин):**

| | n | avg favourable | win rate | net (-0.2%) | cumulative |
|---|---|---|---|---|---|
| LONG TP at high | 13 | +0.331% | 61.5% | +0.131% | +1.70% |
| SHORT TP at low | 17 | +0.449% | 82.4% | +0.249% | +4.23% |
| **Combined** | 30 | — | — | — | **+5.93%** |

### Порог |B| >= 0.3: 54 сделки

| Метрика | V52 (natural) | V51 (inverted) |
|---|---|---|
| Win rate (close) | 46.3% | 53.7% |
| Cumulative (close) | -15.28% | -6.32% |

★ |B| >= 0.3 — шум: win rate < 50% для V52, avg P&L отрицательный для обеих версий. Реальная граница — |B| >= 0.5 (грабля #202).

### 1 минута vs 15 минут (|B| >= 0.5): favourable / adverse

| Метрика | LONG 1 мин | LONG 15 мин | SHORT 1 мин | SHORT 15 мин |
|---|---|---|---|---|
| Favourable win rate | 69.2% (9/13) | 61.5% (8/13) | 82.4% (14/17) | 82.4% (14/17) |
| Avg favourable | +0.358% | +0.331% | -0.501% | -0.449% |
| Avg adverse | -0.280% | -0.350% | +0.250% | +0.204% |

★ 1 минута лучше 15 минут по favourable movement
★ 15 минут добавляют adverse range (убыток сильнее при ложном сигнале)
★ Шорты надёжнее лонгов (82.4% vs 69.2% favourable)

### Исторический базовый уровень MX (все 186 дней, без фильтра B)

**Разница от mx_close (среднее):**

| Метрика | pts | % |
|---|---|---|
| HIGH 1min | +225.5 | +0.088% |
| HIGH 15min | +335.6 | +0.134% |
| LOW 1min | -95.4 | -0.052% |
| LOW 15min | -86.7 | -0.055% |

**Разница от mx_close (медиана):**

| Метрика | pts | % |
|---|---|---|
| HIGH 1min | +150.0 | +0.056% |
| HIGH 15min | +250.0 | +0.105% |
| LOW 1min | -112.5 | -0.048% |
| LOW 15min | 0.0 | 0.000% |

★ Утренний дрейф вверх — структурный: high 1m = +225 pts, low 1m = -95 pts (в 2.4 раза сильнее вверх)
★ 15 минут добавляют только верх: high расширяется +49%, low почти не меняется
★ Медиана LOW 15m = 0: в половине дней цена не уходила ниже закрытия

### Смена режима по контрактам (среднее, pts)

| Контракт | Дней | HIGH 1m | HIGH 15m | LOW 1m | LOW 15m |
|---|---|---|---|---|---|
| MXH6 | 50 | +329.5 | +418.5 | +224.0 | +334.5 |
| MXM6 | 63 | +217.5 | +270.2 | +98.0 | +236.9 |
| MXU6 | 65 | +121.2 | +283.8 | -526.2 | -708.5 |
| MXZ6 | 8 | +487.5 | +753.1 | -115.6 | -215.6 |

★ MXH6/MXM6 (первое полугодие) — low положительный, бычий режим. Цена не уходила ниже закрытия.
★ MXU6 (июнь-сентябрь) — low резко отрицательный (-526/-708), медвежий режим.
★ 77% сильных сделок (|B| >= 0.5) из MXU6 — результаты бэктеста могут быть артефактом одного волатильного периода (грабля #205).

### Качество 15-минутных данных (грабля #201)

★ 57.5% строк V13 имеют flat OHLC (open==high==low==close — нет диапазона)
★ В 48 случаях 15-min HIGH ниже 1-min HIGH — математически невозможно
★ Причина: ISS 15-min aggregation для ранних утренних свечей возвращает обобщённую свечу
★ Решение: агрегировать из 1-мин свечей вручную, НЕ использовать ISS 15-min endpoint напрямую

### Метрики качества стратегии (|B| >= 0.5, V51, выход по TP)

| Метрика | Значение |
|---|---|
| Profit factor | 4.63 |
| Max drawdown | -0.91% |
| Max win streak | 9 |
| Max loss streak | 2 |
| Expectancy | +0.145% |
| Sharpe-like (per trade) | 0.48 |

### Ключевые выводы

1. **Проблема не в направлении, а в точке выхода** (грабля #203). Mean-reversion существует внутри 15 минут, но разворачивается к закрытию. TP по best price = +5.93% net, close = -0.65%.
2. **Асимметрия лонг/шорт — структурная** (грабля #204). Падение вечером → отскок утром (лонги). Рост вечером → продолжение (шорты по close не работают, но по TP — работают).
3. **Порог |B| >= 0.5 — реальная граница** (грабля #202). Ниже — шум, win rate < 50%.
4. **1 минута лучше 15 минут** по favourable movement. Дополнительные 14 минут добавляют adverse, не favourable.
5. **Смена режима по контрактам** (грабля #205). Результаты могут быть артефактом MXU6. Нужна валидация на большем периоде.
6. **30 сделок — мало для статистики** (9 месяцев). Profit factor 4.63 может быть случайным.
7. **Slippage 0.05%** съедает 35% прибыли (net падает с +4.34% до +2.84% при round-trip close).
8. **Корреляция B ↔ gap = -0.28** — слабая. B объясняет лишь ~8% дисперсии гэпа.

### Связка с другими разделами

| Связь | Раздел | Описание |
|-------|--------|----------|
| Механика гэпа | 44.6 | Формула B, порог (обновлён: 0.5 для торговли) |
| Бэктест через ISS | 44.9 | Источник данных, формула, логика |
| Rolling-бэктест | 44.10 | Генерация истёкших контрактов |
| Качество данных | 19 | Грабля #201 (15-min flat OHLC) |
| Порог | 19 | Грабля #202 (|B| 0.3 — шум) |
| Точка выхода | 19 | Грабля #203 (close убивает прибыль) |
| Асимметрия | 19 | Грабля #204 (лонг/шорт структурная) |
| Смена режима | 19 | Грабля #205 (контракты) |

# КОНЕЦ