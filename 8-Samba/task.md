
# Шарим


1. Установите пакет samba
```sh
apt-get install samba
```
2. Что такое общая папка, зачем оно может быть нужно?<br />
Общая папка — директория, доступная для нескольких пользователей или устройств в сети. Нужна для обмена файлами между различными системами<br /> 
3. Создайте общую папку без пароля с правами только на чтение файлов<br />
* Создадим директории
```sh
sudo mkdir /media/samba/public
```
* Настроим прав доступа
```sh
sudo chmod -R 0755 /media/samba/public
sudo chown -R nobody:nogroup /media/samba/public
```
* Настроим файл конфигурации Samba<br />
* Откроем файл конфигурации Samba:
```sh
sudo nano /etc/samba/smb.conf
```
* Добавим следующую секцию в конец файла:
```sh
[public]
  path = /media/samba/public
  browseable = yes
  writable = no
  guest ok = yes
  read only = yes
```
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
* Добавим следующую секцию в конец файла:
```sh
[private]
  path = /media/samba/private
  browseable = yes
  writable = yes
  guest ok = no
  valid users = username
```
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
* Добавим следующую секцию в конец файла:
```sh
[group_share]
  path = /media/samba/group_share
  browseable = yes
  writable = yes
  guest ok = no
  valid users = @groupname
```
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
* Добавим следующую секцию в конец файла:
```sh
[multi_group_share]
  path = /media/samba/multi_group_share
  browseable = yes
  writable = yes
  guest ok = no
  valid users = @full_access_group @read_only_group
  read list = @read_only_group
  write list = @full_access_group
```
* Перезапустим службы Samba
```sh
sudo systemctl restart smbd
```
