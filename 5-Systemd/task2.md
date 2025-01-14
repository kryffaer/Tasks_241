# Пишем юниты

1. Создайте скрипт который создаёт папку заполняет её файлами ( имена 1-4 ) и записывает в них информацию
о текущей дате, версии ядра, имени компьютера и списе всех файлов в домашнем каталоге пользователя от которого выполняется скрипт( не забудьте сдлеать проверку на существование файлов и папок)<br />
```sh
#!/bin/bash
set -euo pipefail
M_DIR="$HOME/folder"

if [ ! -d "$M_DIR" ]; then
    mkdir "$M_DIR"
    echo "Папка создана!"
else
    echo "Папка найдена |\/|"
fi

for i in {1..4}; do
    if [ ! -f "$M_DIR/$i" ]; then
        touch $M_DIR/$i
        echo "Файл $i создан!"
        if [ "$i" == 1 ]; then
             date > $M_DIR/1
        elif [ "$i" == 2 ]; then
             cat /proc/version > $M_DIR/2
        elif [ "$i" == 3 ]; then
             hostname > $M_DIR/3
        else
             ls -la > $M_DIR/4
    fi
    else
        echo "Файл $i обнаружен |\/|"
fi
done 
```
2. Создайте юнит который будет вызывать этот скрипт при запуске. Проверьте<br />
```sh
[Unit]
Description = This is a test unit!
After=network.target

[Service]
ExecStart=/home/systemd-script
User=ananas
Group=ananas
Type=oneshot
WorkingDirectory=/home/ananas

[Install]
WantedBy=multi-user.target
```
3. Создайте таймер который будет вызывать выполнение одноимённого systemd юнита каждые 5 минут.<br />
```sh
[Unit]
Description=Таймер для периодического запуска myunit.service
Requires=myunit.service

[Timer]
Unit=myunit.service
OnUnitActiveSec=5m

[Install]
WantedBy=timers.target
```
4. От какого пользователя вызыаются юниты поумолчанию?<br />
По умолчанию юниты systemd вызываются от Root (можно указать, от кого надо вызывать).<br />
5. Создайте пользователя от имени которого будет выполняться ваш скрипт.<br />
```sh
sudo useradd testuser
```
6. Дополните юнит информацией о пользователе от которого должен выплняться скрипт.<br />
```sh
[Unit]
Description=My Script
[Service]
User=testuser
ExecStart=/path/to/your/script.sh
[Install]
WantedBy=multi-user.target
```
7. Дополните ваш скрипт так, что бы он независимо от местоположения всега выполнялся в домашней папке того кто его вызывает.<br />
```sh
#!/bin/bash
cd $HOME
echo "Выполняем скрипт в директории $HOME"
```
