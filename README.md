# OCR_License_Plates

## Общее описание
Системы распознавания автомобильных номеров состоят из двух модулей: детекция и распознавание символов (Optical Character Recognition, OCR). Детектор выделяет прямоугольник с номером из изображения, а OCR конвертирует его в текст. Будем считать, что детектор уже реализован. Здесь реализована модель OCR для автомобильных номеров.

**Пример входа:** 
![Автомобильный номер](https://algocode.ru/files/course_dlfall22/number.png)

**Пример выхода:** 皖AD16688

## Архитектура решения
Реализована модель, состоящая из двух блоков: Fully-convolutional CNN (FCNN) и Bi-LSTM. На выходе использован CTC-loss. 

![Архитектура](https://algocode.ru/files/course_dlfall22/architecture.png)

## Корпус данных
Подготовленный корпус можно скачать по [ссылке](https://disk.yandex.ru/d/adjYzzNayB1pag).

## Что включает решение
1. **Подготовка данных.** Реализован класс данных (наследник torch.utils.data.Dataset). Класс считывает входные изображения и выделяет метки из имён файлов. Для чтения изображений использована библиотека OpenCV (методы cv2.imread, cv2.resize и cv2.cvtColor).
2. **Создание и обучение модели.** Код модели реализован через слои стандартной библиотеки torch. 
3. **Подсчет метрик.** Качество модели оценивается по двум метрикам: accuracy и Character Error Rate (CER). Accuracy считает долю правильно распознанных номеров. CER оценивает число посимвольных ошибок.
4. **Анализ ошибок модели.** В этой секции найдены изображения из тестового корпуса, на которых модель ошибается сильнее всего (по loss или по CER). 

## Результаты: 
* Loss: CTCLoss
* Optimizer: Adam
* Scheduler: StepLR
* Tricks: Нормализация изображений

* Test accuracy: 0.984
* Test CER: 0.003

