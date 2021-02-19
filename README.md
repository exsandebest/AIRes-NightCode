# AIRes NightCode#1

### Info
* Трек: ML
* Команда: exsandebest
* Участники: exsandebest (Даниил Богданов)

### Проект
* Задача: система для подбора сотрудников по критериям работодателя.
* Результат: Jupyter Notebook
* Язык: Python
* Библиотеки: Pandas, NumPy, CatBoost, sklearn (train_test_split)
* Подразумевается, что модель будет внедряться после определённого периода работы компании на "ручном" подборе кандидатов для формирования датасета. Для каждого работодателя отдельная модель, обученная на данных о предыдущих откланённых или принятых на работу кандидатах.
* Задача бинарной классификации с результатом в виде predict probability:  
0 - не подходит работодателю  
1 - подходит работодателю  
По predict probability (вероятность на отрезке [0;1]) будем оценивать то, насколько подходит кандидат работодателю.
* Метрика для обучения:  
Accuracy не подойдёт из-за неравенства классов (наверняка непринятых на работу гораздо больше). Нам важно как то, чтобы все предложенные моделью кандидаты были действительно хорошими (precision), так и то, чтобы модель не упускала потенциально хороших кандидатов (recall), поэтому используем метрику F1, как комбинацию precision и recall.
* Данные о предыдущих кандидатах и их участи в формате `.csv` с колонкой-target `hired` и n колонками-фичами.
* Данные для примера синтетические и с малым количеством фичей

#### Весь процесс обработки данных, обучения модели и получения ответов описан в [`AIRes.ipynb`](https://github.com/exsandebest/AIRes-NightCode/blob/main/AIRes.ipynb)
##### Если вкратце, то
* Загрузили данные предыдущих работников с их результатами (были ли они наняты или нет)
* Испрвили ошибки в анкетах
* Заполнили пропущенные значения медианами
* Линейно нормализовали числовые данные
* Обработали категориальные фичи
* Сделали разделение на основную и валидационную выборку
* Настроили гиперпараметры модели
* Обучили модель
* Нашли вероятность предсказания вердикта "нанят" для каждого нового кандидата
* Отсекли по пороговому значению кандидатов, в которых модель не уверена
* Получили список идентификационных номеров кандидатов, которых стоит рассмотреть для приглашения на собеседование
