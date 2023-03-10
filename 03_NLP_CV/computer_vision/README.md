`Keras` `pandas` `seaborn`

# Определение возраста покупателей
В проекте разрабатывалась система для определения возраста покупателей магазина, для проверки добросовестности продовцов при продаже алкоголя и анализа покупок, которые могут заинтересовать покупателей каждой возрастной группы.
Данные взяты с сайта ChaLearn Looking at People.
По фотографии нужно определить возраст человека, поэтому предстоит решать задачу регрессии. Метрикой качества будет MAE.

Модель обучалась отдельно на GPU. В проекте представлены результаты обучения


# Анализ обученной модели
Для обучения модели используется достаточно большой датасет 7.5 тыс объектов, хотя он и значтельно меньше, чем те, что хранятся в открытых источниках на CIFAR и ImageNet и других ресурсах.

Судя по распределению, есть небольшой скос гистограмы вправо.Больше всего объектов в диапозоне 20-30 лет. Соответствено модель лучше обучится предсказывать признак на этой категории фотографий. Для более точного обучения модели, к тренировочной выборке применились специальные гиперпараметры (поворот, изменение яркости). Тестовая выборка оставлена без изменений.

В качестве основы за модель взяли уже предобученную нейросеть. В выходном слое, для более точного обучения модели, использовали оптимизацию Adam c шагом обучения 0.0003, а метрикой качества выбрана MSE, что немного ускорило процесс обучения. Последним выходным слоем был выбран ReLU. Положительные прогнозы сети функция ReLU не меняет, а все отрицательные — приводит к нулю. Чисел меньше 0 быть не может.

С такими параметрами модель на 9 эпохе обучения достигла значения по метрике 6.2107 (цель меньше 7 дотигнута)

Таким образом мы достигли требуемой точности предсказания возраста нашей моделью.
