**Загрузка сайта**
1. Клонировать репозиторий в папку www/
2. Додати домен в /etc/hosts
4. Створити БД  тут http://localhost:8080/

**запуск** 
 docker-compose up -d
 
**стоп**
 docker-compose stop
  
 
**<<-   -    -   -   -   -   >>**
**Заметки**
  1) - После установки phpmyadmin будет доступен по порту 8080 / pass - root, user - root
  2) - Для добавления нового сайта 
            a) - создать файл конвига в папке hosts
            b) - прописать адрес в файле /etc/hosts
            c) - создать папку для сайта в папке www/
  
**<<-   -    -   -   -   -   >>**
 
 Также возможны проблемы с уже занятыми портами, их нужно будет освободить 
 
 **Остановить  mysql**
 sudo /etc/init.d/mysql stop
 
 **apache2 stop**
 sudo service apache2 stop
 
 sudo service mariadb stop
 
 **nginx stop**
 sudo service nginx stop


**пересобрать контейнер**
docker-compose build --no-cache nginx mysql
