## 1.  Создайте локальный Git-репозиторий.

```
ubuntu@dm-c2-9-53-14:~$ mkdir myrep
ubuntu@dm-c2-9-53-14:~$ cd myrep/
ubuntu@dm-c2-9-53-14:~/myrep$ git init
Initialized empty Git repository in /home/ubuntu/myrep/.git/
```

## 2.Настройте имя пользователя и email для текущего репозитория.

```
ubuntu@dm-c2-9-53-14:~/myrep$ git config user.name 'Timofeev Sergey'
ubuntu@dm-c2-9-53-14:~/myrep$ git config user.email serge152@mail.ru

ubuntu@dm-c2-9-53-14:~/myrep$ git config --list --show-origin
file:/home/ubuntu/.gitconfig    user.email=s_timofeev@lesta.group
file:/home/ubuntu/.gitconfig    user.name=Sergey Timofeev
file:/home/ubuntu/.gitconfig    core.editor=nano
file:.git/config        core.repositoryformatversion=0
file:.git/config        core.filemode=true
file:.git/config        core.bare=false
file:.git/config        core.logallrefupdates=true
file:.git/config        user.name=Timofeev Sergey
file:.git/config        user.email=serge152@mail.ru
```

## 3. Создайте структуру проекта с несколькими директориями.
```
ubuntu@dm-c2-9-53-14:~/myrep$ mkdir -p  MT/tanks MT/maps MK/ships MK/maps
```

## 4. Добавьте не менее трёх файлов в разные каталоги.
```
ubuntu@dm-c2-9-53-14:~/myrep$ touch ./MT/tanks/IS7.txt ./MT/maps/Prokhorovka.txt \
> ./MK/ships/Avrora.txt ./MK/maps/Ocean.txt
ubuntu@dm-c2-9-53-14:~/myrep$ touch Git_theory.md  README.md

ubuntu@dm-c2-9-53-14:~/myrep$ ls -R
.:
Git_theory.md  MK  MT  README.md

./MK:
maps  ships

./MK/maps:
Ocean.txt

./MK/ships:
Avrora.txt

./MT:
maps  tanks

./MT/maps:
Prokhorovka.txt

./MT/tanks:
IS7.txt
```

## 5. Настройте .gitignore, исключив один из подкаталогов от отслеживания.
```
ubuntu@dm-c2-9-53-14:~/myrep$ echo '/MK/maps' > .gitignore
ubuntu@dm-c2-9-53-14:~/myrep$ git add .
ubuntu@dm-c2-9-53-14:~/myrep$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   .gitignore
        new file:   Git_theory.md
        new file:   MK/ships/Avrora.txt
        new file:   MT/maps/Prokhorovka.txt
        new file:   MT/tanks/IS7.txt
        new file:   README.md
```

## 6. Создайте две ветки от main: feature/api и feature/ui.

```
ubuntu@dm-c2-9-53-14:~/myrep$ git commit -m "Initial commit"
ubuntu@dm-c2-9-53-14:~/myrep$ git branch feature/api
ubuntu@dm-c2-9-53-14:~/myrep$ git branch feature/ui
ubuntu@dm-c2-9-53-14:~/myrep$ git branch -a
  feature/api
  feature/ui
* master
```

## 7. В каждой ветке внесите независимые изменения.
Сделайте как минимум по 2 коммита в каждой ветке с осмысленными сообщениями.

```
ubuntu@dm-c2-9-53-14:~/myrep$ git switch feature/api
ubuntu@dm-c2-9-53-14:~/myrep$ echo 'please read me' > README.md
ubuntu@dm-c2-9-53-14:~/myrep$ git add .
ubuntu@dm-c2-9-53-14:~/myrep$ git commit -m 'chage README.md file'

ubuntu@dm-c2-9-53-14:~/myrep$ nano Git_theory.md
<some text>
ubuntu@dm-c2-9-53-14:~/myrep$ git add .
ubuntu@dm-c2-9-53-14:~/myrep$ git commit -m 'change Git_theory.md file'

ubuntu@dm-c2-9-53-14:~/myrep$ git switch feature/ui
ubuntu@dm-c2-9-53-14:~/myrep$ echo -e 'Name - IS7\nHP - 2500\nSpeed - 65\nDamage - 650' > ./MT/tanks/IS7.txt
ubuntu@dm-c2-9-53-14:~/myrep$ git add .
ubuntu@dm-c2-9-53-14:~/myrep$ git commit -m 'change IS7.txt file'

ubuntu@dm-c2-9-53-14:~/myrep$ echo -e 'Name - Avrora\nHP - 25000\nSpeed - 19\nDamage - 2700' > ./MK/ships/Avrora.txt
ubuntu@dm-c2-9-53-14:~/myrep$ git add .
ubuntu@dm-c2-9-53-14:~/myrep$ git commit -m 'change Avrora.txt file'
```

## 8. Выполните слияние ветки feature/api в main с использованием --no-ff.

```
ubuntu@dm-c2-9-53-14:~/myrep$ git switch master
ubuntu@dm-c2-9-53-14:~/myrep$ git merge --no-ff -m 'merge changes' feature/api
```

## 9. Зафиксируйте изменения.

```
ubuntu@dm-c2-9-53-14:~/myrep$ cat ./README.md
please read me
```

## 10.Убедитесь, что история коммитов отображает ветвление.

```
ubuntu@dm-c2-9-53-14:~/myrep$ git log --graph --oneline --decorate --all
*   854a6d0 (HEAD -> master) Merge branch 'feature/api'
|\
| * 69755bb (feature/api) change Git_theory.md file
| * 045f82a chage README.md file
|/
| * 8f822c9 (feature/ui) change Avrora.txt file
| * 4b8e25f change IS7.txt file
|/
* 860c5f5 Initial commit
```
## 11. Выполните ребейз ветки feature/ui относительно main.
```
ubuntu@dm-c2-9-53-14:~/myrep$ git switch feature/ui
ubuntu@dm-c2-9-53-14:~/myrep$ git rebase master
```
## 12. Разрешите возможные конфликты.

```
Successfully rebased and updated refs/heads/feature/ui.
```

## 13. Зафиксируйте изменения.
```
ubuntu@dm-c2-9-53-14:~/myrep$ git log --graph --oneline --decorate --all
* 05e29e8 (HEAD -> feature/ui) change Avrora.txt file
* 0cd437a change IS7.txt file
*   854a6d0 (master) Merge branch 'feature/api'
|\
| * 69755bb (feature/api) change Git_theory.md file
| * 045f82a chage README.md file
|/
* 860c5f5 Initial commit
```
## 14. Создайте тег v1.0.0 на коммите, в котором объединены все изменения.

```
ubuntu@dm-c2-9-53-14:~/myrep$ git tag -a v1.0.0 05e29e8 -m 'Release'
```
## 15. Подпишите тег с сообщением.
```
ubuntu@dm-c2-9-53-14:~/myrep$ git tag -s v1.0.0 -m "Подписанный релиз" 05e29e8
```

## 16. Имитируйте ошибочный коммит в любой из веток.
```
ubuntu@dm-c2-9-53-14:~/myrep$ echo 'wrong code' >> README.md
ubuntu@dm-c2-9-53-14:~/myrep$ git add .
ubuntu@dm-c2-9-53-14:~/myrep$ git commit -m 'commit wrong code'
```

## 17. Отмените его с помощью git revert, а затем — другим способом с использованием git reset.
```
ubuntu@dm-c2-9-53-14:~/myrep$ git log --oneline
d64af25 (HEAD -> master) commit wrong code
05e29e8 (tag: v1.0.0, tag: show, feature/ui, feature/api) change Avrora.txt file
0cd437a change IS7.txt file
854a6d0 Merge branch 'feature/api'
69755bb change Git_theory.md file
045f82a chage README.md file
860c5f5 Initial commit

ubuntu@dm-c2-9-53-14:~/myrep$ git revert d64af25
[master 11ffaef] Revert "commit wrong code"
 1 file changed, 1 deletion(-)

ubuntu@dm-c2-9-53-14:~/myrep$ echo 'wrong code' >> README.md
ubuntu@dm-c2-9-53-14:~/myrep$ git add .
ubuntu@dm-c2-9-53-14:~/myrep$ git commit -m 'commit wrong code'

ubuntu@dm-c2-9-53-14:~/myrep$ git log --oneline
34b046c (HEAD -> feature/api, master, feature/ui) commit wrong code
11ffaef Revert "commit wrong code"
d64af25 commit wrong code
05e29e8 (tag: v1.0.0, tag: show) change Avrora.txt file
0cd437a change IS7.txt file
854a6d0 Merge branch 'feature/api'
69755bb change Git_theory.md file
045f82a chage README.md file
860c5f5 Initial commit

ubuntu@dm-c2-9-53-14:~/myrep$ git reset --hard 11ffaef
HEAD is now at 11ffaef Revert "commit wrong code"
```

## 18. Смоделируйте ситуацию с временными изменениями.
```
ubuntu@dm-c2-9-53-14:~/myrep$ echo 'new code' >> README.md
```
## 19. Используйте git stash для сохранения незакоммиченных изменений.
```
ubuntu@dm-c2-9-53-14:~/myrep$ git stash
```

## 20. Затем восстановите их и продолжите работу.
```
ubuntu@dm-c2-9-53-14:~/myrep$ git stash pop
```
