
# Шарим


1. Установите пакет samba<br />
![alt text](https://github.com/kryffaer/Tasks_241/blob/my_reply/8-Samba/screenshots/1.png?raw=true)<br />
2. Что такое общая папка, зачем оно может быть нужно?<br />
Общая папка — директория, доступная для нескольких пользователей или устройств в сети. Нужна для обмена файлами между различными системами<br /> 
3. Создайте общую папку без пароля с правами только на чтение файлов<br />
* Создадим директории<br />
![alt text](https://github.com/kryffaer/Tasks_241/blob/my_reply/8-Samba/screenshots/2.png?raw=true)<br />
* Настроим прав доступа<br />
![alt text](https://github.com/kryffaer/Tasks_241/blob/my_reply/8-Samba/screenshots/3.png?raw=true)<br />
* Настроим файл конфигурации Samba<br />
* Откроем файл конфигурации Samba:<br />
![alt text](https://github.com/kryffaer/Tasks_241/blob/my_reply/8-Samba/screenshots/4.png?raw=true)<br />
* Добавим следующую секцию в конец файла:<br />
![alt text](https://github.com/kryffaer/Tasks_241/blob/my_reply/8-Samba/screenshots/5.png?raw=true)<br />
* Перезапустим службы Samba
```sh
sudo systemctl restart smbd
```
4. Создайте общую папку с паролем с правами на чтение и запись<br />
* Создадим директории
```sh
sudo mkdir /media/samba/private
```
* Настроим прав доступа
```sh
sudo chmod -R 0770 /media/samba/private
sudo chown -R username:groupname /media/samba/private
```
* Создим пользователя Samba
```sh
sudo smbpasswd -a username
```
* Настроим файл конфигурации Samba<br />
* Откроем файл конфигурации Samba:
```sh
sudo nano /etc/samba/smb.conf
```
* Добавим следующую секцию в конец файла:<br />
![alt text](https://github.com/kryffaer/Tasks_241/blob/my_reply/8-Samba/screenshots/8.png?raw=true)<br />
* Перезапустим службы Samba
```sh
sudo systemctl restart smbd
```
5. Создайте общую папку с доступом для какой-то группы с полными правами<br />
* Создадим директории
```sh
sudo mkdir /media/samba/group_share
```
* Настроим прав доступа
```sh
sudo chmod -R 0770 /media/samba/group_share
sudo chown -R groupname:groupname /media/samba/group_share
```
* Настроим файл конфигурации Samba<br />
* Откроем файл конфигурации Samba:
```sh
sudo nano /etc/samba/smb.conf
```
* Добавим следующую секцию в конец файла:<br />
![alt text](https://github.com/kryffaer/Tasks_241/blob/my_reply/8-Samba/screenshots/10.png?raw=true)<br />
* Перезапустим службы Samba
```sh
sudo systemctl restart smbd
```
6. Создайте общую папку в которой у одной группы будет полный доступ, а у другой только доступ на чтение.<br />
Третья группа не должна иметь к ней доступа
* Создадим директории
```sh
sudo mkdir /media/samba/multi_group_share
```
* Настроим права доступа
```sh
sudo chmod -R 0770 /media/samba/multi_group_share
sudo chown -R full_access_group:full_access_group /media/samba/multi_group_share
```
* Настроим файл конфигурации Samba<br />
* Откроем файл конфигурации Samba:
```sh
sudo nano /etc/samba/smb.conf
```
* Добавим следующую секцию в конец файла:<br />
![alt text](https://github.com/kryffaer/Tasks_241/blob/my_reply/8-Samba/screenshots/12.png?raw=true)<br />
* Перезапустим службы Samba
```sh
sudo systemctl restart smbd
```
Результат изменения прав доступа:<br />
![alt text](https://github.com/kryffaer/Tasks_241/blob/my_reply/8-Samba/screenshots/13.png?raw=true)<br />

![alt text](https://github.com/kryffaer/Tasks_241/blob/my_reply/8-Samba/screenshots/final.jpg?raw=true)<br />
