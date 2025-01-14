
# Открываем iptables

1. Установите iptables<br />
```sh
apt-get install iptables
```
2. Проверьте осталась ли возможность подключения по ssh к вашему серверу<br />
```sh
ssh username@server_ip
```
3. Почему может пропасть такая возможность?<br />
Если заблокирован порт 22<br />
4. Откройте нужный порт на сервере чтобы восстановить подключение<br />
```sh
iptables -A INPUT -p tcp --dport 22 -j ACCEPT
```
5. Это будет udp или tcp прот?<br />
ssh использует TCP, протокол с установленным соединением.<br />

# Сохраняем

6. Сохраняются ли записанные вами правила после перезагрузки?<br />
iptables не сохраняет правила автоматически после перезагрузки, нужно сохранять<br />
7. Как их сохранить?<br /><br />
```sh
sudo iptables-save -f /etc/sysconfig/iptables
```
![alt text](https://github.com/kryffaer/Tasks_241/blob/my_reply/9-Firewall/screenshots/1.png?raw=true)<br />

При работе с firewall не рекомендую отключаться от текущей сессии ssh. Лучше подключаться из другой консольки.
