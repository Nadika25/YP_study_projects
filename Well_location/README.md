# Описание работы
Добывающая компания «ГлавРосГосНефть» хочет узнать, где бурить новую скважину. В нескольких регионах собрали характеристики для скважин: качество нефти и объем её запасов. Необходимо определить регион с максимальной суммарной прибылью отобранных скважин.

# Результат работы
Во время **исследовательского анализа** данных обнаружено:

* В **регионе 1** наблюдается умеренная положительная корреляция (0.48) между объемом запасов скважин и столбцом f2, а также умеренная отрицательная корреляция (-0.44) между признаками f0 и f1.
* В **регионе 2** наблюдается весьма высокая корреляция (1) между объемом запасов скважин и столбцом f2.
* В **регионе 3** наблюдается умеренная корреляция (0.45) между объемом запасов скважин и столбцом f2.

Также по всем данным были **изучены гистограммы** и проверены признаки на **выбросы**.

По **региону 1** обнаружили выбросы в столбце f2 в количестве 247 строк, а также одну скважину с нулевым запасом нефти.

По **региону 2** обнаружили выбросы в столбце  f1 в количестве 441 строки, а также 8235 скважин c нулевым запасом нефти.

По **региону 3** обнаружили выбросы в столбце f0 в количестве 382 строки, выбросы в столбце f1 в количестве 388 строк,  выбросы в столбце f2 в количестве 567 строк, а также одну скважину с нулевым запасом нефти.

Выбросы трогать не стали. Скважины с  нулевым запасом нефти также оставили без изменений.

Далее перешли к **обучению модели**. Данные были разделены на обучающую и валидационную выборки. Все модели были обучены, а затем для данных каждого региона найдены: реальный средний запас сырья, предсказанный средний запас сырья и среднеквадратическая ошибка RMSE.

Результаты:

**Регион 1:**
Реальный средний запас сырья: 92.08
Предсказанный средний запас сырья: 92.59
RMSE: 37.58

**Регион 2:**
Реальный средний запас сырья: 68.72
Предсказанный средний запас сырья: 68.73
RMSE: 0.89

**Регион 3:**
Реальный средний запас сырья: 94.88
Предсказанный средний запас сырья: 94.97
RMSE: 40.03

Величина отклонения предсказанного среднего запаса сырья от реального среднего запаса сырья для регионов 1 и 3 примерно одинаковая. Самую большую точность прогноза показала модель региона 2.

На следующем этапе подготовились к **расчету прибыли**. Задали переменные для входных значений. Определили, что для безубыточной разработки необходимо **111.11 тыс. баррелей сырья**, нашли средний запас сырья в каждом регионе. 

Результаты:

* **Регион 1**:
 - Средний запас: **92.50 тыс. баррелей**
 - Процент скважин с объёмом больше необходимого: 36.58%
 - Количество скважин с объёмом больше необходимого: 36583
 
 
* **Регион 2**:
 - Средний запас: **68.83 тыс. баррелей**
 - Процент скважин с объёмом больше необходимого: 16.54%
 - Количество скважин с объёмом больше необходимого: 16537
 
* **Регион 3**:
 - Средний запас: **95.00 тыс. баррелей**
 - Процент скважин с объёмом больше необходимого: 38.18%
 - Количество скважин с объёмом больше необходимого: 38178
 
Средние запасы сырья во всех регионах оказались ниже необходимого порога. Перешли к выявлению наиболее выгодных скважин в каждом регионе. Рассчитали прибыли и риски, учитывая, что компания исследует 500 точек, а разработает 200 лучших.

Результат:

* **Регион 1**:
 - Средняя выручка с 200-т лучших скважин: 425938526.91
 - доверительный интервал (95%): [-102090094.83793654, 947976353.3583689]
 - Риск получения убытков: 6.0
 
 
* **Регион 2**:
 - Средняя выручка с 200-т лучших скважин: 518259493.7
 - Доверительный интервал (95%): [128123231.43308444, 953612982.0669085]
 - Риск получения убытков: 0.3
 
* **Регион 3**:
- Средняя выручка с 200-т лучших скважин: 420194005.34
- Доверительный интервал (95%): [-115852609.16001143, 989629939.8445739]
- Риск получения убытков: 6.2

Как видно, все три региона являются прибыльными. Самая высокая выручка из 200-т лучших скважин в регионе 2. Доверительный интервал уже и, риск получения убытков меньше также в регионе 2. В регионе 1 и в регионе 2 высока вероятность убытков значительно выше. Таким образом по всем показателям **наиболее выгодный регион для разработки - регион 2**.