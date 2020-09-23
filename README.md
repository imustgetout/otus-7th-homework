## Задача:

### скрипт для крона

который раз в час присылает на заданную почту

- X IP адресов (с наибольшим кол-вом запросов) с указанием кол-ва запросов c момента последнего запуска скрипта

- Y запрашиваемых адресов (с наибольшим кол-вом запросов) с указанием кол-ва запросов c момента последнего запуска скрипта

- все ошибки c момента последнего запуска

- список всех кодов возврата с указанием их кол-ва с момента последнего запуска

в письме должно быть прописан обрабатываемый временной диапазон

должна быть реализована защита от мультизапуска 

-----------------------------------------------------

### Реализация:

Случайно система получилась из двух скриптов.
Первый скрипт вычисляет последнее время запуска второго скрипта(в секундах, по atime, вывод команды stat) и запускает второй скрипт с параметром в виде времени последнего запуска(+ создание блокировки от повторного запуска с помощью flock) и отправляет вывод на почту.

Второй скрипт печатает время начальной записи и текущее время как интервал обработки. Далее временные записи из access.log преобразуются в дату (в секундах), сравниваются с последним временем запуска, переданным скрипту. Как только дата становиться больше последнего времени запуска, вычисляем номер строки этой записи.

Читая access.log с нужной строки, до конца файла производим требуемые действия, и выводим данные.

Sorry за название скрипта.
