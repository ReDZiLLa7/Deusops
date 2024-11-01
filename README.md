# Deusops

## 1. Установка Ansible

Я пользуюсь ОС Windows, поэтому мне понадобилось установить WSL 2, чтобы скачать Ansible.

Это можно сделать с помощью команды:

```bash
wsl --install -d Ubuntu-20.04
```
Также потребовалость установить дистрибутив по умолчанию, которым является только что скаченная Ubuntu 20.04 LTS

```bash
wsl --set-default Ubuntu-20.04
```

На данном скриншоте видно, что стоит именно Ubuntu-20.04, а также WSL версии 2

![image](https://github.com/user-attachments/assets/68ca1197-e3ef-4585-8f9f-1b43e9107ef4)

После этих шагов установил сам Ansible, используя команды для Ubuntu:

```bash
sudo apt update
sudo apt install ansible
```

Установка прошла успешно, проверим версию командой:

```bash
ansible --version
```

![image](https://github.com/user-attachments/assets/79104b35-41e6-455d-b3f2-b6a17d87941d)

## 2. Установка Vagrant

На Windows установка Vagrant происходит обычным путём - скачиванием установочного файла с официального сайта 

https://developer.hashicorp.com/vagrant/install

![image](https://github.com/user-attachments/assets/7ed8f625-ae18-4185-a989-be466825de00)

Перед дальнейшей преднастройкой Vagrant, нужно иметь у себя на компьютере VirtualBox версии именно 7.0 или ниже, так как на самой новой версии он не работает

Не лишним будет установка VirtualBox Extension Pack для установленной версии VirtualBox

Вернемся к Vagrant, создадим новую папку для нашего проекта, у меня она будет находится по данному пути:

C:\Itmo\deusops-itmo

Теперь в этой же дирректории проинициализируем Vagrant командой:

```bash
vagrant init
```

Даное действие создаст Vagrantfile, а также папку .vagrant.d, в которой в папку boxes, мы поместим образ ОС, которая в будущем будет стоять на наших nodes

![image](https://github.com/user-attachments/assets/05c3094f-5fe7-4815-8d8c-81637174f2b7)

Теперь откроем только что созданный Vagrantfile через любой текстовый редактор, я буду использовать Sublime Text, и напишем в нем данный скрипт:

![image](https://github.com/user-attachments/assets/f20e1910-45d6-41a8-a4a1-c10ea674486c)

## 3. После всех этих действий, мы наконец можем поднять все наши сервера командой:

```bash
vagrant up
```

Для каждого сервера увидим вот такой результат:

![image](https://github.com/user-attachments/assets/3719fac2-c69d-44da-97db-4dd31c9592ab)

![image](https://github.com/user-attachments/assets/da214746-9b93-43eb-a55c-cf463b7834e9)

Попробуем подключиться к одному из серверов:

![image](https://github.com/user-attachments/assets/85030bcd-a418-49a5-82c1-dfd8ca6f46f2)

## Успешно!

## 4. Написание inventory-файла для развернутых хостов

Создадим в домашней дирректории inventory-файл:

![image](https://github.com/user-attachments/assets/5d63a7b7-4f73-471e-9886-540f3c89fcae)

## 5. Написание playbook для установки Docker

Создадим в домашней дирректории новый playbook:

![image](https://github.com/user-attachments/assets/a902bebd-0f6b-4221-b21b-e9b40fdbd150)
![image](https://github.com/user-attachments/assets/936a1550-2543-418c-a301-c591d73f676b)

## 6. Запустим приложение на нодах группы [app] используя ansible

![image](https://github.com/user-attachments/assets/043797ab-2c5f-4213-9667-2074f9360935)
![image](https://github.com/user-attachments/assets/6684c821-2359-4850-a6ff-468fab1b24d4)

Проверим работу нашего приложение, зайдя на один из серверов и прописав команду:

```bash
lynx http://localhost:8000
```
Примим Coockie файлы:

![image](https://github.com/user-attachments/assets/2f71546c-c372-4bf6-b14e-bf1e693d57b2)
![image](https://github.com/user-attachments/assets/66066b90-a599-40ec-b719-c05159ab50cb)
![image](https://github.com/user-attachments/assets/dc012719-54f2-44f8-8d46-95e9cfd98b04)

В конечном итоге увидим работающее приложение Django:

![image](https://github.com/user-attachments/assets/5d49e5dd-7b43-440b-be70-d8e0e03adf2a)
