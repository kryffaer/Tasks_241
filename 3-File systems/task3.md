# Продолжаем

1. Выведите содержимое fstab. Что хранится в fstab?<br />
В fstab хранится информация о том, что и куда нужно монтировать. Каждая строчка в файле описывает раздел, который нужно примонтировать к определенной точке.<br />
* Устройство монтируемой файловой системы: имя устройства, метка устройства или UUID устройства 
* Точка монтирования - путь, по которому будет смонтировано устройство. 
* Тип файловой системы 
* Параметры монтирования - опции, определяющие, как файловая система будет смонтирована. 
* Флаг, указывающий, должна ли утилита dump создавать резервные копии этой файловой системы.
* Порядок, в котором файловая система будет проверена программой fsck при загрузке системы. <br />
![alt text](https://github.com/kryffaer/Tasks_241/blob/my_reply/3-File%20systems/screenshots/5.png?raw=true)<br />
2. Добавьте в виртуальную машину ещё один диск<br />
* Заходим в настройки виртуальной машины
* Добавляем новый виртуальный диск
* Перезагружаем виртуальную машину<br />
![alt text](https://github.com/kryffaer/Tasks_241/blob/my_reply/3-File%20systems/screenshots/6.png?raw=true)<br />
3. Узнайте как ситема видит ваш диск - выведите информацию о блочных устройствах<br />
![alt text](https://github.com/kryffaer/Tasks_241/blob/my_reply/3-File%20systems/screenshots/7.png?raw=true)<br />
4. С помощью полученной информации создайте на диске таблицу разделов и фаловую систему ext4<br />
![alt text](https://github.com/kryffaer/Tasks_241/blob/my_reply/3-File%20systems/screenshots/8.png?raw=true)<br />
![alt text](https://github.com/kryffaer/Tasks_241/blob/my_reply/3-File%20systems/screenshots/9.jpg?raw=true)<br />
5. Примонитруте диск в каталог /mnt<br />
![alt text](https://github.com/kryffaer/Tasks_241/blob/my_reply/3-File%20systems/screenshots/9.png?raw=true)<br />
6. Зайдите в каталог и создайте там файлы<br />
![alt text](https://github.com/kryffaer/Tasks_241/blob/my_reply/3-File%20systems/screenshots/10.png?raw=true)<br />
7. Отмонтируйте диск и проверье остались ли файлы<br />
![alt text](https://github.com/kryffaer/Tasks_241/blob/my_reply/3-File%20systems/screenshots/11.jpg?raw=true)<br />
8. Сделайте так чтобы диск автоматически подключался при загрузке систем ( добавьте информацию о нём с fstab)<br />
Получаем UUID диска:<br />
```sh
blkid /dev/sdb2
```
Редактируем файл /etc/fstab:<br />
```sh
UUID=[uuid] /mnt ext4 defaults 0 2
```
9. Проверьте корретность записанных в fstab данных перед перезагрузкой<br />
```sh
mount -a
```
10. Перезагрущите систему и убедитесь что диск был подключён к системе<br />
```sh
reboot now
lsblk
```
