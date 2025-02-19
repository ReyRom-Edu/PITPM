**Лекция: Регрессионное тестирование**

### Введение
Регрессионное тестирование — это тип тестирования программного обеспечения, который проверяет, не повлияли ли последние изменения в коде на уже существующий функционал. Его цель — удостовериться, что после добавления новых функций, исправления багов или любых других изменений в системе старый функционал продолжает работать корректно. Регрессионное тестирование особенно важно в среде, где изменения происходят часто, например, в проектах с Agile-методологиями или непрерывной интеграцией и доставкой (CI/CD).

### Основные задачи регрессионного тестирования
1. **Обеспечение стабильности кода**: убедиться, что обновления не нарушают уже работающие функции.
2. **Снижение риска откатов**: выявление возможных проблем на ранней стадии, что позволяет избежать излишних откатов и больших изменений.
3. **Повышение уверенности в системе**: проверка на уровне регрессионного тестирования повышает уверенность в том, что система работает надежно, и можно продолжать разработку.

### Когда необходимо регрессионное тестирование?
Регрессионное тестирование может потребоваться при следующих сценариях:
- **Добавление новой функциональности**: каждая новая функция или улучшение могут потенциально затронуть существующие.
- **Исправление дефектов**: изменения в коде для устранения багов могут повлиять на другой функционал.
- **Изменения конфигурации системы**: обновление библиотек, изменение параметров окружения и переход на новые платформы.
- **Оптимизация производительности**: любая оптимизация кода может внести изменения в логику работы системы.
  
### Типы регрессионного тестирования
1. **Корректирующее регрессионное тестирование**: используется при отсутствии изменений в спецификации и поведении приложения. Тесты в этом случае проверяют, что приложение продолжает функционировать как и раньше.
2. **Избирательное регрессионное тестирование**: применяется, когда были внесены только частичные изменения, и тестировщик выбирает только те тест-кейсы, которые могли бы быть затронуты изменениями.
3. **Полное регрессионное тестирование**: применяется при значительных изменениях в коде или после крупных обновлений, когда важно проверить всю систему целиком.
4. **Регрессионное тестирование с использованием автоматизации**: автоматизация регрессионного тестирования позволяет повторять тесты быстро и эффективно, экономя время и ресурсы.

### Методы регрессионного тестирования
1. **Ручное регрессионное тестирование**: все тесты выполняются вручную, что может быть дорого и требует времени. Это подходит для небольших изменений или одноразовых проверок.
2. **Автоматизированное регрессионное тестирование**: автоматизация тестов обеспечивает повторное использование тест-кейсов и быстрое обнаружение ошибок. Подходит для больших и постоянных проектов.
3. **Комбинированный подход**: сочетание ручного и автоматизированного тестирования. Например, для критических функций используется автоматизация, а новые или менее важные изменения проверяются вручную.

### Подходы к выбору тест-кейсов для регрессионного тестирования
1. **Часто используемые функции**: тесты, покрывающие наиболее критичные и часто используемые функции, должны быть в приоритете.
2. **Функции, которые затрагивались изменениями**: те части системы, которые подверглись изменению, должны быть протестированы в первую очередь.
3. **Уязвимые области системы**: если некоторые модули в прошлом были подвержены большему количеству ошибок, они требуют большего внимания.
4. **Общие сценарии использования**: популярные пути использования системы, которые проходят большинство пользователей, следует обязательно включать в тестирование.

### Внедрение автоматизации в регрессионное тестирование
Автоматизация регрессионного тестирования позволяет:
- Экономить время за счёт сокращения ручных проверок;
- Быстро реагировать на изменения;
- Улучшить покрытие тестами и повысить точность тестирования.

**Инструменты для автоматизированного регрессионного тестирования**:
1. **Selenium**: популярный инструмент для веб-приложений, позволяет создавать сложные тесты с различными сценариями взаимодействия.
2. **JUnit/NUnit**: подходящие для тестирования Java и .NET приложений, также поддерживают интеграцию с CI/CD.
3. **TestNG**: позволяет создавать и управлять тестовыми сценариями для Java-приложений.
4. **Appium**: подходит для тестирования мобильных приложений.
5. **Jenkins** и другие CI/CD-инструменты: автоматизируют запуск регрессионных тестов после каждого обновления кода.

### Вызовы и сложности регрессионного тестирования
1. **Ресурсоёмкость**: полное регрессионное тестирование требует значительных ресурсов, особенно при ручном выполнении.
2. **Обновление тест-кейсов**: при изменении логики приложения приходится пересматривать существующие тест-кейсы.
3. **Приоритизация тестов**: сложно определить, какие тесты приоритетны, особенно в крупных системах.
4. **Фальшивые положительные результаты**: иногда автоматические тесты выдают ложные ошибки из-за изменений в приложении, требуя их пересмотра.

### Преимущества регрессионного тестирования
- **Уменьшение числа ошибок**: предотвращение появления багов после обновлений.
- **Ускорение разработки**: автоматизация позволяет разработчикам получать быструю обратную связь.
- **Повышение качества**: стабильный продукт привлекает пользователей, а также уменьшает нагрузку на поддержку.

### Заключение
Регрессионное тестирование является важной составляющей процесса разработки, обеспечивающей стабильность и надежность продукта. Это тестирование минимизирует риски, позволяет поддерживать высокое качество кода и помогает компании быстро вносить изменения в продукт без потери качества.



**Лекция: Test-Driven Development (TDD)**

### Введение
Test-Driven Development (TDD), или разработка через тестирование, — это подход к разработке программного обеспечения, при котором тесты пишутся перед реализацией самого функционала. Основная идея TDD — сначала определить требования к функционалу через тесты, затем реализовать его и, наконец, убедиться в правильности работы. TDD помогает разработчикам создавать более качественный код, уменьшать количество ошибок и улучшать структуру программы.

### Принципы TDD
В основе TDD лежит цикл **«Red-Green-Refactor»**:
1. **Red (красный)**: Написать тест для нового функционала, который на данный момент не реализован. Тест не проходит, так как соответствующая функция ещё не написана.
2. **Green (зелёный)**: Реализовать минимально необходимую логику, чтобы тест успешно прошёл.
3. **Refactor (рефакторинг)**: Оптимизировать и улучшить код, не нарушая работу тестов.

Этот процесс повторяется для каждого нового функционала, обеспечивая, что все части кода покрыты тестами и продолжают работать корректно на протяжении всего жизненного цикла разработки.

### Основные задачи TDD
1. **Повышение уверенности в коде**: поскольку каждое изменение тестируется, разработчики могут быть уверены, что не вносят багов.
2. **Улучшение дизайна кода**: TDD поощряет написание кода, ориентированного на тестируемость и декомпозицию, делая код более чистым и структурированным.
3. **Раннее обнаружение ошибок**: тесты позволяют выявить ошибки в коде до того, как они попадут в основную ветку проекта или в продакшен.

### Ключевые этапы процесса TDD
1. **Написание теста**: формулирование теста, определяющего поведение, которое необходимо реализовать. Это включает в себя описание входных данных и ожидаемого результата.
2. **Запуск теста и проверка его провала**: убедиться, что тест не проходит, что подтверждает отсутствие соответствующей функциональности.
3. **Создание минимальной реализации**: написание минимального кода, чтобы тест начал проходить. Важно избегать избыточности на этом этапе.
4. **Запуск теста и проверка его успешного прохождения**: удостовериться, что тест пройден, и нужная функциональность теперь реализована.
5. **Рефакторинг кода**: улучшение структуры и качества кода, при этом тесты помогают убедиться, что функциональность остаётся неизменной.

### Преимущества TDD
1. **Снижение числа ошибок**: автоматические тесты обнаруживают баги на ранней стадии.
2. **Улучшение архитектуры и дизайна**: при написании тестируемого кода разработчики склонны использовать более гибкие и модульные структуры.
3. **Повышение уверенности в рефакторинге**: автоматизированные тесты позволяют легко изменять код, не опасаясь сломать функционал.
4. **Более быстрое и эффективное развитие**: наличие тестов позволяет добавлять новый функционал без риска разрушения существующей функциональности.

### Примеры TDD в реальной разработке
Представим пример разработки функции сложения двух чисел. Применим процесс TDD для этой функции:

1. **Red**: Написать тест, который проверяет, что `Add(2, 3)` возвращает `5`.
2. **Green**: Реализовать функцию `Add`, которая возвращает сумму двух чисел.
3. **Refactor**: Убедиться, что код читается легко, и нет избыточности.

Каждый новый тест делает реализацию более полной, добавляя необходимую логику в функцию, пока она не покроет все сценарии.

### Разработка через TDD vs. традиционная разработка
В традиционной разработке сначала пишут основной код, а затем тесты. Это может приводить к тому, что тесты будут недоразвиты или покрывать не весь функционал. В TDD тесты определяют, что и как нужно реализовать, а значит:
- Каждый тест имеет конкретную цель, связанную с функционалом, что снижает вероятность появления незадокументированных или ненадёжных частей системы.
- Рефакторинг становится безопасным и контролируемым процессом, так как тесты выступают гарантом, что функционал не ломается.

### Основные паттерны TDD
1. **Mock Objects**: используются для эмуляции поведения зависимостей, позволяя тестировать модули изолированно.
2. **Arrange-Act-Assert (AAA)**: шаблон, разделяющий тест на три части: подготовка данных, выполнение тестируемого кода и проверка результата.
3. **Parameterized Tests**: позволяют использовать одни и те же тесты для разных наборов данных.

### Проблемы и сложности TDD
1. **Повышенные временные затраты**: на начальном этапе может потребоваться больше времени для написания тестов, что замедляет разработку.
2. **Сложности с поддержанием тестов**: когда система меняется, тесты также должны быть актуализированы, иначе они начинают давать ложные результаты.
3. **Сложности с тестированием пользовательского интерфейса**: TDD больше ориентирован на модульные тесты, а тестирование UI требует дополнительных подходов.
4. **Перекос в сторону тестов**: разработчики иногда пишут слишком простые или неинформативные тесты, что снижает эффективность TDD.

### Инструменты для TDD
Популярные инструменты для TDD зависят от используемого языка программирования и могут включать:
- **JUnit** и **TestNG** для Java
- **NUnit** и **xUnit** для .NET
- **Mocha** и **Jest** для JavaScript
- **PyTest** и **unittest** для Python

Эти фреймворки предлагают возможность легко писать, запускать и организовывать тесты, а также предоставляют инструменты для мока и ассертов, чтобы упростить тестирование сложных сценариев.

### Примеры применения TDD
TDD широко используется в разработке микросервисов, библиотек и модулей с независимой бизнес-логикой. Особенно подход TDD эффективен в CI/CD-процессах, где тесты, написанные в рамках TDD, интегрируются в конвейеры и обеспечивают быстрые проверки при каждом изменении кода. В крупных проектах, таких как банковские системы или интернет-магазины, TDD позволяет гибко адаптировать проект к новым требованиям.

### Заключение
TDD — это мощный инструмент для разработки надёжного и качественного программного обеспечения. Он дисциплинирует разработчиков, направляя их на создание тестируемого, чистого и легко поддерживаемого кода. Однако, TDD — это не панацея, и его использование может быть оправдано не во всех проектах, например, при создании сложных пользовательских интерфейсов.