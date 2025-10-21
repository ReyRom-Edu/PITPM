# Лекция: GitHub Actions для автоматизированного тестирования ПО

**GitHub Actions** — это встроенный инструмент автоматизации, который позволяет создавать рабочие процессы (workflows) для автоматического выполнения задач при изменениях в репозитории. Одно из ключевых применений — автоматизированное тестирование программного обеспечения.

## Основные понятия

- **Workflow** — последовательность шагов, которые выполняются при определённых событиях (например, push или pull request).
- **Job** — набор шагов, выполняющихся на одном runner.
- **Step** — отдельное действие внутри job, например, установка зависимостей или запуск тестов.
- **Runner** — сервер, на котором выполняются jobs.

## Преимущества использования GitHub Actions

- **Интеграция с GitHub** — не требует сторонних сервисов.
- **Гибкость** — поддержка различных языков и платформ.
- **Масштабируемость** — параллельное выполнение jobs.
- **Прозрачность** — результаты тестов видны прямо в pull request.

## Пример рабочего процесса для тестирования

```yaml
name: .NET Autotests

on:
    push:
        branches: ["master"]
    pull_request:
        branches: ["master"]

jobs:
    build-and-test:
        runs-on: ubuntu-latest

        steps:
          - name: Checkout repository
            uses: actions/checkout@v4

          - name: Setup .NET
            uses: actions/setup-dotnet@v4
            with:
                dotnet-version: '8.0.x'

          - name: Restore dependencies
            run: dotnet restore

          - name: Build solution
            run: dotnet build --no-restore --configuration Release

          - name: Run tests and generate TRX log
            run: dotnet test --no-build --configuration Release --logger "trx;LogFileName=test_results.trx"

          - name: Generate Report
            uses: dorny/test-reporter@v2
            if: success() || failure()
            with:
                name: Test results
                path: "**/*.trx"
                reporter: dotnet-trx
        
```

Это файл GitHub Actions (workflow) для запуска сборки и автотестов .NET-проекта. Он запускается на `push` и `pull_request` в ветку `master`, поднимает среду .NET 8, восстанавливает зависимости, собирает решение, запускает тесты и отправляет TRX-отчёты в `dorny/test-reporter`.

Ниже подробнее разберем все части данного файла

---

```yaml
name: .NET Autotests
```

Имя workflow — отображается в UI GitHub Actions.

---

```yaml
on:
    push:
        branches: ["master"]
    pull_request:
        branches: ["master"]
```

Workflow запускается при следующих действиях:

* `push` в ветку `master`.
* `pull_request` с целью в `master`.

Также для запуска можно добавить фильтрацию по путям (`paths` и `paths-ignore`) если нужно запускать только при изменении кода/тестов.

```yaml
on:
  push:
    paths:
      - '**.cs'
```
Workflow с такими параметрами запуска будет выполняться при загрузке в репозиторий файлов кода C#

```yaml
    paths-ignore:
      - '**/README.md'
```
Workflow с такими параметрами запуска не будет выполняться при загрузке в репозиторий файла README.md

---

```yaml
jobs:
    build-and-test:
        runs-on: ubuntu-latest
```

Один джоб `build-and-test`, выполняется на образе `ubuntu-latest`. [Подробнее о доступных вариантах запуска](https://docs.github.com/en/actions/reference/workflows-and-actions/workflow-syntax#jobsjob_idruns-on)

---

```yaml
        steps:
          - name: Checkout repository
            uses: actions/checkout@v4
```

Шаг checkout — клонирует репозиторий на рабочую машину раннера.

---

```yaml
          - name: Setup .NET
            uses: actions/setup-dotnet@v4
            with:
                dotnet-version: '8.0.x'
```

Устанавливает .NET SDK версии 8.0.x. Формат `8.0.x` позволяет брать последнюю минорную/патч-версию 8.0.

---

```yaml
          - name: Restore dependencies
            run: dotnet restore
```

Восстанавливает NuGet-пакеты для решения/проекта(ов). Если решение находится в подкаталоге — нужно указать `working-directory` или путь к `.sln`.
```yaml
            working-directory: src/MySolutionFolder
```

---

```yaml
          - name: Build solution
            run: dotnet build --no-restore --configuration Release
```

Собирает решение в конфигурации Release. Флаг `--no-restore` используется, потому что restore выполнён заранее — экономит время.

---

```yaml
          - name: Run tests and generate TRX log
            run: dotnet test --no-build --configuration Release --logger "trx;LogFileName=test_results.trx" --results-directory ./TestResults
```

Запускает тесты и генерирует TRX-файл логов. Флаг `--no-build` используется потому что мы собрали ранее; если тесты всё же требуют сборки, можно опустить `--no-build`. По умолчанию `dotnet test` создаст TRX рядом с проектом поэтому лучше явно указать `--results-directory` для хранения отчетов о тестировании в одном месте.

---

```yaml
          - name: Generate Report
            uses: dorny/test-reporter@v2
            if: success() || failure()
            with:
                name: Test results
                path: "**/*.trx"
                reporter: dotnet-trx
```

Шаг, который агрегирует TRX-отчёты и показывает сводку.

* `if: success() || failure()` — шаг выполнится и при успехе, и при провале тестов (нужно, чтобы получить отчёт даже при падении).
* `path: "**/*.trx"` — glob ищет все TRX-файлы в репозитории; это удобно если у вас несколько тест-проеков.
* `reporter: dotnet-trx` — указывает формат.

## Дополнительные возможности

```yaml
      #Добавляем отчет о покрытии кода тестами
      - name: Run tests with coverage
        run: |
          mkdir -p TestResults
          dotnet test --no-build -c Release --collect:"XPlat Code Coverage" --results-directory ./TestResults --logger "trx;LogFileName=test_results.trx"

      - name: Install reportgenerator
        run: dotnet tool install -g dotnet-reportgenerator-globaltool

      - name: Generate HTML coverage report
        run: |
          reportgenerator -reports:TestResults/**/coverage.cobertura.xml -targetdir:coverage-report -reporttypes:Html

      #Предоставляем возможность скачать результаты тестирования
      - name: Upload Test Results
        uses: actions/upload-artifact@v4
        with:
          name: test-results
          path: TestResults/*.trx

      - name: Upload Coverage Report
        uses: actions/upload-artifact@v4
        with:
          name: coverage-html
          path: coverage-report/**
```


