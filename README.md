# (Не)известный солдат
## Данные по призыву времен Великой Отечественной Войны

В проекте мы использовали карточки учета военно-пересыльных пунктов, взятые с сайта ОБД Мемориал. В этом репозитории мы приводим агрегированные данные по регионам рождения, призыва и возрастам призывников. Кроме этого приведена справочная информация о населении республик.

*Важное замечание:* Слово `draft` в рамках данного репозитория переводится как "призыв", а не "черновик".

### Переписи
В папке `census/` приведена справочная информация о населении республик. Файлы:
* `census_1937.tsv`: Перепись 1937 года с разбивкой по республик. Дана по данным книги "Полвека под грифом секретно. Всесоюзная перепись населения 1937 года" за авторством В.Б.Жиромской, И.Н.Киселева, Ю.А.Полякова.
* `census_1939.tsv`: Перепись 1939 года с разбивкой по республикам и возрастным когортам. Дана по данным книги "Всесоюзная перепись населения 1939 года. Основные итоги" за авторством Ю.А.Полякова.
* `used_population.tsv`:  Численность республик, которое было взято в исследование. В наших расчетах использовалась перепись 1939 года, плюс сторонние данные о республиках Прибалтики. К сожалению, эти данные обладают большой степенью неточности  и в силу возможных фальсификаций при проведении переписи, и в силу изменения границ СССР. Так с момента проведения переписи по начала Великой Отечественной Войны к СССР были присоединены Прибалтийские республики, Западные Украина и Белоруссия, а также Бессарабия и часть приграничных территорий Финляндии. Также менялось административно-территориальное деление внутри СССР, в результате чего границы (а значит, и население отдельных республик) - менялось.

### Текстовые описания
В файле `draft_events.json` даны текстовые описания различных событий, повлиявших на призыв.
