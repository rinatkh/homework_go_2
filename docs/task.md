# Задание 2: переменные, типы и память

## Объём и уровни

Банк содержит **123 функции**: **BASIC — 24**, **PRACTICE — 88**, **CHALLENGE — 11**. Ещё семь TODO относятся к группам констант (всего 130 TODO-маркеров). BASIC требует maxAttempts и блок статусов; остальные пять групп const дополнительные. Сигнатуры, пакеты и заготовки сохраняются.

BASIC напрямую закрепляет урок. PRACTICE усложняет последовательность действий. CHALLENGE соединяет темы или требует обхода последовательности; ReverseRunes, IsPalindrome, JoinWithComma и Initials не обязательны после этой встречи.

Числовые преобразования предполагают представимость результата в целевом типе. Для ReplaceFirstRune аргумент r задан допустимой кодовой точкой Unicode.

Все текстовые задания работают с валидным UTF-8 и Unicode code points, если явно не указано ASCII. Rune не равна графемному кластеру. Float-входы конечны, не NaN/Inf; ожидаемые результаты также представимы. Обычная целая арифметика предполагает представимые промежуточные результаты; CountPages дополнительно должен работать вплоть до MaxInt без переполнения формулы округления.

`make starter-check` проверяет форматирование, vet и компиляцию. Это не принятие TODO. `make test-basic` и `make ci-basic` принимают только BASIC, включая граничные проверки. `make ci` проверяет весь банк, все CLI Examples, race, покрытие 80% и сборку. Тематические тесты могут включать задания всех уровней.

## Цель

Закрепить базовые типы Go, арифметику, логические выражения, строки и Unicode, константы, преобразования типов, обработку ошибок и указатели.

В проекте каждая тема разделена на три части:

- `internal/<topic>/<topic>.go` — функции-заготовки с `TODO`, которые нужно реализовать;
- `internal/<topic>/<topic>_test.go` — unit-тесты;
- `cmd/<topic>/main.go` — запуск демонстрационного примера через `Example()`.

Логику нужно писать только в файлах `internal/<topic>/<topic>.go`. Изменять сигнатуры функций, готовые тесты и `main.go` не нужно.

## Как выполнять

1. Выберите один раздел и прочитайте таблицу с требованиями.
2. Откройте указанный файл в `internal`.
3. Начните с функций BASIC; остальные уровни выбирайте дополнительно.
4. Запустите unit-тесты раздела.
5. После BASIC запустите make ci-basic. CLI Example может использовать дополнительные функции; полный вывод проверяется после всего раздела.
6. После выполнения всех разделов запустите `make ci`.

---

## 01. Integer

Файл: `internal/integer/integer.go`

| Функция | Ввод | Вывод и правила | Уровень |
|---|---|---|---|
| `Add` | `a`, `b` — два `int` | Сумма `a` и `b`. | BASIC |
| `Subtract` | `a`, `b` — два `int` | Разность: из `a` вычитается `b`. | PRACTICE |
| `Multiply` | `a`, `b` — два `int` | Произведение `a` и `b`. | PRACTICE |
| `Divide` | `a` — делимое, `b` — делитель | Результат целочисленного деления. При `b == 0` вернуть `0`. | BASIC |
| `Remainder` | `a` — делимое, `b` — делитель | Остаток от целочисленного деления. При `b == 0` вернуть `0`; для отрицательных значений сохранить стандартное поведение Go. | BASIC |
| `IsEven` | `n` — `int` | `true`, если число чётное, иначе `false`. Ноль считается чётным. | BASIC |
| `LastDigit` | `n` — `int` | Последняя десятичная цифра числа как неотрицательное значение от `0` до `9`. Например, для `-987` вернуть `7`. | PRACTICE |
| `Max` | `a`, `b` — два `int` | Большее значение; при равенстве вернуть это же значение. | PRACTICE |
| `Min` | `a`, `b` — два `int` | Меньшее значение; при равенстве вернуть это же значение. | PRACTICE |
| `Clamp` | `value`, `min`, `max` | Если `value < min`, вернуть `min`; если `value > max`, вернуть `max`; иначе вернуть `value`. Считайте, что `min <= max`. | PRACTICE |
| `SumThree` | `a`, `b`, `c` — три `int` | Сумма трёх значений. | PRACTICE |
| `Average` | `a`, `b` — два `int` | Среднее арифметическое с целочисленным результатом; дробная часть отбрасывается по правилам Go. | PRACTICE |
| `IntToInt64` | `n` — `int` | То же числовое значение типа `int64`. | PRACTICE |
| `NonNegativeToUint` | `n` — `int` | Для `n >= 0` вернуть значение типа `uint`; для отрицательного `n` вернуть `0`. | PRACTICE |
| `CountPages` | `totalItems` — число элементов, `pageSize` — размер страницы | Количество страниц с округлением вверх. При `totalItems <= 0` или `pageSize <= 0` вернуть `0`. | BASIC |

Проверка:

```bash
make test-integer
make run-integer
```

---

## 02. Bases / Byte

Файл: `internal/basesbytes/basesbytes.go`

| Функция | Ввод | Вывод и правила | Уровень |
|---|---|---|---|
| `Decimal42` | Нет | Число `42`, записанное десятичным литералом. | PRACTICE |
| `Hex2A` | Нет | Число `42`, записанное шестнадцатеричным литералом. | PRACTICE |
| `Binary101010` | Нет | Число `42`, записанное двоичным литералом. | PRACTICE |
| `Octal52` | Нет | Число `42`, записанное восьмеричным литералом. | PRACTICE |
| `SameNumber` | Нет | `true`, если значения четырёх функций выше равны между собой и равны `42`. | PRACTICE |
| `MaxByte` | Нет | Максимальное значение типа `byte`: `255`. | BASIC |
| `FormatDecimal` | `n` — `uint64` | Десятичная запись числа без префикса, например `42` → `"42"`. | BASIC |
| `FormatBinary` | `n` — `uint64` | Двоичная запись без префикса, например `42` → `"101010"`. | BASIC |
| `FormatOctal` | `n` — `uint64` | Восьмеричная запись без префикса, например `42` → `"52"`. | PRACTICE |
| `FormatHex` | `n` — `uint64` | Шестнадцатеричная запись без префикса и с буквами в нижнем регистре, например `42` → `"2a"`. | PRACTICE |
| `FormatAllBases` | `n` — `uint64` | Строка формата `dec=<decimal> bin=<binary> oct=<octal> hex=<hex>`. Для `42`: `dec=42 bin=101010 oct=52 hex=2a`. | PRACTICE |
| `IsASCII` | `b` — `byte` | `true` для значений от `0` до `127` включительно, иначе `false`. | PRACTICE |
| `ToUpperASCII` | `b` — `byte` | Строчную латинскую ASCII-букву `a-z` заменить на соответствующую `A-Z`; остальные значения вернуть без изменений. | PRACTICE |
| `ToLowerASCII` | `b` — `byte` | Заглавную латинскую ASCII-букву `A-Z` заменить на соответствующую `a-z`; остальные значения вернуть без изменений. | PRACTICE |
| `PackTwoBytes` | `high`, `low` — два `byte` | Значение `uint16`, в котором `high` занимает старшие 8 бит, а `low` — младшие 8 бит. Например, `(1, 2)` → `258`. | CHALLENGE |

Проверка:

```bash
make test-bases
make run-bases
```

---

## 03. Float

Файл: `internal/float/float.go`

| Функция | Ввод | Вывод и правила | Уровень |
|---|---|---|---|
| `Add` | `a`, `b` — два `float64` | Сумма значений. | PRACTICE |
| `Subtract` | `a`, `b` — два `float64` | Разность: из `a` вычитается `b`. | PRACTICE |
| `Multiply` | `a`, `b` — два `float64` | Произведение значений. | PRACTICE |
| `Divide` | `a` — делимое, `b` — делитель | Результат дробного деления. При `b == 0` вернуть `0`. | PRACTICE |
| `DiscountPrice` | `price` — цена, `percent` — скидка в процентах | Цена после скидки. Отрицательная скидка не изменяет цену; скидка `100%` и выше даёт цену `0`. | PRACTICE |
| `AddTax` | `price` — цена, `taxPercent` — налог в процентах | Цена после добавления налога. Отрицательный налог не изменяет цену. | BASIC |
| `CelsiusToFahrenheit` | Температура в °C | Температура в °F по стандартному соотношению шкал. Контрольные точки: `0°C` → `32°F`, `100°C` → `212°F`. | PRACTICE |
| `FahrenheitToCelsius` | Температура в °F | Температура в °C. Контрольные точки: `32°F` → `0°C`, `212°F` → `100°C`. | PRACTICE |
| `Average` | `a`, `b` — два `float64` | Среднее арифметическое двух значений. | BASIC |
| `Round2` | `value` — `float64` | Число, округлённое до двух знаков после десятичной точки. Например, `12.345` → `12.35`. | PRACTICE |
| `FormatPrice` | `price` — `float64` | Строка ровно с двумя знаками после точки: `12.3` → `"12.30"`, `100` → `"100.00"`. | PRACTICE |
| `PercentOf` | `total`, `percent` | Указанный процент от `total`; отрицательный процент даёт отрицательный результат. | PRACTICE |
| `GrowthPercent` | `oldValue`, `newValue` | Процентное изменение от старого значения к новому. Уменьшение даёт отрицательный результат; при `oldValue == 0` вернуть `0`. | CHALLENGE |
| `IsPositive` | `value` — `float64` | `true` только для значения строго больше нуля. | PRACTICE |
| `FloatToInt` | `value` — `float64` | Значение типа `int`; дробная часть отбрасывается в сторону нуля. Например, `-12.99` → `-12`. | PRACTICE |

Проверка:

```bash
make test-float
make run-float
```

---

## 04. Boolean

Файл: `internal/boolean/boolean.go`

| Функция | Ввод | Вывод и правила | Уровень |
|---|---|---|---|
| `CanEnter` | `age`, `hasTicket` | `true`, только если возраст не меньше `18` и билет есть. | BASIC |
| `IsAdult` | `age` | `true` при `age >= 18`, иначе `false`. | PRACTICE |
| `CanBuyAlcohol` | `age` | В рамках задания покупка разрешена при `age >= 18`. | PRACTICE |
| `CanRest` | `isWeekend`, `isHoliday` | `true`, если установлен хотя бы один из флагов. | BASIC |
| `IsWorkingDay` | `day` — строка на английском в нижнем регистре | `true` для `monday`, `tuesday`, `wednesday`, `thursday`, `friday`; для `saturday`, `sunday` и неизвестных значений — `false`. | PRACTICE |
| `HasAccess` | `isAdmin`, `isOwner` | `true`, если пользователь администратор или владелец. | PRACTICE |
| `CanApplyDiscount` | `isVIP`, `total` | `true`, если пользователь VIP или сумма заказа не меньше `5000`. | PRACTICE |
| `ShouldNotify` | `emailVerified`, `notificationsEnabled` | `true`, только если email подтверждён и уведомления включены. | PRACTICE |
| `IsValidScore` | `score` | `true` для диапазона от `0` до `100` включительно. | PRACTICE |
| `IsInRange` | `value`, `min`, `max` | `true`, если `value` находится в диапазоне `[min, max]`, включая обе границы. | PRACTICE |
| `IsLeapYear` | `year` | Результат по календарному правилу: год кратен `400` либо кратен `4`, но не кратен `100`. | BASIC |
| `CanWithdraw` | `balance`, `amount`, `blocked` | `true`, если аккаунт не заблокирован, `amount > 0` и суммы на балансе достаточно. | PRACTICE |
| `LoginAllowed` | `passwordOK`, `otpOK` | `true`, только если успешно пройдены обе проверки. | PRACTICE |
| `IsEmpty` | `text` | `true` только для строки длиной `0`; строка из пробелов или перевода строки не считается пустой. | PRACTICE |
| `Not` | `flag` | Противоположное логическое значение. | PRACTICE |

Проверка:

```bash
make test-boolean
make run-boolean
```

---

## 05. Text

Файл: `internal/text/text.go`

| Функция | Ввод | Вывод и правила | Уровень |
|---|---|---|---|
| `ByteLen` | `s` — строка | Размер строки в байтах. Например, `"Привет"` занимает `12` байт. | BASIC |
| `RuneLen` | `s` — строка | Количество кодовых точек Unicode. Например, в `"Привет"` — `6` кодовых точек. | BASIC |
| `FirstRune` | `s` — строка | Первая кодовая точка Unicode как строка; для пустой строки вернуть `""`. | PRACTICE |
| `LastRune` | `s` — строка | Последняя кодовая точка Unicode как строка; для пустой строки вернуть `""`. | PRACTICE |
| `Trim` | `s` — строка | Строка без пробельных символов по краям; внутренние символы не изменяются. | PRACTICE |
| `ToLower` | `s` — строка | Строка в нижнем регистре с поддержкой Unicode. | PRACTICE |
| `ToUpper` | `s` — строка | Строка в верхнем регистре с поддержкой Unicode. | PRACTICE |
| `NormalizeEmail` | `email` — строка | Удалить пробельные символы по краям и привести всю строку к нижнему регистру. | BASIC |
| `ContainsWord` | `text`, `word` | `true`, если `word` встречается внутри `text`. Поиск чувствителен к регистру; пустая подстрока считается найденной. | PRACTICE |
| `ReplaceFirstRune` | `s` — строка, `r` — новая `rune` | Новая строка с заменённой первой кодовой точкой Unicode; для пустой строки вернуть `""`. | BASIC |
| `ReverseRunes` | `s` — строка | Строка, развёрнутая по кодовым точкам Unicode. UTF-8 остаётся валидным, но составные графемы могут распасться. | CHALLENGE |
| `Initials` | `firstName`, `lastName` | Первые кодовые точки Unicode очищенных имён в верхнем регистре, без разделителя. Пустая часть пропускается: `("", "Ivanova")` → `"I"`. | CHALLENGE |
| `RepeatWord` | `word`, `count` | `word`, повторённое `count` раз без разделителя; при `count <= 0` вернуть `""`. | PRACTICE |
| `JoinWithComma` | `values` — `[]string` | Все элементы в исходном порядке через `,` без дополнительных пробелов; пустой или `nil`-срез даёт `""`. | CHALLENGE |
| `IsPalindrome` | `s` — строка | Сравнить строку без учёта регистра и пробелов. Кириллица должна поддерживаться; строка только из пробелов считается палиндромом. | CHALLENGE |

Проверка:

```bash
make test-text
make run-text
```

---

## 06. Constants / iota / switch

Файл: `internal/constants/constants.go`

### Константы

| Константы | Требование | Уровень |
|---|---|---|
| `appName` | Значение `"go-homework-2"`. | PRACTICE |
| `maxAttempts` | Значение `3`. | BASIC |
| `StatusNew`, `StatusPaid`, `StatusCanceled` | Последовательные значения `0`, `1`, `2`. | BASIC |
| `RoleGuest`, `RoleUser`, `RoleAdmin` | Последовательные значения `0`, `1`, `2`. | PRACTICE |
| `PriorityLow`, `PriorityMedium`, `PriorityHigh` | Последовательные значения `1`, `2`, `3`; значение `0` считается неизвестным. | PRACTICE |
| `EventCreated`, `EventUpdated`, `EventDeleted` | Три различных последовательных значения в указанном порядке. | PRACTICE |

### Функции

| Функция | Ввод | Вывод и правила | Уровень |
|---|---|---|---|
| `AppName` | Нет | Значение константы `appName`. | PRACTICE |
| `MaxAttempts` | Нет | Значение константы `maxAttempts`. | BASIC |
| `StatusText` | `status` | `new`, `paid`, `canceled`; для неизвестного значения — `unknown`. | BASIC |
| `IsFinalStatus` | `status` | `true` для `StatusPaid` и `StatusCanceled`; для нового и неизвестного статуса — `false`. | PRACTICE |
| `NextStatus` | `status` | Новый статус переходит в оплаченный; оплаченный и отменённый не меняются; неизвестный превращается в `StatusNew`. | PRACTICE |
| `RoleText` | `role` | `guest`, `user`, `admin`; для неизвестного значения — `unknown`. | PRACTICE |
| `CanEdit` | `role` | `true` только для `RoleAdmin`. | PRACTICE |
| `HTTPStatusText` | HTTP-код | `200` → `OK`, `201` → `Created`, `400` → `Bad Request`, `404` → `Not Found`; остальные → `Unknown`. | PRACTICE |
| `DayType` | Номер дня: `1` — понедельник, `7` — воскресенье | `working` для `1...5`, `weekend` для `6...7`, иначе `unknown`. | PRACTICE |
| `PriorityText` | `priority` | `low`, `medium`, `high`; для неизвестного значения — `unknown`. | PRACTICE |
| `IsKnownStatus` | `status` | `true` только для трёх объявленных статусов. | PRACTICE |
| `PaymentStateText` | `paid`, `canceled` | `canceled`, если отмена установлена; иначе `paid`, если оплата установлена; иначе `pending`. | PRACTICE |
| `TrafficLightAction` | `color` | `red` → `stop`, `yellow` → `wait`, `green` → `go`; иначе `unknown`. | PRACTICE |
| `GradeText` | `score` | Вне `0...100` → `invalid`; `90...100` → `excellent`; `75...89` → `good`; `50...74` → `passed`; `0...49` → `retry`. | PRACTICE |
| `EventTypeText` | `eventType` | `created`, `updated`, `deleted`; для неизвестного значения — `unknown`. | PRACTICE |

Проверка:

```bash
make test-constants
make run-constants
```

---

## 07. Conversion / named types / strconv

Файл: `internal/conversion/conversion.go`

| Функция | Ввод | Вывод и правила | Уровень |
|---|---|---|---|
| `IntToInt64` | `n` — `int` | То же числовое значение типа `int64`. | PRACTICE |
| `Int64ToInt` | `n` — `int64` | То же числовое значение типа `int`; переполнение в этой задаче не обрабатывается. | PRACTICE |
| `RubToKop` | `rub` — `Rub` | Количество копеек типа `Kop`; один рубль равен `100` копейкам. Отрицательные значения сохраняют знак. | PRACTICE |
| `KopToRub` | `kop` — `Kop` | Целое количество рублей типа `Rub`; неполные рубли отбрасываются. | PRACTICE |
| `UserIDToString` | `id` — `UserID` | Десятичная строка с идентификатором. | PRACTICE |
| `ParseInt` | `text` — строка | Успешно распарсенное `int` и `nil`; для пустой или некорректной строки — ненулевая ошибка. | PRACTICE |
| `ParseAndDouble` | `text` — строка | Распарсенное число, умноженное на `2`; ошибку парсинга нужно вернуть вызывающему коду. | BASIC |
| `IntToString` | `n` — `int` | Десятичная строка со значением. | PRACTICE |
| `FloatToString` | `value` — `float64` | Строка ровно с двумя знаками после точки и округлением: `12.345` → `"12.35"`. | PRACTICE |
| `ParseBoolText` | `text` — строка | Поддержать стандартные значения `"true"`, `"false"`, `"1"`, `"0"`; для неподдерживаемой строки вернуть ошибку. | PRACTICE |
| `BoolToText` | `value` — `bool` | `"true"` или `"false"`. | PRACTICE |
| `SumIntAndInt64` | `a` — `int`, `b` — `int64` | Сумма типа `int64`. | BASIC |
| `PriceRubStringToKop` | Строка с целым числом рублей | Для неотрицательного числа вернуть цену типа `Kop`; некорректная или отрицательная цена должна вернуть ошибку. | CHALLENGE |
| `SafeParsePositive` | `text` — строка | Положительное целое число; для нуля, отрицательного числа, пустой или некорректной строки вернуть `0`. | PRACTICE |
| `FormatUser` | `id` — `UserID`, `name` — строка | Строка формата `user:<id>:<name>`, например `user:1001:Maria`. Пустое имя допустимо. | PRACTICE |

Проверка:

```bash
make test-conversion
make run-conversion
```

---

## 08. Pointers

Файл: `internal/pointers/pointers.go`

| Функция | Ввод | Вывод и правила | Уровень |
|---|---|---|---|
| `ValueOrDefault` | `p` — `*int`, `def` — значение по умолчанию | Значение по адресу; если `p == nil`, вернуть `def`. Нулевое значение по ненулевому указателю не заменяется. | BASIC |
| `Increment` | `p` — `*int` | Увеличить исходное значение на `1` и вернуть новый результат; при `nil` вернуть `0`. | BASIC |
| `SetValue` | `p` — `*int`, `value` | Записать новое значение и вернуть `true`; при `nil` вернуть `false`. | PRACTICE |
| `Swap` | `a`, `b` — два `*int` | Поменять значения местами и вернуть `true`; если хотя бы один указатель `nil`, ничего не менять и вернуть `false`. | PRACTICE |
| `ResetToZero` | `p` — `*int` | Записать `0` и вернуть `true`; при `nil` вернуть `false`. | PRACTICE |
| `AddToValue` | `p` — `*int`, `delta` | Прибавить `delta` к исходному значению и вернуть результат; при `nil` вернуть `0`. | PRACTICE |
| `MaxPointer` | `a`, `b` — два `*int` | Указатель на большее значение; при равенстве — `a`; если один указатель `nil`, вернуть второй; если оба `nil`, вернуть `nil`. | PRACTICE |
| `IsNil` | `p` — `*int` | `true`, если указатель равен `nil`. | PRACTICE |
| `CopyValue` | `p` — `*int` | Копия значения; при `nil` вернуть `0`. Изменять исходное значение не нужно. | PRACTICE |
| `DoubleInPlace` | `p` — `*int` | Умножить исходное значение на `2` и вернуть `true`; при `nil` вернуть `false`. | PRACTICE |
| `NewInt` | `value` — `int` | Ненулевой указатель на новое значение, равное `value`. | BASIC |
| `DivideInto` | `out` — `*int`, `a`, `b` | Записать в `out` результат целочисленного деления и вернуть `true`. При `out == nil` или `b == 0` вернуть `false`; существующее значение `out` не менять. | PRACTICE |
| `ApplyDiscountInPlace` | `price` — `*int`, `percent` | Применить целочисленную скидку и вернуть `true`. При `percent >= 100` записать `0`; при отрицательном проценте или `nil` вернуть `false` и не менять цену. | CHALLENGE |
| `ChoosePointer` | `primary`, `fallback` | Вернуть `primary`, если он не `nil`; иначе вернуть `fallback`. Значение по адресу, включая `0`, не влияет на выбор. | PRACTICE |
| `PointToLarger` | `a`, `b` — два `*int` | Те же правила выбора, что у `MaxPointer`: большее значение, при равенстве первый указатель, безопасная обработка `nil`. | PRACTICE |

Проверка:

```bash
make test-pointers
make run-pointers
```

---

## 09. Calculator [CHALLENGE]

Файл: `internal/calculator/calculator.go`

| Функция | Ввод | Вывод и правила | Уровень |
|---|---|---|---|
| `Calculate` | `a`, `b` — `int`; `operation` — одна из строк `+`, `-`, `*`, `/`, `%` | Вернуть результат выбранной операции и `nil`. Деление выполняется как целочисленное. Для `/` или `%` при `b == 0`, а также для неизвестной или пустой операции вернуть ошибку. | CHALLENGE |

Примеры:

| Ввод | Вывод |
|---|---|
| `Calculate(10, 5, "+")` | `15, nil` |
| `Calculate(17, 5, "/")` | `3, nil` |
| `Calculate(17, 5, "%")` | `2, nil` |
| `Calculate(1, 0, "/")` | Ошибка |
| `Calculate(1, 2, "add")` | Ошибка |

Проверка:

```bash
make test-calculator
make run-calculator
```

---

## 10. Profile [CHALLENGE]

Файл: `internal/profile/profile.go`

| Функция | Ввод | Вывод и правила | Уровень |
|---|---|---|---|
| `BuildUserCard` | `name` — строка, `age` — `int`, `active` — `bool` | Вернуть строку `name=<name> age=<age> group=<group> status=<status>`. Имя очистить по краям, привести к нижнему регистру и сделать первый символ заглавным; пустое имя заменить на `Unknown`. `group=adult` при `age >= 18`, иначе `group=minor`. `status=active` при `active == true`, иначе `status=inactive`. | CHALLENGE |

Примеры:

| Ввод | Вывод |
|---|---|
| `BuildUserCard("  MARIA  ", 20, true)` | `name=Maria age=20 group=adult status=active` |
| `BuildUserCard("ivan", 17, false)` | `name=Ivan age=17 group=minor status=inactive` |
| `BuildUserCard("   ", 30, false)` | `name=Unknown age=30 group=adult status=inactive` |

Проверка:

```bash
make test-profile
make run-profile
```

---

## 11. Order [CHALLENGE]

Файл: `internal/order/order.go`

### Константы статусов

`StatusNew`, `StatusPaid`, `StatusCanceled` должны иметь последовательные значения `0`, `1`, `2` в указанном порядке.

| Функция | Ввод | Вывод и правила | Уровень |
|---|---|---|---|
| `OrderSummary` | `status` — статус заказа, `priceRub` — цена в целых рублях, `paid` — флаг оплаты | Вернуть строку `status=<status_text> payment=<payment_text> price_kop=<price>`. Статусы: `new`, `paid`, `canceled`, неизвестный → `unknown`. Оплата: `paid` при `true`, иначе `not_paid`. Цену перевести в копейки; отрицательную цену считать равной `0`. | CHALLENGE |

Примеры:

| Ввод | Вывод |
|---|---|
| `OrderSummary(StatusPaid, 1200, true)` | `status=paid payment=paid price_kop=120000` |
| `OrderSummary(StatusNew, 500, false)` | `status=new payment=not_paid price_kop=50000` |
| `OrderSummary(99, -100, false)` | `status=unknown payment=not_paid price_kop=0` |

Проверка:

```bash
make test-order
make run-order
```

---

## Финальная проверка

После реализации всех задач выполните:

```bash
make ci
```

Работа считается завершённой, когда проходят unit-тесты, integration-тесты, форматирование, `go vet`, проверка покрытия и сборка всех программ.
