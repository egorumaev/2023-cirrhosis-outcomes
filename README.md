# 2023-cirrhosis-outcomes
Прогнозирование исхода лечения пациентов с циррозом печени

# **ПРОЕКТ «Прогнозирование исхода лечения цирроза печени – Prediction of Cirrhosis Outcomes»**

---
![](https://github.com/egorumaev/2023-cirrhosis-outcomes/blob/main/Multi-Class%20Prediction.PNG)

Проект выполнен в рамках участия в соревновании на **Kaggle** «Multi-Class Prediction of Cirrhosis Outcomes» (декабрь 2023)

* [Официальный сайт соревнования](https://www.kaggle.com/competitions/playground-series-s3e26 'Ссылка на официальный сайт')

---

## **Примененные библиотеки и технологии**

* Pandas, Numpy, Matplotlib, Seaborn, Missingno, Dataprep, Phik, Category_encoders, Sklearn, Imblearn, Catboost, XGBoost

* IQR (Interquartile Range), PCA (Principal component analysis), LDA (Linear Discriminant Analysis), t-SNE (T-distributed Stochastic Neighbor Embedding), Feature Engineering, Polynomial Features, Pipeline, VarianceThreshold, SMOTETomek

---

## **Цель и задачи проекта**

**Цель** – используя мультиклассовый подход спрогнозировать исход лечения пациентов с циррозом печени, предсказав вероятность для каждого пациента одного из трех статусов: C, CL или D.

Для достижения цели были решены следующие **задачи**:

 * данные проверены на наличие пропусков, явные дубликаты, выбросы;

 * выбросы обработаны;

 * признаки проверены на мультиколлинеарность;

 * данные подготовлены для сжати с помощью алгоритмов PCA, LDA, t-SNE;

 * проведена оценка требуемого для машинного обучения количества главных компонент для применения PCA;

 * данные высокой размерности представлены в 2D с помощью алгоритмов PCA, LDA, t-SNE;

 * проведено обучение моделей CatBoost и XGBoost как с применением классических подходов обработки данных с помощью Pipeline, так и с помощью алгоритмов сжатия данных PCA и LDA, подготовлены csv-файлы для серии сабмитов.

Решаемая в рамках проекта задача является задачей **мультиклассификации**.

---

## **Основные результаты**

**(1)** Выполнено визуальное представление данных высокой размерности с помощью **PCA**, **LDA**, **t-SNE**, показавшее, что имеющиеся для машинного обучения данные плохо разделяются на группы, разные классы целевого признака перемешаны. Несколько лучшее распределение данных наблюдается на рисунках, построенных на данных, сжатых с помощью **t-SNE**. Однако, метод **t-SNE** применим только для визуализации и не пригоден для обработки данных с целью передачи модели машинного обучения.

**(2)** Для машинного обучения выбраны две модели градиентного бустинга: CatBoost и XGBoost, каждая из которых обучена на трех разных датасетах:

 * **train_features** (исходный датасет, включающий категориальные и числовые признаки, обработанный с помощью Pipeline с помощью обычных функций)

 * **train_for_compress** (19 числовых признаков)

 * **train_for_compress_polynom** (210 числовых признаков, большая часть которых – полиномиальные)

**(3)** В серии сабмитов лучшие и почти одинаковые результаты показали обе отобранные для машинного обучения модели CatBoost и XGBoost, обученные на датасете с исходными признаками **train_features**. 

**(4)** Сабмиты, выполненные на специально подготовленных датасетах **train_for_compress** и **train_for_compress_polynom** по итогам экспериментов с подбором числа главных компонент алгоритма **PCA** показали результаты, уступающие обучению моделей на датасете с исходными признаками **train_features**. 

**(5)** Самые низкие результаты показали сабмиты, выполненные по результатам обучения машинных моделей с помощью алгоритма сжатия данных **LDA**.

**(6)** Более низкие результаты обучения машинных моделей, полученные с помощью **PCA** и **LDA**, в целом были ожидаемы, так как на серии визуализаций представления данных высокой размерности было отчетливо видно, что классы целевого признака плохо разделяются на группы, накладываются друг на друга.
