**запуск** 
скопировать и переименовать файл .env.example у .env

 docker-compose up -d (Если первый раз то займет много времени так ка будут загружаться все images)
 
**стоп**
 docker-compose stop
  
 
**<<-   -    -   -   -   -   >>**
**Заметки**
  1) - После установки phpmyadmin будет доступен по порту 8080 (http://localhost:8080/) / pass - root, user - root
  2) - Для добавления нового сайта 
            a) - создать папку для сайта в папке www/ или зделать пулл из репозитория
            b) - прописать адрес в файле /etc/hosts (локально на ubuntu)
            c) - создать файл конвига в папке hosts
            
            
Команды composer, php запускаем из контейнера php7.2 где они уже установлены
**<<-   -    -   -   -   -   >>**  
  Импорт данных из .sql файла
    1- Загружаем файл в папку /dump
    2- Создаем БД через phpMyadmin или
        зайдем в mysql контейнер и выполним команду "mysql -u root -p"
        Создаем новую бд командой "CREATE DATABASE new_database;" и выходим "exit"
    3- Выполняем команду "mysql -u root -p new_database < data-dump.sql" (пароль root)
    4- Ждем окончания выполнения скрипта

**<<-   -    -   -   -   -   >>**
 
 Также возможны проблемы с уже занятыми портами, их нужно будет освободить 
 
 **Остановить  mysql**
 sudo /etc/init.d/mysql stop
 
 **apache2 stop**
 sudo service apache2 stop
 
 sudo service mariadb stop
 
 **nginx stop**
 sudo service nginx stop

/****/
Дом команды
**пересобрать контейнер**
docker-compose build --no-cache nginx mysql

**Удалить  промежуточные (хорошие) образы**
docker rmi $(docker images -f "dangling=true" -q)

**зайти в контейнер**
docker exec -it name_container bash (У файле .env задать имя пользвателя по каким заходить в контейнер)

**Удалить контейнер**
docker rm container_id


**Иногда нужен доступ по фтп(цмс например)**
      PUBLICHOST: "localhost"
      FTP_USER_NAME: root
      FTP_USER_PASS: root


