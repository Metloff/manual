# Масштабирование
При возрастании количества данных, которые находятся у нас в БД или при увеличении количества запросов, мы с талкиваемся с тем, что скорость выполнения запросов становится неудовлитворительной. В этот момент мы задумываемся о масштабировании.

Виды масштабирования:
- Вертикальное: покупаем более мощное железо. В определенный момент становится очень дорого + всегда есть пределы.
- Вертикальное: партиционирование.
- Горизонтальное: увеличиваем количество машин (шардирование).
  
## Партиционирование
TODO

## Шардирование

Разделение данных по какому-либо признаку (id, возраст...) и хранение их в разных БД на разных серверах.

Способы получения данных из шардированной системы:
- Клиент посылает запрос сразу на все шарды
- Клиент посылает запрос в прослойку, которая уже знает, какой диапозон данных в каком шарде лежит. Самый частоиспользуемый случай.
- Клиент сам знает, по какому принципу происходит шардирование и сам посылает запросы.

### Выбор ключа

Выбор ключа сильно зависит от ваших данных и того, как они в дальнейшем будут использоваться.

От удачности выбора ключа, по которому будет происходит шардирование зависит:
- равномерность нагрузки по шардам (все запросы не идут в одну и ту же реплику, а равномерно ходят в разные)
- как часто прийдется делать запрос на несколько шардов и объединять результаты


# Разобрать
https://habr.com/ru/company/oleg-bunin/blog/309330/
https://habr.com/ru/company/oleg-bunin/blog/433370/
https://ruhighload.com/%D0%A8%D0%B0%D1%80%D0%B4%D0%B8%D0%BD%D0%B3+%D0%B8+%D1%80%D0%B5%D0%BF%D0%BB%D0%B8%D0%BA%D0%B0%D1%86%D0%B8%D1%8F
