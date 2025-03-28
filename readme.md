# README по git

----

# Инструкция и порядок работы с Git

**Настройка** – Указываем имя и email, чтобы Git знал, кто делает коммиты.  
**Создание репозитория** – Инициализируем новый репозиторий или клонируем существующий.  
**Добавление изменений** – Проверяем статус, добавляем файлы в отслеживание и фиксируем изменения коммитом.  
**Работа с ветками** – Создаем новые ветки, переключаемся между ними, объединяем изменения.  
**Отмена изменений** – Можно откатить файл к предыдущему состоянию, отменить коммит или убрать изменения.  
**Синхронизация с удаленным репозиторием** – Загружаем (push) и получаем (pull) изменения с сервера.  
**Просмотр истории** – Можно видеть список коммитов, кто и что изменил.  
**Сохранение незавершенных изменений** – Если нужно переключиться на другую задачу, можно временно сохранить изменения (stash).  
**Дополнительные возможности** – Используем rebase для чистой истории, cherry-pick для выборочного переноса коммитов, теги для важных версий.  

----

# Список команд

## Настройка Git

1. Указание имени и email

```
git config --global user.name "Ваше Имя"
git config --global user.email "your.email@example.com"
```

2. Просмотр текущих настроек

```
git config --list
```

3. Изменение имени и email для конкретного репозитория

```
git config user.name "Другое Имя"
git config user.email "another.email@example.com"
```

## Создание/клонирование репозитория

```
git init                      # Создать новый репозиторий  
git clone <URL>               # Клонировать удаленный репозиторий  
```

## Связать локальный и удаленный репозиторий

Перейдите на страницу удалённого репозитория, выберите тип SSH и скопируйте URL.  
Откройте консоль, перейдите в каталог локального репозитория и введите команду

```
git remote add
git remote add origin git@github.com:%ИМЯ_АККАУНТА%/first-project.git
```
Убедиться, что репозитории связаны -  

```
git remote -v
```

## Настройка окружения

```
git config --global user.name "Ваше Имя"  
git config --global user.email "your.email@example.com"  
git config --list  # Проверить настройки  
```

## Работа с файлами

```
git status                    # Проверить состояние репозитория
git add <file>                # Добавить файл в индекс
git add .                     # Добавить все файлы
git commit -m "Описание коммита"  # Зафиксировать изменения
git commit --amend            # Изменить последний коммит
```

## Работа с удаленными репозиториями

```
git remote add origin <URL>    # Добавить удаленный репозиторий  
git remote -v                  # Показать список удаленных репозиториев  
git push origin <branch_name>  # Отправить изменения в удаленный репозиторий  
git pull origin <branch_name>  # Получить изменения из удаленного репозитория  
git fetch                      # Забрать изменения без слияния  
git push --set-upstream origin <branch_name>  # Запомнить удаленную ветку  
```

## Отправка изменений на удаленный репозиторий

Обычно выполняется команда 

```
git push
```
В первый раз нужно вызывать команду с флагом -u

```
git push -u origin main # Если команда приведёт к ошибке, попробуйте 
                          # заменить main на master.
```

----

# Хеш - идентификатор коммита

**Хеширование** (от англ. hash, «рубить», «крошить», «мешанина») — это способ преобразовать набор данных и   получить их «отпечаток» (англ. fingerprint).  

Информация о коммите — это набор данных: когда был сделан коммит, содержимое файлов в репозитории на   момент коммита и ссылка на предыдущий, или родительский (англ. parent), коммит.  

Git хеширует (преобразует) информацию о коммите с помощью алгоритма SHA-1 (от англ. Secure Hash   Algorithm — «безопасный алгоритм хеширования») и получает для каждого коммита свой уникальный хеш —   результат хеширования.  

## Получить сокращенный лог

```
git log --oneline
```

Сокращённый лог полезен, если в репозитории уже много коммитов — например, сотни или тысячи. В этом случае   можно быстро найти нужный по описанию.

Сокращённый хеш (то есть первые несколько символов полного) можно использовать точно так же, как и полный.   Для этого команда git log --oneline автоматически подбирает такую длину сокращённых хешей, чтобы они были   уникальными в пределах репозитория и Git всегда мог понять, о каком коммите идёт речь.  

----

# HEAD — всему голова

# Файл HEAD

Файл HEAD (англ. «голова», «головной») — один из служебных файлов папки .git. Он указывает на коммит, который   сделан последним (то есть на самый новый).  
В этом можно убедиться с помощью терминала. Перейдите в папку .git командой cd. Посмотрите содержимое файла   HEAD командой cat.  
Внутри HEAD — ссылка на служебный файл: refs/heads/master (или refs/heads/main в зависимости от названия   ветки). Если заглянуть в этот файл, можно увидеть хеш последнего коммита.  

Когда вы делаете коммит, Git обновляет refs/heads/master — записывает в него хеш последнего коммита.   Получается, что HEAD тоже обновляется, так как ссылается на refs/heads/master.  
При работе с Git указатель HEAD используется довольно часто. Мы уже упоминали, что многие команды Git   принимают в качестве параметра хеш коммита. Если нужно передать последний коммит, то вместо его хеша можно   просто написать слово HEAD — Git поймёт, что вы имели в виду последний коммит.  

----

# Статусы файлов в Git

## Статусы untracked/tracked, staged и modified

1. **untracked** (англ. «неотслеживаемый»)

Мы говорили, что новые файлы в Git-репозитории помечаются как untracked, то есть неотслеживаемые. Git   «видит», что такой файл существует, но не следит за изменениями в нём. У untracked-файла нет предыдущих   версий, зафиксированных в коммитах или через команду git add.  
2. **staged** (англ. «подготовленный»)    
После выполнения команды git add файл попадает в staging area (от англ. stage — «сцена», «этап [процесса]» и   area — «область»), то есть в список файлов, которые войдут в коммит. В этот момент файл находится в состоянии   staged.  
3. **tracked** (англ. «отслеживаемый»)
Состояние tracked — это противоположность untracked. Оно довольно широкое по смыслу: в него попадают файлы,   которые уже были зафиксированы с помощью git commit, а также файлы, которые были добавлены в staging area   командой git add. То есть все файлы, в которых Git так или иначе отслеживает изменения.  
4. **modified** (англ. «изменённый»)
Состояние modified означает, что Git сравнил содержимое файла с последней сохранённой версией и нашёл   отличия. Например, файл был закоммичен и после этого изменён. 

----
