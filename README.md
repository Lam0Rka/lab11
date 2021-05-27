# lab11
## Laboratory work XI

Данная лабораторная работа посвещена изучению процесса создания сеансов совместной разработки с использованием инструмента **ngrok**

0. В процессе разработки бывают ситуации, когда необходимо показать результат другому человеку. Можно делать свой локальный проект и если необходимо получать запросы от внешних сервисов при интеграции.

Для данных случаев можно воспользоваться сервисами создания туннелей до компьютера. Одним из популярных сервисов для построения туннелей до компьютера является ngrok. Он простой и одновременно функциональный.
Для работы с ngrok необходимо:

1. скачать бинарный файл для вашей системы — ngrok;

2. зарегистрировать аккаунт на ngrok для получения токена;

3. удостовериться, что ваш локальный сервис запущен и ожидает HTTP запросов;

4. запустить ngrok.

```sh
$ open https://ngrok.com/
```

## Tasks

- [x] 1. Ознакомиться со ссылками учебного материала
- [x] 2. Выполнить инструкцию учебного материала
- [x] 3. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Tutorial
 переходим в корневой каталог
 Создаем директорию 
 Создаем директорию 
 Задаем локальную переменную HOME_PREFIX
 Выведем значение этой переменной
 Задаем локальную перменную USERNAME

```sh
$ cd ~
$ mkdir install
$ mkdir tmp
$ export HOME_PREFIX=`pwd`/install
$ echo $HOME_PREFIX
$ export USERNAME=`whoami`
```
Переходим в директорию tmp
```sh
$ cd tmp
```
 Скачиваем архив с библиотекой libevent, чтобы взаимодействовать с Libevent API 
 Распаковываем архив и выводим его содержимое
. Переходим в требуемую директорию с библиотекой
. Указываем директорию, в которую будет производится установка
 Производим установку
. Поднимаемся на директорию выше

```sh
$ wget https://github.com/libevent/libevent/releases/download/release-2.1.8-stable/libevent-2.1.8-stable.tar.gz
$ tar -xvzf libevent-2.1.8-stable.tar.gz
$ cd libevent-2.1.8-stable
$ ./configure --prefix=${HOME_PREFIX}
$ make && make install
$ cd ..
```
. Скачиваем архив с библиотекой ncures, чтобы иметь возможность управлять вводом выводом на терминал. Она позволяет не беспокоиться об аппаратных различиях терминалов и писать переносимый код.
. Распаковываем архив и выводим его содержимое
 Переходим в требуемую директорию с библиотекой
. Указываем директорию, в которую будет производится установка
 Производим установку
 Поднимаемся на директорию выше

```sh
$ wget http://invisible-island.net/datafiles/release/ncurses.tar.gz
$ tar -xvzf ncurses.tar.gz
$ cd ncurses-5.9
$ ./configure --prefix=${HOME_PREFIX}
$ make && make install
$ cd ..
```
 Действия аналогичный предыдущим. Устанавливаем tmux.
tmux — свободная консольная утилита-мультиплексор, предоставляющая пользователю доступ к нескольким терминалам в рамках одного экрана.

```sh
$ wget https://github.com/tmux/tmux/releases/download/2.5/tmux-2.5.tar.gz
$ tar -xvzf tmux-2.5.tar.gz
$ cd tmux-2.5
$ ./configure --prefix=${HOME_PREFIX} CFLAGS="-I${HOME_PREFIX}/include -I${HOME_PREFIX}/include/ncurses" LDFLAGS="-L${HOME_PREFIX}/lib"
$ make && make install
$ cd ..
```
 Скачиваем архив, содержащий ngrok
. Установим unzip
 Распаковываем скачаный архив
 Перемещаем каталог с ngrok в директорию bin (полный путь: /Users/navckin/install/bin)
```sh
$ wget https://bin.equinox.io/c/4VmDzA7iaHb/ngrok-stable-linux-amd64.zip
$ unizp ngrok-stable-linux-amd64.zip
$ mv ngrok ${HOME_PREFIX}/bin
```
LD_LIBRARY_PATH -это предопределенная переменная среды в Linux/Unix, которая задает путь, по которому компоновщик должен искать при связывании динамических библиотек/общих библиотек.
 Задаем перемнные окружения 
 Запускаем tmux

```sh
$ export LD_LIBRARY_PATH=${HOME_PREFIX}/lib
$ export PATH="${HOME_PREFIX}/bin:${PATH}"
$ tmux
```
 Возвращяемся в корневой каталог
 Удаляем директории tmp и install

```sh
$ cd ~
$ rm -rf tmp install
```
 Альтернативный способ установки tmux и ngrok
```sh
$ brew install tmux ngrok # or use linuxbrew 🎉
```
 Создаем новую сессию
```sh
$ tmux new -s session_with_group
```
 Теперь необходимо поднять вм, которую создавали в прошлой лабораторной
 Открываем сайт и регистрируемся
 задаем значению переменной значение токена
 Указываем токен в качестве аутентификационного токена
 Указываем порт, чтобы получить доступ по SSH

```sh
# Alisa:
$ open https://ngrok.com/signup
$ export NGROK_TOKEN=<токен>
$ ngrok authtoken ${NGROK_TOKEN}
$ ngrok tcp 22
<порт_ngrok_сервера>
```
 Работаем в виртуальной машине
  Подключемся к созданной групповой сессии
 Вертикальное разделение консольного окна
 
```sh
# Bob:
$ ssh ${USERNAME}@0.tcp.ngrok.io -p<порт_ngrok_сервера>
<пароль_от_учетной_записи>
$ tmux a -t session_with_group
$ <C-B>"
```

## Links

- [Tmux](https://raw.githubusercontent.com/tmux/tmux/master/README)
- [Libevent](http://libevent.org)
- [Ncurses](http://invisible-island.net/ncurses/)

```
Copyright (c) 2015-2021 The ISC Authors
```
