# Расчет метрик продукта *(онлайн курсы)*, А/В тестирование

## Общее описание:
### Задание 1. A/B–тестирование

1. Условие

Одной из основных задач аналитикака в нашей команде является корректное проведение экспериментов. Для этого мы применяем метод A/B–тестирования. В ходе тестирования одной гипотезы целевой группе была предложена новая механика оплаты услуг на сайте, у контрольной группы оставалась базовая механика. В качестве задания Вам необходимо проанализировать итоги эксперимента и сделать вывод, стоит ли запускать новую механику оплаты на всех пользователей.

2. Входные данные

В качестве входных данных Вы имеете 4 csv-файла:

 - `groups.csv` - файл с информацией о принадлежности пользователя к контрольной или экспериментальной группе (А – контроль, B – целевая группа) 
 - `groups_add.csv` - дополнительный файл с пользователями, который вам прислали спустя 2 дня после передачи данных
 - `active_studs.csv` - файл с информацией о пользователях, которые зашли на платформу в дни проведения эксперимента. 
 - `checks.csv` - файл с информацией об оплатах пользователей в дни проведения эксперимента
 
3. Вопросы

 - На какие метрики Вы смотрите в ходе анализа и почему?
 - Имеются ли различия в показателях и с чем они могут быть связаны?
 - Являются ли эти различия статистически значимыми?
 - Стоит ли запускать новую механику на всех пользователей?

### Задание 2. SQL

1. Очень усердные ученики.

1.1 Условие

Образовательные курсы состоят из различных уроков, каждый из которых состоит из нескольких маленьких заданий. Каждое такое маленькое задание называется "горошиной".

Назовём очень усердным учеником того пользователя, который хотя бы раз за текущий месяц правильно решил 20 горошин.

1.2 Задача

Дана таблица `default.peas`:

Название атрибута|Тип атрибута|Смысловое значение
-----------------|-------------|------------------
st_id|int|ID ученика
timest|timestamp|Время решения карточки
correct|bool|Правильно ли решена горошина?
subject|text|Дисциплина, в которой находится горошина

Необходимо написать оптимальный запрос, который даст информацию о количестве очень усердных студентов.
- NB! Под усердным студентом мы понимаем студента, который правильно решил 20 задач за текущий месяц. 
- 
2. Оптимизация воронки

2.1 Условие

Образовательная платформа предлагает пройти студентам курсы по модели trial: студент может решить бесплатно лишь 30 горошин в день. Для неограниченного количества заданий в определенной дисциплине студенту необходимо приобрести полный доступ. Команда провела эксперимент, где был протестирован новый экран оплаты.

2.2 Задача

Дана таблицы: `default.peas` (см. выше), `default.studs`:
Название атрибута|  Тип атрибута|   Смысловое значение
-----------------|-------------|------------------
st_id|  int|     ID ученика
test_grp|   text    | Метка ученика в данном эксперименте

и `default.final_project_check`:

Название атрибута|  Тип атрибута|   Смысловое значение
-----------------|-------------|------------------
st_id   |int    |ID ученика
sale_time|  timestamp|  Время покупки
money|  int|    Цена, по которой приобрели данный курс
subject|    text | Предмет

Необходимо в одном запросе выгрузить следующую информацию о группах пользователей:

- ARPU 
- ARPAU 
- CR в покупку 
- СR активного пользователя в покупку 
- CR пользователя из активности по математике (`subject = 'math'`) в покупку курса по математике

ARPU считается относительно всех пользователей, попавших в группы.

Активным считается пользователь, за все время решивший больше 10 задач правильно в любых дисциплинах.

Активным по математике считается пользователь, за все время решивший 2 или больше задач правильно по математике.


### Задание 3. Python
3.1 Задача

1. Реализуйте функцию, которая будет автоматически подгружать информацию из дополнительного файла `groups_add.csv` (заголовки могут отличаться) и на основании дополнительных параметров пересчитывать метрики.
2. Реализуйте функцию, которая будет строить графики по получаемым метрикам.
