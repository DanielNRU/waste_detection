# Обнаружение и классификация пластиковых отходов

Этот проект посвящён разработке системы для обнаружения пластикового мусора на изображениях с использованием моделей YOLOv11. Основной целью является создание модели, способной точно и эффективно детектировать различные типы мусора на сортировочном конвейере мусороперерабатывающего завода.

## Оглавление

1. [Описание проекта](#описание-проекта)  
2. [Особенности реализации](#особенности-реализации)  
3. [Требования](#требования)  
4. [Установка](#установка)  
5. [Использование](#использование)  
6. [Результаты](#результаты)  
7. [Рекомендации по улучшению](#рекомендации-по-улучшению)  
8. [Контакты](#контакты)  

---
## Заказчик
[Renue](https://renue.ru/) 

## Описание проекта

В рамках проекта были обучены две модели: **YOLO11n** и **YOLO11m**, использующие предобученные веса. Модели дообучались на размеченных данных, включающих изображения пластикового мусора различных типов. Основной задачей являлось сравнение производительности двух подходов и выбор наилучшего решения для задачи детекции.

## Особенности реализации

- **YOLO11n**:
  - Лёгкая модель, обеспечивающая высокую точность при минимальных вычислительных затратах.  
  - Подходит для использования в средах с ограниченными ресурсами (например, встраиваемые устройства).  
- **YOLO11m**:
  - Увеличенное количество параметров для более точной детекции объектов.  
  - Обеспечивает более высокие метрики за счёт использования увеличенного разрешения изображений.  
- Применение расширенных аугментаций данных (AugMix, HSV-преобразования) для улучшения обобщающей способности модели.  
- Оценка производительности на тренировочной, валидационной и тестовой выборках.  

## Требования

Для выполнения проекта требуется Python версии 3.10 и следующие библиотеки:

- PyTorch (>=2.5.1)  
- Ultralytics  
- Numpy  
- Pandas  
- Matplotlib  
- OpenCV  
- Scikit-learn  

Полный список библиотек с версиями доступен в [requirements.txt](requirements.txt).

## Установка

1. Склонируйте репозиторий:  
   ```bash
   git clone https://github.com/danielnru/waste_detection.git
   ```
2. Перейдите в папку проекта:  
   ```bash
   cd waste_detection
   ```
3. Установите зависимости:  
   ```bash
   pip install -r requirements.txt
   ```

## Использование

1. Подготовьте данные:  
   - Убедитесь, что размеченные данные расположены в директории `data/`. Формат аннотаций — YOLO.  
2. Для обучения модели YOLO11n выполните:  
   ```bash
   python train.py --model yolov11n --data data.yaml --epochs 150
   ```
3. Для обучения модели YOLO11m выполните:  
   ```bash
   python train.py --model yolov11m --data data.yaml --epochs 150
   ```
4. Для тестирования модели выполните:  
   ```bash
   python test.py --weights best.pt --data data.yaml
   ```

## Результаты

**Оценки производительности моделей:**  

| Модель       | Precision (P) | Recall (R) | mAP@50 | mAP@50-95 |  
|--------------|---------------|------------|--------|-----------|  
| **YOLO11n** | 0.975         | 0.907      | 0.953  | 0.854     |  
| **YOLO11m** | 0.982         | 0.921      | 0.960  | 0.892     |  
| **YOLO11m (очищенный датасет)** | 0.991         | 0.945      | 0.975  | 0.909     |  

**Ключевые выводы:**  
- Модель YOLO11n показала достойные результаты на тренировочной и валидационной выборках, обеспечив высокую точность и полноту при низких вычислительных затратах.
- Модель YOLO11m превзошла YOLO11n, особенно в задачах с более сложной детекцией, благодаря увеличенной архитектурной сложности и использованию улучшенных настроек аугментации.
- Исключение пустых рамок из тренировочного датасета привело к дальнейшему повышению метрик, однако на тестовой выборке результаты могли ухудшиться из-за наличия таких рамок в её изображениях.

## Рекомендации по повышению качества модели

- Увеличить объём тренировочных данных, добавив изображения, лучше отражающие характеристики тестового датасета.
- Исследовать новые подходы к аугментации, например, с учётом особенностей пластикового мусора.
- Рассмотреть использование других архитектур моделей и методов автоматического подбора гиперпараметров для дальнейшего улучшения производительности.

## Контакты

Если у вас есть вопросы, предложения или обратная связь, свяжитесь со мной:  

- **Имя**: Даниил Мельник  
- **Email**: git@danieln.ru  
- **GitHub**: [DanielNRU](https://github.com/DanielNRU)  

--- 