# Churn Prediction Service
Небольшое ML‑исследование для прогнозирования оттока клиентов на датасете с Kaggle. Проведён EDA, анализ связей/корреляций, обучение и сравнение моделей классификации по метрикам качества с последующим выбором и дообучением лучшей модели.


Датасет
Источник: Kaggle — <https://www.kaggle.com/datasets/muhammadshahidazeem/customer-churn-dataset/slug>


Подготовка: обработка пропусков, масштабирование числовых, кодирование категориальных (One‑Hot/Target), борьба с дисбалансом (class_weight/oversampling).

Методика и модели
Бейзлайн: логистическая регрессия.

Модели: DecisionTree, RandomForest, XGBoost.

Валидация: Stratified K‑Fold (k=5), фиксированные сиды.


Метрики: ROC‑AUC (основная), F1, PR‑AUC, Recall для положительного класса.

Архитектура и стек
Язык/библиотеки: Python 3.11, pandas, numpy, scikit‑learn, CatBoost.
