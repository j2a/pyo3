{% meta %}
    tags: [mine,django,sqlalchemy]
    title: Что это было?
{% endmeta %}

{% mark body %}{% filter markdown %}
Часть читателей, видимо заметила некоторый период непонятного состояния блога. То 500 ISE, то работает, то таймаут, то "under maintenance", то опять 500 ISE. Другая часть получила кучу спама о новых комментариях.
<!--more-->

В общем, дело оказалось довольно безхитростным, но наложившемся на форс-мажор на работе и отсутствием времени дома. До вчера у меня использовался SQLite как самый простой вариант базы данных. Но у этой "СУБД" есть один момент: при записи блокируется вся база целиком. Как следствие, если есть "долгоиграющий" процесс, открывший БД на запись, то все остальные с чтением обламываются.

В общем, вчера перед сном решил быстренько поменять SQLite на MySQL, понадеявшись на `manage.py dumpdata/loaddata`. Поскольку всё это планировалось "быстренько", то не удосужился проверить на домашней машине. В итоге, данные не перенёс, лёг поздно, блог отправил в maintenance mode. С утра встал, не выспался, удостоверился, что штатными средствами Django получаю от ворот поворот, начал писать небольшую "вещь" для миграции с SQLite на MySQL. После относительного разгребания груды дел на работе, протестировал на связке SQLite->PostgreSQL и SQLite->MySQL, и, немного "доточив", положил в песочницу: [sandbox/movedb](http://hg.pyobject.ru/sandbox/file/tip/movedb/).

Ну и поскольку вы блог читаете, то значит данные я благополучно перенёс.

P.S. А еще эта штука сама разруливает порядок вставки таблиц с внешними ключами ;)
{% endfilter %}{% endmark %}
