# (Не)известный солдат
## Данные по призыву времен Великой Отечественной Войны

В проекте мы использовали карточки учета военно-пересыльных пунктов, взятые с сайта ОБД Мемориал. В этом репозитории мы приводим агрегированные данные по регионам рождения, призыва и возрастам призывников. Кроме этого приведена справочная информация о населении республик.

*Важное замечание:* Слово `draft` в рамках данного репозитория переводится как "призыв", а не "черновик".

### Переписи
В папке `census/` приведена справочная информация о населении республик. Файлы:
* `census_1937.tsv`: Перепись 1937 года с разбивкой по республик. Дана по данным книги "Полвека под грифом секретно. Всесоюзная перепись населения 1937 года" за авторством В.Б.Жиромской, И.Н.Киселева, Ю.А.Полякова.
* `census_1939.tsv`: Перепись 1939 года с разбивкой по республикам и возрастным когортам. Дана по данным книги "Всесоюзная перепись населения 1939 года. Основные итоги" за авторством Ю.А.Полякова.
* `used_population.tsv`:  Численность республик, которое было взято в исследование. В наших расчетах использовалась перепись 1939 года, плюс сторонние данные о республиках Прибалтики. К сожалению, эти данные обладают большой степенью неточности  и в силу возможных фальсификаций при проведении переписи, и в силу изменения границ СССР. Так с момента проведения переписи до начала Великой Отечественной Войны к СССР были присоединены Прибалтийские республики, Западные Украина и Белоруссия, а также Бессарабия и часть приграничных территорий Финляндии. Также менялось административно-территориальное деление внутри СССР, в результате чего границы (а значит, и население отдельных республик) - менялось.

### Текстовые описания
В файле `draft_events.json` даны текстовые описания различных событий, повлиявших на призыв.

### Детальное распределение карточек
Наиболее грубое распределение карточек (суммарное количество карточек по республике призыва) приведено в файле `total_draft_by_region.tsv`.

В файле `num_cards_by_draft_and_birth_date_and_region.tsv` приведена детальная разбивка карточек по нескольким признакам. Каждая строка указывает, сколько было карточек, в которых указаны определенные республика и дата призыва (с точностью до месяца), а также определенные республика и год (но не месяц) рождения. Количество карточек указано в столбце `num_cards`.

Если в строке какое-то из полей не заполнено, значит было столько карточек, в которых это поле не заполнено или заполнено недостаточно, чтобы восстановить релевантное значение. Например, в графе региона указано название села, но не упомянуто, в какой республике он находится.

### Распределение карточек по месяцам призыва
В папке `regions/` расположены файлы (по одному на каждую республику) с распределением призыва по месяцам и возрастам. Столбец `num_cards_extrapolated` указывает число карточек людей, призванных в этом месяце и году, экстраполированное, как указано в соответствующем разделе. Также приведено кумулятивное распределение призывников по возрастам.

Менее детальное распределение (не учитывающее возрастной состав призывников) по всем республикам приведено в файле `draft_by_region_per_month.tsv`.

## Экстраполяция данных

### Фильтрация данных
Мы отбросили записи, которые предположительно принадлежали одному и тому же человеку. Полное дублирование ФИО и даты-места рождения почти не встречалось, но например, иногда военно-призывные пункты оставляют о солдате две записи: о прибытии и убытии. Из пары таких записей мы оставляли одну. Также мы отбросили все записи, в которых были указаны даты призыва, выходящие за рамки 1939-1945 годов.

### Нормализация данных
Если в карточке указано название области, мы обычно можем дозаполнить республику (см. файлы в папке `region_curation/`). Под республиками здесь подразумеваются крупные образования, такие как РСФСР. Например, карточка из Башкирской АССР в этих данных отнесена к РСФСР, а карточка из Ровенской области будет отнесена к УССР.

### Восстановление пропусков
Для подготовки итоговых графиков используются экстраполированные данные. В файле `num_cards_by_draft_and_birth_date_and_region.tsv` эти данные указаны в столбце `num_cards_extrapolated`.
Экстраполяция сделана, поскольку у многих карточек часть полей не была заполнена. С её помощью мы пытаемся оценить, сколько карточек из тех, на которых республика призыва не указана, относятся к которой республике.

Для восстановления республики призыва используется следующая простая эвристика: чаще всего человек, родившийся в республике X, в ней же и призывается, несколько реже призывается в республике Y и совсем редко - в республике Z. По карточкам, на которых указаны места и рождения, и призыва, мы восстанавливаем пропорцию, в которой распределялись уроженцы разных республик по местам призыва. Карточки, в которых указана лишь республика рождения, но не призыва, мы распределили в той же пропорции. Карточки, на которых не были указаны ни республика рождения, ни республика призыва были распределены в том же соотношении, в котором были распределены карточки без республики рождения, но с республикой призыва (это соответствует вышеописанной процедуре, если считать прочерк в месте рождения названием фиктивной республики).

Все прочие поля (дата рождения и призыва) у карточек, распределенных таким образом, мы оставляли неизменными.

По карточкам, для которых известны обе даты (рождения и призыва) мы оценили распределение возрастов призывников. В файлах со сводными данными по регионам в папке `regions/` можно найти кумулятивное распределение возрастов призывников в каждый из проанализированных месяцов. Например, колонка rate_less_than_22 означает долю призывников возраста до 21 года включительно (less than - это строгое неравенство).

Мы не применяли сходную экстраполяцию для восстановления дат. Для графиков призыва по месяцам мы использовали только карточки, у которых указана дата призыва (с точностью до месяца).
