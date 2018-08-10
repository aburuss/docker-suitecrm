# Образ сервера mariadb, подготовленного для Suite CRM
# https://www.howtoforge.com/tutorial/debian-suitecrm-installation/

# Репозиторий
FROM debian:stable

# Установка пакетов
RUN apt-get clean && apt-get update
RUN apt-get install -y --no-install-recommends apt-utils
RUN echo "debconf debconf/frontend select noninteractive" | debconf-set-selections
RUN apt-get install -qy net-tools vim mariadb-server mariadb-client

VOLUME /var/lib/mysql

EXPOSE 3306 

CMD /usr/bin/mysqld_safe
