# Мобильное приложение "Ненужные вещи"
**Основные моменты:**
- расчет метрик(удержания, времемени в приложении, частоты действий, конверсии) для различных групп пользователей

**Описание**

В приложении пользователи продают свои ненужные вещи, размещая их на доске объявлений.

**Данные**

- mobile_dataset - содержит данные о названии и времени совершения события, а также id пользователя
- mobile_sources - содержит данные о источнике, с которого установлено приложение и id пользователя

**Задача**

Главная цель - посмотреть на аудиторию приложения и выделить группы пользователей на основе их поведения.

Группы пользователей должны различаться по метрикам:
- retention rate
- время, проведённое в приложении
- частота действий
- конверсия в целевое действие — просмотр контактов

**Проделанные шаги**

- Загрузка и обзор данных
- Предобработка данных
  - Проверка и обработка пропусков
  - Изменение типов данных и переименование столцов
  - Проверка данных на аномалии и исправления
  - Проверка дубликатов
  - Объединение разных событий, связанных с поиском, в одно search
- Исследовательский анализ данных
  - Выделение сессий пользователя относительно тайм-аута.
  - Формирование пользовательского профиля. Подсчет количества событий для каждого пользователя и их распределение.
  - Источники привлечения и доля пользователей в них
  - Изучить пользователей для каждого события. Построить продуктовую воронку.
- Сегментация пользователей на основе действий
  - Сегментация пользователей определенным образом(например, по длительности сессии)
  - Рассчет следующих метрик для выделенных групп: retention rate; время, проведённое в приложении; частота действий; конверсия в целевое действие — просмотр контактов.
- Проверка статистических гипотез
  - Некоторые пользователи установили приложение по ссылке из yandex, другие — из google. Гипотеза: две эти группы демонстрируют разную конверсию в просмотры контактов.
  - Пользователи разделены на группы по времени сессии. Гипотеза - конверсии в целевое событие для пользователей из различных групп отличаются.
  
**Выводы**
- На этапе предобработки привели типы данных в столбцах к необходимым для дальнейшего анализа, объеденили два исходных датасета с событиями и данными о источниках пользователей и похожие друг на друга события объеденили в одно.
- Исходя из времени событий и таймаута между ними были выделены пользовательские сессии
- Для уникальных пользователей посчитаны:
  - среднее количество событий - 9
  - среднее количество сессий - 2
  - среднее количество событий в одной сессии - 4
  - источник привлечения пользователя не влияет на эти цифры
- Построен график периодичности событий(активность пользователей в приложении). Периодичность имеет суточный характер. К ночи активность снижается, днем она самая высокая.
- Исходя из количества уникальных пользователей для события можно сказать:
  - меньше 10% пользователей, увидевших рекомендованное объявление, перешли на него
  - 25% пользователей просмотривает фотографии в объявлениях
  - довольно много пользователей пользуются картой для отображения объявлений
  - из пользователей просмотревших контакты продавца, через приложение звонят около 20%
- На основе выделенных пользовательских профилей:
  - в период с 7 по 15 октября наблюдается увеличение числа пользователей, дальше показатели одинаковые
  - спады и увеличения числа пользователей по датам совпадают для всех источников.
  - чаще всего пользователи приходили из Яндекса, примерно одинаково из Googla и других источников.
- Пользователи разбиты на 3 группы исходя из длительности их сессий
- Различие групп по метрикам:
  - хуже всего удержание у 3-ей группы пользователей, лучше всего у 1-ой
  - дольше всех в приложении находились пользователи из 3-ей группы - 36 дней, меньше всех из 1-ой - 15 дней, из 2-ой - 24 дня
  - у 3-ей группы больше всего событий - 30 тысяч, у 1-ой меньше всего - 20 тысяч, у 2-ой - 24 тысячи
  - у 1-ой группы конверсия значительно выше двух остальных групп, 27% против 22 и 20 соответственно
- Конверсии пользователей в просмотры контактов из источников yandex и google не различаются
- Конверсии в просмотры контактов для пользователей из 2 и 3 группы не отличаются. Для пользователей из 1 и 3, а также для 1 и 2 группы отличаются.

**Рекомендации**
- Чтобы увеличить конверсию в событие просмотр контактов, то нужно стремиться уменьшать среднюю длительность сессии пользователя. Исходя из количества пользователей в разных группах, потенциал для увеличения конверсии порядка 75%. Нужно отметить, что разница между конверсиями групп пользователей значимая.
- У пользователей пришедших с Яндекса: сильно лучше динамика привлечения; удержание для 1-ой и 3-ей группы не отличается от других источников, для 2-ой группы удержание для Яндекса хуже, чем для двух других источников.
Соответственно можно делать упор на платформу Яндекс. Это даст нам прирост пользователей в группу с самой высокой конверсией и удержанием.
- Событие "просмотр фотографий" характерно для пользователей целевой 1-ой группы. Значит наличие фотографий в объявлении положительно влияет на его привлекательность для интересующих нас пользователей.
  - Можно установить обязательные правила при подаче объявления на наличие фотографий или их количество и качество.
  - Также можно продвигать на первые места при поиске объявления с фотографиями.
  - При выдаче рекомендованных объявлений(событие tips_show), нужно отображать объявления с фотографиями.

# Дашборд
Для данного проекта реализован дашборд в Tableau. Ссылка на него и пояснения находятся в проекте в разделе `Материалы`.
