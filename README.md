# SF-DS-diploma-project

Университет SkillFactory

Дипломный проект Pawel_MTW (Павел Матушевский)

Описание: 

Классификация картинок по признаку "С маской", "Без маски" на лице. Обучение Computer Vision Deep Learning.

Цели и задачи проекта: создать модель, которая будет "видеть" наличие или отсутствие медицинской маски на лице. Если наша модель работает хорошо, то мы сможем например быстро выявлять нарушителей масочного режима, лучше и проще контролировать требования ношения маски среди людей на предприятии или на улице.
Таким образом, эффективность ограничительных мер масочного режима увеличивается. Также такая система поможет предприятию, магазину контролировать посетителей и избежать штрафов за нарушение масочного режима среди посетителей или сотрудников.
В этом соревновании требуется классифицировать наличие маски на лице, используя изображения по фотографии. Основной целью проекта является подбор оптимальной и эффективной модели (не сильно громоздкой и быстрой), применение различных новых техник, позволяющих улучшить качество модели. 

Задача: поставлена задача создать модель, которая будет предсказывать наличие/отсутствие маски на лице.

Данные: было использовано более 14 тыс. изображений (взяты из открытого доступа с ресурса Kaggle.com), соединены несколько датасетов, чтобы получился своего рода микс данных.

В ходе работы над проектом были решены следующие задачи:

К данным изображениям TRAIN и VALIDATION была применена аугментация. Проведен анализ по распределению изображений по классам.

Обучение модели:

1. Модель. Построена сверточная нейросеть CNN  DL. На вход подавались изображения с различными лицами (в маске/без),IMG_SIZE=124, IMG_CHANNELS =3. Результаты обучения: Accuracy = 0.9453, Roc_auc = 0.9918.
2. Модель. Построена сверточная нейросеть DL на базе предобученной сети MobileNetV2 (large). На вход подавались изображения с различными лицами (в маске/без).IMG_SIZE=124, IMG_CHANNELS =3. Обучались все слои модели (так результат обучения модели на выходе лучше). Результаты обучения:Accuracy (best) = 0.9879,  Roc_auc = 0.9980, Precision = 0.9912, Recall = 0.9837, Specifity (TNR) = 0.9919, Sensivity (TPR) = 0.9837.

Файлы в репозитории содержит 3 ноутбука (они соответствуют этапам работы):

1) face-mask-detection-cv-model-vol.1 - основной ноутбук с разработкой модели (Есть также на Kaggle.com с возможностью Edit).

2) face-mask-detection-cv-predictions-vol-2 - ноутбук где обученная модель внедряется для практического использования на фото изображениях (production algorithm).

3) CV Haar cascade, MTCNN real time video, + bonus. Vol.3 -  ноутбук, продакшн модели для видео потока (video stream).

Output3.mp4 - видеофайл с примером видеострима (с обработкой алгоритма на базе модели c CV haar cascade)(формирует алгоритм ноутбука VOl.3).

OutputMTCNN1.mp4 - видеофайл с примером видеострима (с обработкой алгоритма на базе модели c MTCNN)(формирует алгоритм ноутбука VOl.3).

alarmX.jpg - пример фотофиксации (формирует алгоритм ноутбука VOl.3).

webcam.log - пример лог-файла (формирует алгоритм ноутбука VOl.3).


Никнейм на Kaggle -Pawel_MTW

Значение метрик, которых удалось добиться:
Accuracy - 0.9879,
Loss - 0.17, 
Roc_auc = 0.9980 (метрика эффективности для бизнеса)
Specifity (TNR) = 0.9919. 
Specifity (FPR) = 0.0081.
Sensivity (TPR) = 0.9837.


Выводы:
Удалось добиться решения поставленной задачи, обученная модель достаточно точно выполняет поставленную задачу. Удалось сделать интересный прототип продакшена для модели:
с возможностью анализировать видеопоток real-time (кадр за кадром), считать кол-во людей в кадре, определять наличие маски на лице, замерять дистанцию между людьми, сигнализировать и фиксировать нарушения (без маски, маленькое расстояние между людьми, превышение лимита людей) в виде log.file и фотофиксации, записи всего видеопотока в файл.

В ходе проекта удалось ближе познакомиться с алгоритмами детектирования лица на фото (CV haarcascade, MTCNN), а также ReduceLROnPlateau (система уменьшаемого LR). 

Что не получилось сделать так, как хотелось? 
Можно усовершенствовать модель, для более лучшего детектирования лица в кадре, т.к. в идеале система требует фронтальное лицо (повороты лица и наклоны снижают вероятность обнаружения лица). Не успел реализовать полноценный продакшн (video stream control service через указание клиентом только адреса IP камеры (и логин/пароль доступ к камере). Также считаю интересным внедрение в качестве сигнализирования о событиях (нарушения: без маски, мин. дистанция, макс. людей) - SMS, e-mail оповещение (с фоторассылкой или log события).
