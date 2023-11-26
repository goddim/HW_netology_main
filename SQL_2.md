Домашнее задание к занятию 2. «SQL»

## Задача 1

Используя Docker, поднимите инстанс PostgreSQL (версию 12) c 2 volume, 
в который будут складываться данные БД и бэкапы.

Приведите получившуюся команду или docker-compose-манифест.
## ОТВЕТ
![image](https://github.com/goddim/HW_netology_main/assets/132663924/3bf84e0a-582c-4553-9220-860d0e4be5cc)
![image](https://github.com/goddim/HW_netology_main/assets/132663924/aa112312-b5ab-4334-944c-3eb6207eeaba)

## Задача 2

- создайте пользователя test-admin-user и БД test_db;
- в БД test_db создайте таблицу orders и clients (спeцификация таблиц ниже);
- предоставьте привилегии на все операции пользователю test-admin-user на таблицы БД test_db;
- создайте пользователя test-simple-user;
- предоставьте пользователю test-simple-user права на SELECT/INSERT/UPDATE/DELETE этих таблиц БД test_db.

Таблица orders:

- id (serial primary key);
- наименование (string);
- цена (integer).

Таблица clients:

- id (serial primary key);
- фамилия (string);
- страна проживания (string, index);
- заказ (foreign key orders).

Приведите:

- итоговый список БД после выполнения пунктов выше;
- описание таблиц (describe);
- SQL-запрос для выдачи списка пользователей с правами над таблицами test_db;
- список пользователей с правами над таблицами test_db.
## ОТВЕТ
![image](https://github.com/goddim/HW_netology_main/assets/132663924/0ece8616-6ddf-47b9-8c96-b399ef7b4f55)
![image](https://github.com/goddim/HW_netology_main/assets/132663924/3b5888fa-9628-4c15-aa24-2aad6ec4ab69)
![image](https://github.com/goddim/HW_netology_main/assets/132663924/a4a66a89-14aa-434e-b3a3-91e4ab9d6b67)


## Задача 3

Используя SQL-синтаксис, наполните таблицы следующими тестовыми данными:

Таблица orders

|Наименование|цена|
|------------|----|
|Шоколад| 10 |
|Принтер| 3000 |
|Книга| 500 |
|Монитор| 7000|
|Гитара| 4000|

Таблица clients

|ФИО|Страна проживания|
|------------|----|
|Иванов Иван Иванович| USA |
|Петров Петр Петрович| Canada |
|Иоганн Себастьян Бах| Japan |
|Ронни Джеймс Дио| Russia|
|Ritchie Blackmore| Russia|

Используя SQL-синтаксис:
- вычислите количество записей для каждой таблицы.

Приведите в ответе:

    - запросы,
    - результаты их выполнения.
## ОТВЕТ
![image](https://github.com/goddim/HW_netology_main/assets/132663924/cbac7407-10cd-4e6f-a097-2c1fafcd0554)
![image](https://github.com/goddim/HW_netology_main/assets/132663924/ca825cd9-fc98-42c6-813d-8d6e2e3a174e)

## Задача 4

Часть пользователей из таблицы clients решили оформить заказы из таблицы orders.

Используя foreign keys, свяжите записи из таблиц, согласно таблице:

|ФИО|Заказ|
|------------|----|
|Иванов Иван Иванович| Книга |
|Петров Петр Петрович| Монитор |
|Иоганн Себастьян Бах| Гитара |

Приведите SQL-запросы для выполнения этих операций.

Приведите SQL-запрос для выдачи всех пользователей, которые совершили заказ, а также вывод этого запроса.
 
Подсказка: используйте директиву `UPDATE`.
## ОТВЕТ
![image](https://github.com/goddim/HW_netology_main/assets/132663924/0b39ac63-842b-4133-8ddd-2faefe1fa218)



## Задача 5

Получите полную информацию по выполнению запроса выдачи всех пользователей из задачи 4 
(используя директиву EXPLAIN).

Приведите получившийся результат и объясните, что значат полученные значения.
## ОТВЕТ

![image](https://github.com/goddim/HW_netology_main/assets/132663924/0d8b0997-7bd8-497d-bddc-549faa8b5acc)
- Seq Scan on clients: Планировщик запросов решил выполнить последовательное сканирование (Seq Scan) всей таблицы clients.
(cost=0.00..10.70 rows=70 width=520): Это оценка затрат на выполнение запроса. В данном случае, оценка затрат составляет от 0 до 10.70, и ожидаемое количество строк - 70.
- Filter: ("заказ" IS NOT NULL): Условие фильтрации, где проверяется, что значение столбца заказ не равно NULL.
Данный план выполнения показывает, что PostgreSQL использует последовательное сканирование всей таблицы clients, фильтруя строки по условию "заказ" IS NOT NULL. В данном случае, таблица, вероятно, небольшая (оценка затрат низкая), поэтому использование последовательного сканирования с фильтрацией не является проблемой для производительности.


## Задача 6

Создайте бэкап БД test_db и поместите его в volume, предназначенный для бэкапов (см. задачу 1).

Остановите контейнер с PostgreSQL, но не удаляйте volumes.

Поднимите новый пустой контейнер с PostgreSQL.

Восстановите БД test_db в новом контейнере.

Приведите список операций, который вы применяли для бэкапа данных и восстановления. 
## ОТВЕТ