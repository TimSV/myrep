## Git
Git - это распределенная система контроля версий.

VCS - Version Control System - система контроля версий.
Отслеживает изменения, записывает историю изменений, возвращаться к предыдущим состояниям, сравнивать версии и многое другое.

В гит каждый разработчик имеет полную копию репозитория на своем локальном ПК.
Гит хранит данные в виде набора снимков миниатюрной файловой системы - при коммите система запоминает как выглядит каждый файл в этот момент и сохраняет ссылку на этот снимок.

Гит сохраняет все объекты в свою базу данных не по имени, а по хэш-сумме содержимого объекта.

## Настройка Git
Посмотреть версию git:
```bash
git -version
```

**git config** - утилита позволяет просматривать и настраивать параметры гита.
Эти параметры могут быть сохранены в трех местах:
1. В системе /etc/gitconfig (--system) - общий для всех пользователей системы и для всех репозиториев. Имеет низший приоритет. По умолчанию файл может отсутствовать.

2. У пользователя ~/.gitconfig или ~/.gitconfig/git/config  (--global) - настройки конкретного пользователя. Следующий по приоритету.

3.  В самом каталоге репозитории (--local) - настройки конкретного репозитория. Высший приоритет.
Посмотреть все установленные настройки и откуда они прочитаны:
```bash
git config --list --show-origin
```

После установки гита его нужно настроить под себя:

**Указать имя пользователя**
```bash
git config --global user.name <username>
```

**Указать почту**
```bash
git config --global user.email <email>
```

**Выбор текстового редактора**
```bash
git config --global core.editor nano
```

>💡 **Совет**  
 Чтобы указать эти данные локально, нужно перейти в каталог с репозиторием и написать эти же команды без параметра --global

> 💡 **Факт**
> По умолчанию гит использует стандартный редактор системы (vim)

Проверить настройки
```bash
git config --list
```

```bash
git config <key>
```
---
## Начало работы с Git
Создать каталог под репозитория и в нем набрать команду инициализации:
```bash
git init
```

В каталоге появится скрытая папка .git в которой хранится вся информация о репозитории.

**Репозиторий** - это основное хранилище проекта и всей его истории изменений.
Существует два типа репозиториев:
1. **Локальный** - Расположен на ПК
2. **Удаленный** - Расположен на серверах Githab, Gitlab, Bitbacket
