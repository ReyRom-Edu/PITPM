## 🧭 1. Что такое `curl`

**`curl`** — это консольная утилита для отправки HTTP-запросов и получения ответов от серверов.
Она используется для тестирования API, проверки доступности эндпоинтов и отладки запросов.

---

## ⚙️ 2. Проверка наличия `curl` в Windows

Почти во всех современных версиях Windows (10, 11) `curl` уже встроен.

Открой **Командную строку (CMD)** или **PowerShell** и введите:

```bash
curl --version
```

Если вы видите версию, например:

```
curl 8.5.0 (Windows) ...
```

— значит всё готово.
Если нет — можно скачать с официального сайта:
🔗 [https://curl.se/windows/](https://curl.se/windows/)

---

## 🌐 3. Простейший GET-запрос

Чтобы проверить работу API, выполните:

```bash
curl https://api.example.com
```

или, например:

```bash
curl https://jsonplaceholder.typicode.com/posts
```

Ответ — это **JSON**, возвращаемый сервером.

---

## 📦 4. Добавление заголовков (headers)

Заголовки используются для передачи информации, например формата данных или токена авторизации.

Пример:

```bash
curl -H "Accept: application/json" https://api.example.com/data
```

Несколько заголовков:

```bash
curl -H "Accept: application/json" -H "Authorization: Bearer MY_TOKEN" https://api.example.com/users
```

---

## 📮 5. POST-запрос с данными

Чтобы отправить данные (например, JSON) на сервер:

```bash
curl -X POST https://api.example.com/users ^
     -H "Content-Type: application/json" ^
     -d "{\"name\": \"Roman\", \"email\": \"roman@example.com\"}"
```

*(символ `^` в Windows CMD используется для переноса строки)*

PowerShell-версия:

```bash
curl -Method POST https://api.example.com/users `
     -Headers @{"Content-Type"="application/json"} `
     -Body '{"name":"Roman","email":"roman@example.com"}'
```

---

## ✏️ 6. PUT и DELETE-запросы

**PUT** — обновление данных:

```bash
curl -X PUT https://api.example.com/users/1 ^
     -H "Content-Type: application/json" ^
     -d "{\"email\": \"newmail@example.com\"}"
```

**DELETE** — удаление данных:

```bash
curl -X DELETE https://api.example.com/users/1
```

---

## 📁 7. Сохранение ответа в файл

Если нужно записать результат запроса в файл:

```bash
curl https://api.example.com/data -o result.json
```

---

## 🧩 8. Форматирование JSON (для удобства)

Ответы часто приходят в виде длинной строки.
Для форматирования можно использовать PowerShell:

```bash
curl https://jsonplaceholder.typicode.com/posts | ConvertFrom-Json | ConvertTo-Json -Depth 5
```

или установить утилиту `jq` и сделать:

```bash
curl https://jsonplaceholder.typicode.com/posts | jq
```

---

## 🧠 9. Примеры для тренировки

| Задача                            | Пример команды                                                                                                                                          |
| --------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Получить список пользователей     | `curl https://jsonplaceholder.typicode.com/users`                                                                                                       |
| Получить конкретного пользователя | `curl https://jsonplaceholder.typicode.com/users/1`                                                                                                     |
| Создать новый пост                | `curl -X POST -H "Content-Type: application/json" -d "{\"title\":\"test\",\"body\":\"Hello\",\"userId\":1}" https://jsonplaceholder.typicode.com/posts` |

---

## 🧾 10. Полезные опции

| Опция          | Назначение                                 |
| -------------- | ------------------------------------------ |
| `-v`           | Подробный вывод запроса и ответа (verbose) |
| `-i`           | Показать заголовки ответа                  |
| `-s`           | Тихий режим (без прогресс-бара)            |
| `-o file.json` | Сохранить ответ в файл                     |
| `--location`   | Следовать редиректам (HTTP 3xx)            |

---

## 💡 Пример полного запроса

```bash
curl -X POST https://api.example.com/login ^
     -H "Content-Type: application/json" ^
     -d "{\"username\": \"admin\", \"password\": \"1234\"}" ^
     -i -v
```

