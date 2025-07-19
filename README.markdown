# Система мониторинга лавинной опасности

## Описание проекта

Система мониторинга лавинной опасности — это киберфизическая система для анализа метеоданных и прогнозирования лавинной опасности в горных регионах. Проект реализован как монорепозиторий, включающий микросервисы для сбора, обработки и визуализации данных. Основная цель — повышение безопасности в горных районах путем предоставления точных прогнозов для спасательных служб.

Подробная документация и презентация проекта доступны на [странице](https://ilyadev1.github.io/Avalanche/).

### Основные цели
- Моделирование метеодатчиков для сбора погодных данных.
- Прогнозирование лавин с использованием нейросети KAN.
- Хранение и управление данными в PostgreSQL.
- Мониторинг качества прогнозов через Grafana.

### Ключевые особенности
- Сбор метеоданных (температура, ветер, осадки).
- Прогнозирование с помощью модели KAN (PyTorch).
- REST API на FastAPI.
- Контейнеризация с Docker.
- Мониторинг с Grafana и Prometheus.

## Архитектура

Проект включает микросервисы:
- **Датчики**: Моделируют метеоданные, отправляют в MQTT.
- **MQTT-брокер**: Передает данные между сервисами.
- **API Gateway**: Управляет запросами и сохраняет данные в PostgreSQL.
- **Сервис прогнозирования**: Использует KAN для прогнозов.
- **Grafana/Prometheus**: Мониторинг качества и состояния системы.

Подробности архитектуры и ERD-диаграмма доступны на [странице](https://ilyadev1.github.io/Avalanche/).

## Используемые технологии
- **Языки/фреймворки**: Python, FastAPI, PyTorch, SQLAlchemy.
- **Базы данных**: PostgreSQL, Alembic.
- **Контейнеризация**: Docker, Harbor.
- **Мониторинг**: Grafana, Prometheus, Postgres Exporter.
- **Интеграция**: MQTT, RabbitMQ, GitLab, TeamCity.

## Установка и запуск

### Требования
- Python 3.9+
- Docker, Docker Compose
- PostgreSQL
- Git

### Инструкции
1. Клонируйте репозиторий:
   ```bash
   git clone https://github.com/IlyaDev1/avalanche-monitoring.git
   cd avalanche-monitoring
   ```
2. Настройте `.env` (см. `.env.example`).
3. Запустите контейнеры:
   ```bash
   docker-compose up --build
   ```
4. Выполните миграции:
   ```bash
   alembic upgrade head
   ```
5. Запустите FastAPI:
   ```bash
   uvicorn app.main:app --host 0.0.0.0 --port 8000
   ```

Подробные инструкции на [странице](https://ilyadev1.github.io/Avalanche/).

## Пример API

**Запрос прогноза**:
```bash
curl -X POST "http://localhost:8000/predict" \
-H "Content-Type: application/json" \
-d '{"mountain_id": 1, "sector_id": 1, "datetime": "2025-07-18T10:00:00", "temperature": -5.0, "wind_speed": 10.0, "precipitation": 2.5}'
```

**Ответ**:
```json
{
  "mountain_id": 1,
  "sector_id": 1,
  "datetime": "2025-07-18T10:00:00",
  "avalanche_probability": 75.5
}
```

## Мониторинг
- **Grafana**: Визуализация ошибок модели KAN.
- **Prometheus**: Мониторинг состояния базы данных.
- **Логирование**: Реализовано через Python `logging`.

## Будущие улучшения
- Frontend с картой лавинной опасности.
- Расширение мониторинга качества модели.
- Оптимизация модели KAN.

## Контакты
- Разработчик: Илья Коновалов
- Email: [neiluamaibi@mail.ru](mailto:neiluamaibi@mail.ru)
- Telegram: [t.me/IlyaKonovalov](https://t.me/IlyaKonovalov)
- GitHub: [github.com/IlyaDev1](https://github.com/IlyaDev1)
