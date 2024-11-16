# Deusops

## 1. Поднимем Vagrant-окружение при помощи Vagrantfile, используя команду:

```
vagrant up
```

![image](https://github.com/user-attachments/assets/d7d51e00-c688-4faa-a7fe-f29388d62da9)

## 2. Добавим новую роль nginx, запушим в репозиторий и добавим в requirements.yml ссылку на созданный репозиторий

Создадим роль nginx с помощью команды:

```
ansible-galaxy init nginx
```

![image](https://github.com/user-attachments/assets/02db37b4-049d-41d4-bd02-575cab5eb182)

Создадим новый репозиторий для nginx и запушим туда только что инициализированную роль:

![image](https://github.com/user-attachments/assets/0b8ef6a4-989f-488f-ae2c-2355b6dd5672)

Добавим в requirements.yml ссылку на созданный репозиторий:

![image](https://github.com/user-attachments/assets/4ee77b6e-2c01-48e8-b8a3-b0bc5f6630c6)

## 3-4. Подготовим шаблон конфигурационного файла для Nginx, с настройками для отдачи статических файлов, а также учтём в шаблоне проксирование динамики в контейнер с Django

![image](https://github.com/user-attachments/assets/e790de49-cf02-45b3-9387-8fd6554ab2e7)

## 5. Напишем плейбук установки через роли nginx на хосты группы web, и docker на хосты группы app

![image](https://github.com/user-attachments/assets/de0a67cc-eeb8-407a-8ac1-7ffaa9b237fd)

Запустим playbook с указанием группы хостов web:

![image](https://github.com/user-attachments/assets/95a0478d-e9f9-4192-8465-fe543083badd)

Проверим состояние службы nginx на нашем сервере
```
systemctl status nginx
```

![image](https://github.com/user-attachments/assets/f2525ef6-78b4-4668-bbf7-bbe004843135)

Также проверим работу nginx:
```
curl -I http://localhost:80/catalog/
```

![image](https://github.com/user-attachments/assets/c6101b7c-0bf0-492d-a763-bb225bcd1245)

Можем увидеть, что nginx успешно обработал наш запрос

