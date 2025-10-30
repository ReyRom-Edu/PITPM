В Postman модуль **`pm.test`** используется для написания **тестов** (скриптов проверки), которые выполняются после запроса. Это часть Postman Sandbox API, позволяющая работать с ответом сервера, переменными, статусом и т.д.

Вот подробное описание **базовых возможностей `pm.test`** 👇

---

## 🔹 Что такое `pm.test`

`pm.test(name, function)` — функция для определения **одного теста**.
Она принимает:

* **`name`** — строку с описанием теста;
* **`function`** — код, выполняющий проверку.

Пример:

```js
pm.test("Статус код 200", function () {
    pm.response.to.have.status(200);
});
```

---

## 🔹 Основные проверки через `pm.expect` и `pm.response`

Postman использует библиотеку **Chai** (BDD-синтаксис `expect`) для удобных ассертов.

### Проверка статуса

```js
pm.test("Успешный ответ", function () {
    pm.response.to.have.status(200);
});
```

### Проверка типа содержимого

```js
pm.test("Ответ в формате JSON", function () {
    pm.response.to.be.json;
});
```

### Проверка тела ответа

```js
pm.test("Содержит поле success", function () {
    const json = pm.response.json();
    pm.expect(json).to.have.property("success", true);
});
```

### Проверка заголовков

```js
pm.test("Content-Type = application/json", function () {
    pm.response.to.have.header("Content-Type", "application/json");
});
```

---

## 🔹 Использование `pm.expect`

`pm.expect()` используется для любых произвольных проверок (не только ответа).

Пример:

```js
pm.test("Проверяем значение переменной", function () {
    pm.expect(pm.environment.get("token")).to.not.be.undefined;
});
```

Можно проверять строки, числа, массивы, и т.д.:

```js
pm.test("Проверяем длину массива", function () {
    const data = pm.response.json().items;
    pm.expect(data.length).to.be.above(0);
});
```

---

## 🔹 Группировка проверок

Можно выполнять несколько ассертов внутри одного теста:

```js
pm.test("Проверяем тело и код", function () {
    pm.response.to.have.status(200);
    const body = pm.response.json();
    pm.expect(body.success).to.eql(true);
});
```

---

## 🔹 Работа с переменными

Postman позволяет сохранять значения для последующих запросов:

```js
const data = pm.response.json();
pm.environment.set("userId", data.id);
```

И тестировать их:

```js
pm.test("userId установлен", function () {
    pm.expect(pm.environment.get("userId")).to.exist;
});
```

---

## 🔹 Примеры типичных тестов

### Проверка времени ответа

```js
pm.test("Время ответа меньше 500 мс", function () {
    pm.expect(pm.response.responseTime).to.be.below(500);
});
```

### Проверка части строки в теле

```js
pm.test("Ответ содержит 'OK'", function () {
    pm.expect(pm.response.text()).to.include("OK");
});
```

### Проверка массива

```js
pm.test("Массив не пуст", function () {
    const arr = pm.response.json().items;
    pm.expect(arr).to.be.an("array").that.is.not.empty;
});
```

---

## 🔹 Дополнительные объекты `pm`

| Объект           | Описание                                 |
| ---------------- | ---------------------------------------- |
| `pm.response`    | Доступ к ответу сервера                  |
| `pm.request`     | Данные запроса                           |
| `pm.environment` | Работа с переменными окружения           |
| `pm.globals`     | Глобальные переменные                    |
| `pm.variables`   | Все доступные переменные (с приоритетом) |
| `pm.info`        | Информация о коллекции, итерации и т.д.  |

---

## 🔹 Пример комплексного теста

```js
pm.test("Проверка создания пользователя", function () {
    pm.response.to.have.status(201);
    pm.response.to.be.json;

    const body = pm.response.json();
    pm.expect(body).to.have.property("id");
    pm.expect(body.name).to.eql("Roman");
    pm.environment.set("createdUserId", body.id);
});
```

---

## 🔹 Резюме

| Возможность          | Пример                                                 |
| -------------------- | ------------------------------------------------------ |
| Проверка статуса     | `pm.response.to.have.status(200)`                      |
| Проверка формата     | `pm.response.to.be.json`                               |
| Проверка заголовка   | `pm.response.to.have.header("Content-Type")`           |
| Проверка тела        | `pm.expect(pm.response.json().ok).to.eql(true)`        |
| Проверка скорости    | `pm.expect(pm.response.responseTime).to.be.below(300)` |
| Работа с переменными | `pm.environment.set("token", value)`                   |

---

Хочешь, я подготовлю **таблицу-шпаргалку** по всем командам `pm.test` и часто используемым ассертам (`to.have.status`, `to.be.json`, `pm.expect(...)`, и т.д.) — в виде компактного cheat sheet для печати?
