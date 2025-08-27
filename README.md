# Churn Prediction Service | End-to-End MLOps Project

Проект представляет собой полноценный ML-сервис для предсказания оттока клиентов. Он охватывает весь жизненный цикл модели: от анализа данных до развертывания в виде API с последующим мониторингом.

## Описание проекта

Цель проекта — создать и развернуть модель машинного обучения, которая прогнозирует, уйдет ли клиент в отток. Сервис построен с применением современных MLOps-практик для обеспечения надежности, воспроизводимости и качества.

## Технологический стек

- **Моделирование:** Scikit-learn, Pandas
- **API:** FastAPI
- **Развертывание:** Docker, Uvicorn
- **Эксперименты и версионирование моделей:** MLflow
- **Валидация данных:** Great Expectations
- **Мониторинг моделей:** Evidently AI
- **Тестирование:** Pytest
- **CI/CD:** GitHub Actions

## Архитектура

*Кратко опишите или добавьте простую схему, как компоненты связаны между собой.*

1.  **Обучение (Training):** Данные проходят валидацию в **Great Expectations**, после чего модель обучается. Эксперименты, параметры и метрики логируются в **MLflow**. Лучшая модель регистрируется в **MLflow Model Registry**.
2.  **Сервинг (Serving):** **FastAPI**-приложение загружает модель из реестра и предоставляет эндпоинт `/predict` для получения прогнозов. Все упаковано в **Docker-контейнер**.
3.  **Мониторинг (Monitoring):** Скрипт с **Evidently AI** периодически анализирует дрейф данных и деградацию модели, генерируя HTML-отчеты.

## Как запустить проект

1.  **Клонируйте репозиторий:**
    ```
    git clone https://github.com/your_username/churn-prediction-service.git
    cd churn-prediction-service
    ```

2.  **Установите зависимости:**
    ```
    pip install -r requirements.txt
    ```

3.  **(Рекомендуемый способ) Запуск через Docker Compose:**
    Эта команда поднимет FastAPI-сервис и сервер MLflow.
    ```
    docker-compose up --build
    ```
    - API будет доступен по адресу `http://localhost:8000/docs`.
    - MLflow UI будет доступен по адресу `http://localhost:5000`.

## Как использовать API

Отправьте POST-запрос на `http://localhost:8000/predict` с данными клиента в формате JSON.

**Пример с помощью `curl`:**
```
curl -X 'POST' \
  'http://localhost:8000/predict' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
    "gender": "Female",
    "senior_citizen": 0,
    "partner": "Yes",
    "dependents": "No",
    "tenure": 12,
    "phone_service": "No"
  }'
```

**Ожидаемый ответ:**
```
{
  "churn_probability": 0.85
}
```

## Структура репозитория

```
.
├── .github/workflows/      # CI/CD пайплайны GitHub Actions
├── data/                   # Датасеты
├── great_expectations/     # Конфигурации Great Expectations
├── monitoring_reports/     # HTML-отчеты от Evidently AI
├── notebooks/              # Jupyter-ноутбуки для EDA
├── src/                    # Исходный код
│   ├── api.py              # Логика FastAPI
│   ├── train.py            # Скрипт обучения модели
│   ├── predict.py          # Скрипт для инференса
│   └── monitoring.py       # Скрипт для мониторинга
├── tests/                  # Юнит-тесты
├── Dockerfile              # Dockerfile для API
├── docker-compose.yml      # Конфигурация Docker Compose
└── README.md               # Этот файл
```

## MLOps-функциональность

- **MLflow:** Все запуски экспериментов отслеживаются. Лучшие модели версионируются в Model Registry.
- **Great Expectations:** Встроенная проверка качества данных перед обучением и предсказанием.
- **Evidently AI:** Регулярный мониторинг дрейфа данных и производительности модели. Примеры отчетов находятся в папке `monitoring_reports`.
```
