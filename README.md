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

Для этого зайдем в папку roles/docker/tasks/ и добавим в файл main.yml часть нашего старого playbook:

![image](https://github.com/user-attachments/assets/090148ff-faa2-4c45-af10-9e74799f48d2)

## 3. Параметризация роли через переменные

Далее зайдем в папку roles/docker/defaults/ и вынесем в файл main.yml переменные, которые в дальнейшем можно будет использовать внутри playbook:

![image](https://github.com/user-attachments/assets/cf0de042-0338-4cd5-b7e1-faa184fd5eed)

Также заменим эти переменные внутри файла main.yml в директории roles/docker/tasks/:

![image](https://github.com/user-attachments/assets/f222721f-3d4f-4cd9-b02d-ef22ccc9047d)

## 4. Создание нового репозитория и push роли "Docker" на него:

![image](https://github.com/user-attachments/assets/0c69d450-c03e-4e13-9310-d63d3d6682f7)

Нам также нужно поменять основной playbook, в домашней директории, deploy.yml, добавив туда роль "docker", а также оставив только нужные tasks:

![image](https://github.com/user-attachments/assets/e01f5c73-914d-4ba9-b230-17b45405aafa)

## 5. Создание файла requirements.yml для установки роли Docker из репозитория

Создаем файл в домашней директории и вносим туда данные с нашего удаленного репозитория:

![image](https://github.com/user-attachments/assets/c53b91d8-91c6-42aa-963c-c85bfca9a964)

## 6. Запуск приложения на нодах группы [app] с использованием ansible-playbook и роли “docker”

![image](https://github.com/user-attachments/assets/75899417-e992-4899-ad59-72859b79b39f)
![image](https://github.com/user-attachments/assets/63cf294a-1fc3-4627-bce8-7c9e8de567a9)

Видим, что все задачи отработали без ошибок

Проверим работу docker:
```bash
systemctl status docker
```

![image](https://github.com/user-attachments/assets/ddd8c573-60e2-406e-980c-a8afe0741941)

Проверим загруженные образы:
```bash
docker images
```

![image](https://github.com/user-attachments/assets/753ac472-391b-435b-8ba2-f959fac7e8af)

Проверим список запущенных контейнеров:
```bash
docker ps
```

![image](https://github.com/user-attachments/assets/3e0c39f2-1749-4d2b-867a-3b3cda158d30)

И проверим работу django приложения:
```bash
curl -I http://localhost:8000/catalog/
```

![image](https://github.com/user-attachments/assets/5f4177c5-d722-45f4-9351-57dd73886806)

Видим ответ:

```
HTTP/1.1 200 OK
```
