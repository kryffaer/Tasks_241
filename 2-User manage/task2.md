
# Запрещаем

1. Запретите пользователю user1 из предыдщуего задания выполнять вход в систему<br />
![alt text](https://github.com/kryffaer/Tasks_241/blob/my_reply/2-User%20manage/screenshots/9.png?raw=true)<br />
2. Как вы это сделали?<br />
![alt text](https://github.com/kryffaer/Tasks_241/blob/my_reply/2-User%20manage/screenshots/10.png?raw=true)<br />
3. Какие ещё способы это сделать вы знаете?
* Метод 1: Создание файла /etc/nologin
```sh
sudo touch /etc/nologin
```
* Метод 2: Изменение shell пользователя
```sh
sudo usermod -s /sbin/nologin username
```
* Метод 3: Блокировка учетной записи с помощью passwd
```sh
sudo passwd -l username
```
Чтобы разблокировать учетную запись, использовать ключ -u:
```sh
sudo passwd -u username
```
4. Можно ли создать пользователей с одинаковыми username?<br />
Файл /etc/passwd хранит уникальные записи username у пользователей, это ограничение встроено в инструменты useradd и adduser. Поэтому создавать пользователей с одинаковым username нельзя.
