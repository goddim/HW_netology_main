### Домашнее задание к занятию «SQL. Часть 2»
Инструкция по выполнению домашнего задания
Сделайте fork репозитория c шаблоном решения к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/gitlab-hw или https://github.com/имя-вашего-репозитория/8-03-hw).
Выполните клонирование этого репозитория к себе на ПК с помощью команды git clone.
Выполните домашнее задание и заполните у себя локально этот файл README.md:
впишите вверху название занятия и ваши фамилию и имя;
в каждом задании добавьте решение в требуемом виде: текст/код/скриншоты/ссылка;
для корректного добавления скриншотов воспользуйтесь инструкцией «Как вставить скриншот в шаблон с решением»;
при оформлении используйте возможности языка разметки md. Коротко об этом можно посмотреть в инструкции по MarkDown.
После завершения работы над домашним заданием сделайте коммит (git commit -m "comment") и отправьте его на Github (git push origin).
Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
Любые вопросы задавайте в чате учебной группы и/или в разделе «Вопросы по заданию» в личном кабинете.
Желаем успехов в выполнении домашнего задания.

Задание можно выполнить как в любом IDE, так и в командной строке.

### Задание 1
Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей, и выведите в результат следующую информацию:
фамилия и имя сотрудника из этого магазина;
город нахождения магазина;
количество пользователей, закреплённых в этом магазине.
### Ответ

SELECT 
    CONCAT(staff.first_name, ' ', staff.last_name) AS сотрудник,
    city.city AS город,
    COUNT(customer.customer_id) AS количество_пользователей
FROM 
    store
JOIN staff ON store.manager_staff_id = staff.staff_id
JOIN address ON store.address_id = address.address_id
JOIN city ON address.city_id = city.city_id
JOIN customer ON store.store_id = customer.store_id
GROUP BY 
    store.store_id
HAVING 
    COUNT(customer.customer_id) > 300;

    
![image](https://github.com/goddim/HW_netology_main/assets/132663924/151b13d1-2188-43a0-8c7b-c5952f058197)


### Задание 2
Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.
### Ответ

SELECT COUNT(1) as фильмы_больше_ср_продолжительности, AVG(length) as средняя_продолжительность
FROM film
WHERE length > (SELECT AVG(length) FROM film);
![image](https://github.com/goddim/HW_netology_main/assets/132663924/2080975a-b157-44e1-a12a-7232c742fec4)

### Задание 3
Получите информацию, за какой месяц была получена наибольшая сумма платежей, и добавьте информацию по количеству аренд за этот месяц.
### Ответ
SELECT
    DATE_FORMAT(payment.payment_date, '%m') AS месяц,
    MONTHNAME(payment.payment_date) AS название_месяца,
    SUM(payment.amount) AS сумма_платежей,
    COUNT(rental.rental_id) AS количество_аренд
FROM
    payment
JOIN rental ON payment.rental_id = rental.rental_id
GROUP BY
    месяц, название_месяца
ORDER BY
    сумма_платежей DESC
LIMIT 1;

![image](https://github.com/goddim/HW_netology_main/assets/132663924/428c0d1a-4eba-4f19-a49d-c793232cbcdb)
