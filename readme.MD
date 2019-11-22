# Docker environment
#### О проекте
**Докер среда для запуска нескольких сайтов с разными настройками для локальной розработки web приложений.**

#### Запуск
Скопировать и переименовать файл .env.example у .env

```bash
 docker-compose up -d
```
>  (Если первый раз то займет много времени так ка будут загружаться все images)
 
#### Остановка
```bash
 docker-compose stop
```
#### Заметки

##### PhpMyadmin
После установки **phpmyadmin** будет доступен по порту **8080** (http://localhost:8080/) / **pass - root, user - root**
#### Добавить сайт
1. Создать папку для сайта в папке www/ или зделать пулл из репозитория
2. Прописать адрес в файле /etc/hosts (локально на ubuntu)
3. Создать файл конвига в папке images/nginx/hosts/* (скопировать site.example.conf, переименовать и зменить настройки)*

#### Composer, PHP
Команды composer, php запускаем из контейнера php7.2 где они уже установлены

#### Импорт данных из .sql файла
Можем заимпортить через  **phpMyadmin** предварительно создав базу

##### Через командную строку
1. Загружаем файл в папку /dump
2. Из  **mysql** контейнера выполним команду **mysql -u root -p** и** CREATE DATABASE new_database;** и выходим  **exit**;
3. Импортим **mysql -u sid-media_user -p sid-media_rayon <  /home/sid-media/tmp/08-11-2019-sid-media_rayon

4. Ждем окончания выполнения скрипта

#### Возможные проблемы
Заняты порты, их нужно будет освободить

Возможно придеться зделать перенаправлене в /etc/hosts для выполнения пиграций через команду artisan
127.0.0.1       mysql
mysql -u sid-media_user -p -h  localhost -D sid-media_rayon  --binary-mode -o < /home/sid-media/tmp/08-11-2019-sid-media_rayon.gz

##### Остановить
**  mysql**
```bash
 sudo /etc/init.d/mysql stop
```

 **apache2 stop**
```bash
 sudo service apache2 stop
```
**mariadb**
```bash
 sudo service mariadb stop
```
 
 **nginx stop**
 sudo service nginx stop


#### Дополнительные команды
**Пересобрать контейнер**
```bash
docker-compose build --no-cache *container_name*
```

**Удалить  промежуточные (хорошие) образы**
```bash
docker rmi $(docker images -f "dangling=true" -q)
```

**зайти в контейнер**
```bash
docker exec -it name_container bash 
```

**Удалить контейнер**
```bash
docker rm container_id
```

**Доступ по фтп**
```bash
      PUBLICHOST: "localhost"
      FTP_USER_NAME: root
      FTP_USER_PASS: root
```


**БАГ из mysql_mode** (ни в какую не применялись настройки из скопированого файла)
docker rmi $(docker images -f "dangling=true" -q)
docker rm mysql (возможно предідущая команда и не нужна)

**Символическая ссылка**
Здесь нужно создавать ссылку внутри контейнера например в nginx и делать символическую ссылку внутри контейнера

docker exec -it nginx  bash 

ln -s /var/www/папка-проекта/путь-папке /var/www/папка-проекта/путь-папке/название

example - var/www/laravel/storage/app/public /var/www/laravel/public/storage




