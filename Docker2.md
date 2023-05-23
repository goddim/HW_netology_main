# Домашнее задание к занятию «Docker. Часть 2»
Все задания выполняйте на основе конфигов из лекции.
В заданиях описаны те параметры, которые необходимо изменить.
Если параметр не упомянут вообще, значит, его нужно оставить таким, какой он был в лекции.
Если в каком-то задании, например, в задании 2, нужно изменить параметр, подразумевается, что во всех следующих заданиях будет использоваться уже изменённый параметр.
Выполнив все задания без звёздочки, вы должны получить полнофункциональный сервис.
Любые вопросы по решению задач задавайте в чате учебной группы.


## Задание 1
Напишите ответ в свободной форме, не больше одного абзаца текста.

Установите Docker Compose и опишите, для чего он нужен и как может улучшить вашу жизнь.
### Ответ
Docker Compose  позволяет управлять многоконтейнерными приложениями с использованием файлов конфигурации. Он упрощает запуск и управление несколькими контейнерами Docker, объединяя их в единую систему.

Docker Compose может улучшить жизнь:

Упрощенное развертывание приложений, повторяемость и портативность, управление контейнерами и сетями, воспроизводимость тестового окружения, масштабирование и управление ресурсами, команды для управления ресурсами, легкое восстановление и обновление, расширяемость.

## Задание 2
Выполните действия и приложите текст конфига на этом этапе.

Создайте файл docker-compose.yml и внесите туда первичные настройки:

version;
services;
networks.
При выполнении задания используйте подсеть 172.22.0.0. Ваша подсеть должна называться: <ваши фамилия и инициалы>-my-netology-hw.
### Ответ
![image](https://github.com/goddim/HW_netology_main/assets/132663924/051f90ec-973d-46ae-a01b-4dd4b46eda8b)


## Задание 3
Выполните действия и приложите текст конфига текущего сервиса:

Установите PostgreSQL с именем контейнера <ваши фамилия и инициалы>-netology-db.
Предсоздайте БД <ваши фамилия и инициалы>-db.
Задайте пароль пользователя postgres, как <ваши фамилия и инициалы>12!3!!
Пример названия контейнера: ivanovii-netology-db.
Назначьте для данного контейнера статический IP из подсети 172.22.0.0/24.
### Ответ
![image](https://github.com/goddim/HW_netology_main/assets/132663924/7a19b8ab-e90d-489c-8d88-d58c4dd4c847)


## Задание 4
Выполните действия:

Установите pgAdmin с именем контейнера <ваши фамилия и инициалы>-pgadmin.
Задайте логин администратора pgAdmin <ваши фамилия и инициалы>@ilove-netology.com и пароль на выбор.
Назначьте для данного контейнера статический IP из подсети 172.22.0.0/24.
Прокиньте на 80 порт контейнера порт 61231.
В качестве решения приложите:

текст конфига текущего сервиса;
скриншот админки pgAdmin.

### Ответ
![image](https://github.com/goddim/HW_netology_main/assets/132663924/dcb84528-71ad-42ab-9e60-12811254dda9)


![image](https://github.com/goddim/HW_netology_main/assets/132663924/47bda9c3-811e-49d0-9b6b-6dafc701ca25)

## Задание 5
Выполните действия и приложите текст конфига текущего сервиса:

Установите Zabbix Server с именем контейнера <ваши фамилия и инициалы>-zabbix-netology.
Настройте его подключение к вашему СУБД.
Назначьте для данного контейнера статический IP из подсети 172.22.0.0/24.
### Ответ
![image](https://github.com/goddim/HW_netology_main/assets/132663924/77d18cdd-cd03-486b-aa38-e40244d22c28)




## Задание 6
Выполните действия и приложите текст конфига текущего сервиса:

Установите Zabbix Frontend с именем контейнера <ваши фамилия и инициалы>-netology-zabbix-frontend.
Настройте его подключение к вашему СУБД.
Назначьте для данного контейнера статический IP из подсети 172.22.0.0/24.
### Ответ
![image](https://github.com/goddim/HW_netology_main/assets/132663924/b23af948-a44b-4bbb-a75c-277d6f21509f)



## Задание 7
Выполните действия.

Настройте линки, чтобы контейнеры запускались только в момент, когда запущены контейнеры, от которых они зависят.

В качестве решения приложите:

текст конфига целиком;
скриншот команды docker ps;
скриншот авторизации в админке Zabbix.
### Ответ
![image](https://github.com/goddim/HW_netology_main/assets/132663924/86b7dfb4-df81-4c36-8857-ab600af5de8d)
![image](https://github.com/goddim/HW_netology_main/assets/132663924/8eec51ed-e6ea-4faa-8f81-a6a575238bec)
![image](https://github.com/goddim/HW_netology_main/assets/132663924/6300e85c-c912-4ded-989e-5bd12a328960)

version: '3'

services:
  netology-db:
    image: postgres:latest
    container_name: yashkinvo-netology-db
    ports:
      - 5432:5432
    volumes:
      - ./pg_data:/var/lib/postgresql/data/pgdata
    environment:
      - POSTGRES_PASSWORD=yashkinvo12!3!!
      - POSTGRES_DB=yashkinvo_db
      - PGDATA=/var/lib/postgresql/data/pgdata
    networks:
      yashkinvo-my-netology-hw:
        ipv4_address: 172.22.0.2
    restart: always

  pgadmin:
    image: dpage/pgadmin4
    container_name: yashkinvo-pgadmin
    environment:
      - PGADMIN_DEFAULT_EMAIL=yashkinvo@ilove-netology.com
      - PGADMIN_DEFAULT_PASSWORD=yashkinvo12!3!!
    ports:
      - "61231:80"
    networks:
       yashkinvo-my-netology-hw:
         ipv4_address: 172.22.0.3
    restart: always

  zabbix-server:
    image: zabbix/zabbix-server-pgsql
    depends_on:
      - netology-db
    container_name: yashkinvo-zabbix-netology
    environment:
      - DB_SERVER_HOST=172.22.0.2
      - POSTGRES_USER=postgres
      - POSTGRES_PASSWORD=123
    ports:
      - "10051:10051"
    networks:
       yashkinvo-my-netology-hw:
         ipv4_address: 172.22.0.4
    restart: always

  zabbix_wgui:
    image: zabbix/zabbix-web-apache-pgsql
    depends_on:
      - netology-db
      - zabbix-server
    container_name: yashkinvo-netology-zabbix-frontend
    environment:
      - DB_SERVER_HOST=172.22.0.2
      - POSTGRES_USER=postgres
      - POSTGRES_PASSWORD=123
      - ZBX_SERVER_HOST=zabbix_wgui
      - PHP_TZ
      - DB_SERVER_HOST=zabbix_wgui
      - PHP_TZ=Europe/Moscow
    ports:
      - "80:8080"
      - "443:8443"
    networks:
       yashkinvo-my-netology-hw:
         ipv4_address: 172.22.0.5
    restart: always

networks:
  yashkinvo-my-netology-hw:
    driver: bridge
    ipam:
      config:
        - subnet: 172.22.0.0/24



## Задание 8
Выполните действия:

Убейте все контейнеры и потом удалите их.
Приложите скриншот консоли с проделанными действиями.
### Ответ
![image](https://github.com/goddim/HW_netology_main/assets/132663924/958dff73-0c3f-4294-a230-30e3d2185a15)

Дополнительные задания* (со звёздочкой)
Их выполнение необязательное и не влияет на получение зачёта по домашнему заданию. Можете их решить, если хотите лучше разобраться в материале.


Задание 9*
Запустите свой сценарий на чистом железе без предзагруженных образов.

Ответьте на вопросы в свободной форме:

Сколько ушло времени на то, чтобы развернуть на чистом железе написанный вами сценарий?
Чем вы занимались в процессе создания сценария так, как это видите вы?
Что бы вы улучшили в сценарии развёртывания?
### Ответ
затрачено - минут

Одним из возможных улучшений в сценарии развёртывания может быть добавление инструкций по проверке доступности контейнеров после их запуска, чтобы убедиться, что они работают корректно. Также, стоит убедиться, что используемые образы контейнеров актуальны и безопасны, обновлять их до последних версий.

Кроме того, можно рассмотреть вариант добавления скриптов и конфигурационных файлов для автоматической настройки контейнеров, если требуется дополнительная настройка или настройка окружения.




