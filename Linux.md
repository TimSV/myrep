# Домашнее задание к лекции 3 LUNUX:

## Задание 1
Создайте пользователя docker и группу docker. Создайте папку /mnt/docker и назначьте пользователя docker её владельцем.

```bash
# Создаем пользователя docker
 sudo useradd -m docker
 
 # Смотрим результат
 cat /etc/passwd | grep docker
docker:x:1001:1001::/home/docker:/bin/sh

# При создании пользователя создалась одноименная группа
cat /etc/group | grep docker
docker:x:1001:

# Создаем папку docker
sudo mkdir /mnt/docker

# Меняем права на папку
sudo chown docker /mnt/docker/

# Проверяем так ли это
ls -l  /mnt/
total 4
drwxr-xr-x 2 docker root 4096 May 22 18:20 docker
```
## Задание 2
Создайте в домашней директории файл table и внесите в него список слов (по одному слову в строке): speak, loyal, famous, absorb, ice, skill, galaxy, about, offer, topple, argue, unusual, sing, evoke. Используя awk, выведите все слова, содержащие букву o, и номер строки, где они находятся.

```bash
# Создаем нужный файл
echo -e "speak\nloyal\nfamous\nabsorb\nice\nskill\ngalaxy\nabout\noffer\ntopple\nargue\nunusual\nsing\nevoke" > ~/table

# Используем awk для вывода
awk '/o/ {print NR, $0}' ~/table
2 loyal
3 famous
4 absorb
8 about
9 offer
10 topple
14 evoke
```
## Задание 3
Создайте пользователя test и задайте ему пароль из 16 символов, используя подсказки из pwgen --help. Добавьте пользователя в группу с таким же именем. Затем, войдите под пользователем test и удалите файл table от его имени.

```bash
# Создаем пользователя test
 sudo useradd -m test

# Генерируем пароль 
pwgen -sny 16 1

# Меняем пароль пользователю
sudo passwd test
New password:
Retype new password:
passwd: password updated successfully

# Добавляем пользователя в одноименную группу
sudo usermod -aG test test
cat /etc/passwd | grep test
test:x:1002:1002::/home/test:/bin/sh

# Предварительно меняем права доступа на домашний каталог, чтобы
# другие пользователи могли менять изменять файлы
chmod -R 777 /home/ubuntu/

# Логинимся под пользователем test
su test
Password:

# Удаляем требуемый файл
$ rm /home/ubuntu/table

# Выходим и меняем права обратно
exit
chmod -R 750 /home/ubuntu/
```
