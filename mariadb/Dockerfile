# Образ сервера mariadb, подготовленного для Suite CRM
# https://www.howtoforge.com/tutorial/debian-suitecrm-installation/

# Репозиторий
FROM debian:stable

# Установка пакетов
RUN apt-get clean && apt-get update
RUN apt-get install -y --no-install-recommends apt-utils
RUN echo "debconf debconf/frontend select noninteractive" | debconf-set-selections
RUN apt-get install -qy net-tools vim mariadb-server mariadb-client

COPY --chown=root:root cfg/50-server.cnf /etc/mysql/mariadb.conf.d/

VOLUME /var/lib/mysql

EXPOSE 3306 

CMD /usr/bin/mysqld_safe

# установка:
# docker build -f Dockerfile -t s01_crm_db .

# запуск контейнера:
# docker run -itd --restart=always --name=a_crm_db -p 3336:3306 s01_crm_db

# зайти в контейнер:
# docker exec -it a_crm_db bash

# и запустить:
# mysql -h localhost -e "use mysql; update user set plugin='' where user='root'; flush privileges;"
# mysql_secure_installation
# mysql -uroot -p
# create database mycrm_db;
# grant all privileges on mycrm_db.* to 'crm_user'@'%' identified by 'PASSWORD';
# flush privileges;

# сохранение настроек:
# docker stop a_crm_db
# docker commit a_crm_db s01_crm_db

# ссылка на том:
# sudo ln -s /var/lib/docker/volumes/471a7794897f51618e1cd8f8365a5e3cdaecc9819f746fb8dc2ffd0ff0e56fce/_data  /srv/docker/volumes/suitecrm/db

# удаление контейнера без удаления тома с БД:
# docker stop a_crm_db
# docker rm a_crm_db

# удаление контейнера с удалением тома с БД:
# docker stop a_crm_db
# docker rm -v a_crm_db

