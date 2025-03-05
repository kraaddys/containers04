# Лабораторная работа №4. Использование контейнеров как среды выполнения

## Студент

**Славов Константин, группа I2302**  
**Дата выполнения: _05.03.2025_**

## Цель работы

Данная лабораторная работа призвана напомнить основные команды ОС **Debian/Ubuntu**. Также она позволит познакомиться с **Docker** и его основными командами.

## Задание

Запустить контейнер Ubuntu, установить Web-сервер Apache и вывести в браузере страницу с текстом `Hello, World!`.

## Ход работы

1. Создайте репозиторий `containers04` и склонируйте его себе на компьютер.

    ![image](https://i.imgur.com/kJEuuoF.jpeg)

2. Откройте терминал в папке containers04 и выполните команду:

```sh
docker run -ti -p 8000:80 --name containers04 ubuntu bash
```

Здесь выполняется запуск нового контейнера с **Ubuntu** в **Docker**. Контейнеру присваивается имя `containers04`, а также осуществляется проброс порта 80 контейнера на порт 8000 хоста. После этого система проверяет наличие образа **Ubuntu** локально, не находит его и загружает последнюю версию из официального репозитория. Затем контейнер запускается в интерактивном режиме с оболочкой **Bash**.

![image](https://i.imgur.com/hzTVwpc.jpeg)

После этого у пользователя появляются root-права.

3. В открывшемся окне выполните следующие команды и объясните их назначение.

```sh
apt update
apt install apache2 -y
service apache2 start
```

![image](https://i.imgur.com/Gm1UYnI.jpeg)

В контейнере выполняется команда `apt update`, которая обновляет список доступных пакетов из репозиториев. В результате система сообщает, что 18 пакетов можно обновить.

![image](https://i.imgur.com/fHgsTpx.jpeg)

Здесь выполняется установка веб-сервера **Apache** с помощью команды `apt install apache2 -y`. Вместе с **Apache** устанавливаются дополнительные пакеты, такие как `apache2-bin`, `apache2-data` и другие зависимости.

![image](https://i.imgur.com/xmQV8Z7.jpeg)

На данном скриншоте запускается веб-сервер **Apache** командой `service apache2 start`. Во время запуска выводится предупреждение `AH00558`, указывающее, что сервер не может определить своё полное доменное имя. Это связано с отсутствием директивы **ServerName** в конфигурации.

4. Откройте браузер и введите в адресной строке `http://localhost:8000`. Что вы видите?

В открывшемся окне появилась стандартная страница сервера Apache и надпись **"It Works!"**, по этой надписи можно понять, что все предыдущие операции выполнены корректно.

![image](https://i.imgur.com/ICt1Gcn.jpeg)

5. Выполните следующие команды:

```sh
ls -l /var/www/html/
echo '<h1>Hello, World!</h1>' > /var/www/html/index.html
```

6. Обновите страницу в браузере. Что вы видите?

После обновления страницы в браузере, на странице появилась надпись **"Hello, World!"**.

Это произошло потому, что выполняется команда:

```sh
echo '<h1>Hello, World!</h1>' > /var/www/html/index.html
```

которая заменяет содержимое файла index.html, добавляя в него HTML-код с заголовком:

```html
<h1>Hello, World!</h1>
```

![image](https://i.imgur.com/oiWWGxb.jpeg)

7. Выполните следующие команды:

```sh
cd /etc/apache2/sites-enabled/
cat 000-default.conf
```

![image](https://i.imgur.com/UGadVje.jpeg)

Тут происходит переход в директорию `/etc/apache2/sites-enabled/`, где хранятся конфигурационные файлы активных сайтов. Затем выполняется команда `cat 000-default.conf`, которая выводит содержимое стандартного конфигурационного файла виртуального хоста. В конфигурации указано, что корневой каталог веб-сервера находится по пути `/var/www/html`, а файлы логов записываются в `error.log` и `access.log`.

8. Закройте окно терминала командой `exit`.

![image](https://i.imgur.com/LwRU4cR.jpeg)

9. Просмотрите список контейнеров.

```sh
docker ps -a
```

После выполнения выводится список всех контейнеров, включая остановленные. В списке отображаются существующие контейнеры.

10. Удалите контейнер.

```sh
docker rm containers04
```

Команда удаляет контейнер с названным именем, в данном случае с именем `containers04`.

![image](https://i.imgur.com/XyH5mp5.jpeg)

## Выводы

В рамках лабораторной работы был создан и запущен контейнер на основе образа `ubuntu:latest`, в котором был установлен и настроен веб-сервер Apache. После успешного запуска контейнера веб-страница корректно открывалась в браузере по адресу `http://localhost:8000`.  

В ходе работы были освоены ключевые команды Docker, включая создание и запуск контейнеров, настройку их окружения, работу с файловой системой внутри контейнера, а также управление остановленными контейнерами. Полученные знания послужат фундаментом для дальнейшего изучения контейнеризации и эффективного использования Docker в практических задачах.

## Библиография

- [Официальная документация Docker](https://docs.docker.com) - Подробный справочник по установке, настройке и использованию Docker. Включает примеры работы с контейнерами, образами, сетями и томами.
- [Docker Hub – репозиторий образов](https://hub.docker.com) - Каталог официальных и пользовательских Docker-образов, включая `ubuntu` и `apache`.
- [Официальная документация Apache HTTP Server](https://httpd.apache.org/docs/) - Руководство по установке, настройке и администрированию веб-сервера Apache.
- [DigitalOcean – руководство по установке Apache в Docker](https://www.digitalocean.com/community/tutorials/docker-explained-how-to-containerize-and-use-apache-on-ubuntu) - Подробная статья о развертывании Apache внутри Docker-контейнера.
- [Medium – практические статьи по Docker](https://medium.com/tag/docker) - Различные кейсы и туториалы по работе с Docker.
- [Medium – практические статьи по Apache](https://medium.com/tag/apache) - Различные кейсы и туториалы по работе с Docker и веб-сервером Apache.
