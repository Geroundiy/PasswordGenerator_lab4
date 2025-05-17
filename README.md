Веб-приложение для генерации и управления паролями с тегами. Использует PostgreSQL и BCrypt для шифрования. Поддерживает CRUD, кэширование, гибкие GET-запросы и Spring Security для настройки доступа.

Требования:

- Java 17
- Maven
- PostgreSQL (база: passworddb)
- Переменная окружения DB_PASSWORD
- API Endpoints

# 1. Генерация пароля
- GET `http://localhost:8080/api/passwords/generate?length=X&complexity=Y&owner=Z`

Параметры:
- length: 4-30 символов
- complexity: 1 (цифры), 2 (цифры+буквы), 3 (цифры+буквы+символы)
- owner: опциональное имя владельца

Пример:
`http://localhost:8080/api/passwords/generate?length=12&complexity=3&owner=testUser`

# 2. Поиск паролей по тегу
- GET `http://localhost:8080/api/passwords/by-tag?tagName={tagName}`

Пример:
`http://localhost:8080/api/passwords/by-tag?tagName=work`

# 3. CRUD операции
- Пароли:
`POST|GET|PUT|DELETE http://localhost:8080/api/passwords`

- Теги:
`POST|GET|PUT|DELETE http://localhost:8080/api/tags`

Особенности

- Кэш: In-memory Map для методов: generatePassword, findAll, findById, findPasswordsByTagName(очищается при изменениях данных)
- Хранение: Пароли: таблица passwords
            Теги: таблица tags
- Связи: password_tag (many-to-many)
- Безопасность: Конфигурация Spring Security для открытого доступа к /api/passwords/generate
