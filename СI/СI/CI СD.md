
### Задание 1

**Что нужно сделать:**

1. Установите себе jenkins по инструкции из лекции или любым другим способом из официальной документации. Использовать Docker в этом задании нежелательно.
2. Установите на машину с jenkins [golang](https://golang.org/doc/install).
3. Используя свой аккаунт на GitHub, сделайте себе форк [репозитория](https://github.com/netology-code/sdvps-materials.git). В этом же репозитории находится [дополнительный материал для выполнения ДЗ](https://github.com/netology-code/sdvps-materials/blob/main/CICD/8.2-hw.md).
3. Создайте в jenkins Freestyle Project, подключите получившийся репозиторий к нему и произведите запуск тестов и сборку проекта ```go test .``` и  ```docker build .```.

В качестве ответа пришлите скриншоты с настройками проекта и результатами выполнения сборки.
### ОТВЕТ
![image](https://github.com/goddim/HW_netology_main/assets/132663924/69ae7c92-c4d9-4a4d-954d-d5c3919f4c2f)

![image](https://github.com/goddim/HW_netology_main/assets/132663924/24d1c593-5b0a-48f5-ba61-ca41af63ec77)

---

### Задание 2

**Что нужно сделать:**

1. Создайте новый проект pipeline.
2. Перепишите сборку из задания 1 на declarative в виде кода.

В качестве ответа пришлите скриншоты с настройками проекта и результатами выполнения сборки.
### ОТВЕТ

![image](https://github.com/goddim/HW_netology_main/assets/132663924/6c95bfaf-1949-4326-936c-32bd57a3174b)

скрипт
pipeline {
    agent any

    stages {
        stage('Clone repository') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/goddim/sdvps-materials.git'
            }
        }
        
        stage('Run tests') {
            steps {
                sh 'go test .'
            }
        }
        
        stage('Build Docker image') {
            steps {
                sh 'docker build .'
            }
        }
    }
}

![image](https://github.com/goddim/HW_netology_main/assets/132663924/dc9bf774-c63d-47fb-a24b-35521a1faa67)

---

### Задание 3

**Что нужно сделать:**

1. Установите на машину Nexus.
1. Создайте raw-hosted репозиторий.
1. Измените pipeline так, чтобы вместо Docker-образа собирался бинарный go-файл. Команду можно скопировать из Dockerfile.
1. Загрузите файл в репозиторий с помощью jenkins.

В качестве ответа пришлите скриншоты с настройками проекта и результатами выполнения сборки.
### ОТВЕТ
![image](https://github.com/goddim/HW_netology_main/assets/132663924/de202510-4a8f-4922-b9ea-346bed4cc36e)
![image](https://github.com/goddim/HW_netology_main/assets/132663924/3594ceaf-470b-42fd-9aa8-b4c254c1a189)
![image](https://github.com/goddim/HW_netology_main/assets/132663924/e735e3fa-91cf-427b-9c01-31d7cc895944)

---
## Дополнительные задания* (со звёздочкой)

Их выполнение необязательное и не влияет на получение зачёта по домашнему заданию. Можете их решить, если хотите лучше разобраться в материале.

---

### Задание 4*

Придумайте способ версионировать приложение, чтобы каждый следующий запуск сборки присваивал имени файла новую версию. Таким образом, в репозитории Nexus будет храниться история релизов.

Подсказка: используйте переменную BUILD_NUMBER.

В качестве ответа пришлите скриншоты с настройками проекта и результатами выполнения сборки.
