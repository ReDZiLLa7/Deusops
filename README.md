# Deusops

Перед выполнением данной лабораторной работы, приведем рабочее место в порядок, настроив удобную систему папок

Вот так будет выглядеть домашняя директория Ansible:

![image](https://github.com/user-attachments/assets/fac3258f-307b-4e74-a8da-33c249722f8b)

## 1. Инициализация структуры роли “Docker” через Ansible-Galaxy

Чтобы инициализировать роль "Docker" через Ansible-Galaxy, нужно выполнить команду ниже в папке roles:

```
ansible-galaxy init Docker
```

![image](https://github.com/user-attachments/assets/5d17fc59-4755-45be-bfbf-348958be0d89)

## 2. Вынесение задач, относящихся к Docker в отдульную роль

Для этого зайдем в папку roles/Docker/tasks/ и добавим в файл main.yml часть нашего старого playbook:

![image](https://github.com/user-attachments/assets/37fc7fe2-a95c-4732-b200-91da86ebd6af)

## 3. Параметризация роли через переменные

Далее зайдем в папку roles/Docker/defaults/ и вынесем в файл main.yml переменные, которые в дальнейшем можно будет использовать внутри playbook:

![image](https://github.com/user-attachments/assets/ce4dd20d-211d-4052-ba27-d4d78cc9e89e)

Также заменим эти переменные внутри файла main.yml в директории roles/Docker/tasks/:

![image](https://github.com/user-attachments/assets/37fc7fe2-a95c-4732-b200-91da86ebd6af)

## 4. Создание нового репозитория и push роли "Docker" на него:

![image](https://github.com/user-attachments/assets/d589fbc8-ce5d-4095-a871-f030cd2b79fb)

Нам также нужно поменять основной playbook, в домашней директории, deploy.yml, добавив туда роль "docker", а также оставив только нужные tasks:

![image](https://github.com/user-attachments/assets/14aa201e-e6d6-44e9-a2bb-2a2a9bdb0841)

## 5. Создание файла requirements.yml для установки роли Docker из репозитория

Создаем файл в домашней директории и вносим туда данные с нашего удаленного репозитория:

![image](https://github.com/user-attachments/assets/a04c0324-52f2-4054-a40e-773bf52a8fc8)

## 6. Запуск приложения на нодах группы [app] с использованием ansible-playbook и роли “docker”

![image](https://github.com/user-attachments/assets/dc3bdb56-c8e1-4d6c-be4a-f81724da9394)
![image](https://github.com/user-attachments/assets/3f2af939-5f56-485c-8471-b944addc8c16)

Видим, что все задачи отработали без ошибок
