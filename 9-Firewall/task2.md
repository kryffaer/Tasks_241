# Открываем firewald

1. Удалите iptables и установите firewalld<br />
```sh
apt-get remove iptables -y && apt-get install firewalld -y
```
2. Попробуйте так-же проверить возможность подключения по ssh<br />
Мы можем подключаться по ssh, firewalld отключен<br />
3. Если её нет то откройте порт<br />
```sh
firewall-cmd --add-port=22/tcp --permanent
```
4. Выведите список открытых портов с помощью firewall-cmd<br />
```sh
firewall-cmd --list-all
```
![alt text](https://github.com/kryffaer/Tasks_241/blob/my_reply/9-Firewall/screenshots/2.png?raw=true)<br />
5. Можно ли там добавить порты по названию сервиса?<br />
```sh
firewall-cmd --add-service=ssh --permanent
firewall-cmd --reload
```
6. На вашей Локальной виртуальной машине попробуйте подключиться к серверу samba из предыдущих заданий<br />
![alt text](https://github.com/kryffaer/Tasks_241/blob/my_reply/9-Firewall/screenshots/3.png?raw=true)<br />
7. Если не получилось то откройте нужные порты<br />
```sh
firewall-cmd --add-port=139/tcp --permanent
firewall-cmd --add-port=445/tcp --permanent
```
8. Сделайте так чтобы изменения были постоянными<br />
```sh
systemctl restart firewalld
```
