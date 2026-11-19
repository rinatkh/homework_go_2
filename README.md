# Homework 2: переменные, типы и память

Домашка повторяет формат classroom2: одна тема — один `main`, один `internal` package и тесты.

## Структура

```text
homework_go_2
├── cmd
│   ├── 01_integer/main.go
│   ├── 02_bases_bytes/main.go
│   ├── 03_float/main.go
│   ├── 04_boolean/main.go
│   ├── 05_text/main.go
│   ├── 06_constants/main.go
│   ├── 07_conversion/main.go
│   ├── 08_pointers/main.go
│   ├── 09_calculator/main.go
│   ├── 10_profile/main.go
│   └── 11_order/main.go
├── internal
│   ├── integer
│   ├── basesbytes
│   ├── float
│   ├── boolean
│   ├── text
│   ├── constants
│   ├── conversion
│   ├── pointers
│   ├── calculator
│   ├── profile
│   └── order
├── test/integration
├── docs/task.md
├── Makefile
└── .github/workflows/ci.yml
```

## Правило проекта

`main.go` не содержит логику. Он только вызывает `Example()` из нужного `internal` package и печатает результат.

Логику нужно писать в функциях внутри `internal/<topic>`.

## Объём и стартовое состояние

123 функции: BASIC — 24 обязательных, PRACTICE — 88 дополнительных, CHALLENGE — 11 повышенной сложности. Ещё семь TODO-групп констант; BASIC использует две из них. Классификация каждой функции находится в [docs/task.md](docs/task.md). Все TODO остаются для самостоятельного решения.

Go 1.22+, Make, Git. Module: `github.com/rinatkh/homework_go_2`. От classroom нет импортов. Starter компилируется, а функциональные тесты должны показывать отсутствие реализации.

```bash
make starter-check
make test-basic
make ci-basic
```

Первый вызов должен пройти, два следующих станут зелёными после решения BASIC. `make ci` оставлен для полностью решённого банка. Тематический test-* проверяет тему целиком, включая дополнительные задания.

## Как работать

1. Откройте `docs/task.md`.
2. Выберите тему, например `integer`.
3. Откройте `internal/integer/integer.go`.
4. Реализуйте функции BASIC с `TODO`, остальные уровни — дополнительно.
5. Запустите тесты конкретной темы.

```bash
make test-integer
make run-integer
```

Когда тема готова, переходите к следующей.

## Основные команды

```bash
make help
make compile
make test-unit
make test-integration
make coverage-check
make build
make ci
```

## Команды по отдельным темам

```bash
make run-integer
make test-integer

make run-bases
make test-bases

make run-float
make test-float

make run-boolean
make test-boolean

make run-text
make test-text

make run-constants
make test-constants

make run-conversion
make test-conversion

make run-pointers
make test-pointers

make run-calculator
make test-calculator

make run-profile
make test-profile

make run-order
make test-order
```

## Сдача и CI

Fork → clone → ветка homework-2 → README и docs/task.md → небольшие решения и commits → локальные проверки → push → Pull Request → CI → ревью. Base PR: `rinatkh/homework_go_2`, ветка `main`; head: ваш fork, `homework-2`.

Обычный push/PR запускает BASIC, общий fmt/vet, tidy и сборку всех 11 команд. После полного решения выполнить `make ci`, затем вручную запустить GitHub Actions через workflow_dispatch с profile=full. Полный профиль сохраняет unit/integration/race/coverage и package. CLI Examples и покрытие всего банка не блокируют частично решённый BASIC.

В Git mod-check сравнивает go.mod/go.sum с HEAD. После применения патча сделайте commit инфраструктурных изменений перед полным CI. `make package` собирает Linux/amd64, `make build` — текущую платформу. Установку Go и Git workflow повторно изучать не требуется.

