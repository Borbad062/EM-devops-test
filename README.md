# Effective Mobile Test Project

Простое веб-приложение, развернутое с использованием Docker и Docker Compose. Приложение состоит из двух сервисов:

- **Backend** — Python HTTP-сервер, возвращающий текст "Hello from Effective Mobile!"
- **Nginx** — reverse proxy, принимающий запросы и перенаправляющий их на backend


**Как это работает:**
1. Пользователь отправляет HTTP запрос на порт 8000 хоста
2. Docker пробрасывает запрос на порт 80 контейнера nginx
3. Nginx получает запрос и проксирует его на upstream backend
4. Backend (Python сервер) обрабатывает запрос и возвращает ответ "Hello from Effective Mobile!"
5. Nginx возвращает ответ пользователю

## 🛠️ Технологии

| Технология | Версия | Назначение |
|------------|--------|------------|
| Docker | 20.10+ | Контейнеризация |
| Docker Compose | 2.0+ | Оркестрация контейнеров |
| Python | 3.13 | Язык программирования backend |
| Nginx | 1.27 | Reverse proxy |
| Alpine Linux | 3.19 | Базовый образ (минимальный размер) |

## 📦 Требования

- Docker версии 20.10 или выше
- Docker Compose версии 2.0 или выше
- curl (для тестирования)
- Git (для клонирования)

## 🚀 Быстрый старт

### 1. Клонирование репозитория

- git https://github.com/Borbad062/EM-devops-test.git
- cd EM-devops-test

2. Создание файла окружения

- echo "COMPOSE_PROJECT_NAME=effective-mobile-test" > .env

3. Запуск приложения
   
   docker-compose up --build -d
   Эта команда:
   - Соберет образ для backend-приложения
   - Скачает образ nginx
   - Запустит оба контейнера в фоновом режиме

## Проверка работоспособности

После запуска выполните команду:

- curl http://localhost:8000

Ожидаемый ответ:

Hello from Effective Mobile!

## Проверка состояния контейнеров

Просмотр запущенных контейнеров:

- docker-compose ps

## Просмотр логов:

- docker-compose logs backend
- docker-compose logs nginx

## Остановка проекта

- docker-compose down


## Структура проекта
EM-devops-test/

- ├── backend/
- │   ├── Dockerfile          # Конфигурация образа backend
- │   └── app.py              # Python HTTP сервер
- ├── nginx/
- │   └── nginx.conf          # Конфигурация Nginx
- ├── docker-compose.yml      # Оркестрация сервисов
- ├── .env                    # Переменные окружения
- ├── .gitignore              # Игнорируемые файлы
- └── README.md               # Документация

## Безопасность

1) Non-root пользователь (UID 1001) в обоих контейнерах

2) Backend недоступен напрямую с хоста

3) Конфигурация nginx монтируется только для чтения

4) Изолированная сеть между сервисами
