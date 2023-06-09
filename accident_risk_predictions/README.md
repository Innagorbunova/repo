﻿` `**Предсказание риска ДТП**

**Цель:** создание для каршеринговой компании системы, оценивающей риск ДТП по выбранному маршруту движения (под риском понимается вероятность ДТП с любым повреждением транспортного средства (как только водитель забронировал автомобиль, сел за руль и выбрал маршрут).

**Вывод:** Построены несколько моделей машинного обучения с перебором гиперпараметров для наилучшего показателя метрики качества AUC-ROC: два "Дерева решений" (с применением в качестве борьбы с дисбалансом классов целевого признака аргумента class_weight='balanced' и функции Downsampling), "Случайный лес" и модель градиентного бустинга библиотеки lightgbm также с применением функции Downsampling, модель градиентного бустинга библиотеки catboost на изначальных признаках. Значительных метрик добиться не удалось, самой лучшей (из того что получилось) оказалась модель градиентного бустинга "cb_model", построенная средствами библиотеки CatBoost с метриками AUC ROC = 0.634. 

Самым значимым для модели (46%) является признак "party_sobriety" (трезвость участника). Низкая метрика качества получилась  по причине отсутствия иных признаков, характеризующих личность водителя,  но добавлять их не имеет практического смысла, поскольку перед поездкой эти признаки не известны. 

Для усовершенствования модели машинного обучения по предсказанию "рискованности" водителя заказчику целесообразно саккумулировать данные, характеризующие личность водителя, которые известны до совершения поездки, а не после (типа употребление лекарств, или вид ДТП): о результатах предыдущих поездок водителей (попадал/не попадал в аварии), которые скорее всего в базе данных каршеринговой компании есть (да и потенциальные клиенты как правило выбирают одну и ту же компанию); о водительском стаже (есть в водительском удостоверении); о возрасте потенциального водителя (также есть в водительских правах).
Указанные данные доступны, характеризуют личность водителя и в своей совокупности должны улучшить качество предсказаний именно "рискованности" потенциального водителя до начала поездки, как это необходимо заказчику.

**Стек технологий:** pandas, numpy, seaborn, matplotlib, lightgbm, catboost, SQL, sqlalchemy, OneHotEncoder, StandardScaler,  OrdinalEncoder, LabelEncoder, LogisticRegression, DecisionTreeClassifier, RandomForestClassifier, Pipeline, make_pipeline, RandomUnderSampler, ColumnTransformer.

**Статус проекта:** завершен.






