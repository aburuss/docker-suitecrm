# Образ веб-сервера Apache, подготовленного для Suite CRM
# https://www.howtoforge.com/tutorial/debian-suitecrm-installation/
# на хосте необходимо добавить в crontab запуск шедулера CRM:

#* * * * * /usr/bin/docker exec CONTAINER_NAME sh -c "cd /var/www/html; su www-data -c '/usr/bin/php -f /var/www/html/cron.php' -s /bin/sh"
# также на хосте нужно сделать симлинки для томов
# пример копирования данных в контейнер: docker cp FILE_FROM_HOST CONTAINER_NAME:/var/www/html

# ВАЖНО! при удалении контейнера необходимо следить за томами docker volume ls и удалять ненужные тома

# репозиторий
FROM debian:stable

ENV SUITE_CRM_VERSION 7.10.7

# установка пакетов из репозитория 
RUN apt-get clean && apt-get update && apt-get install -y --no-install-recommends apt-utils
RUN echo "debconf debconf/frontend select noninteractive" | debconf-set-selections
RUN apt-get update \
	&& apt-get install -qy --no-install-recommends net-tools vim php7.0-mysql mariadb-client apache2 libapache2-mod-php7.0 php7.0 php7.0-gd php7.0-opcache php7.0-mbstring php7.0-xml php7.0-json php7.0-zip php7.0-curl php7.0-imap \ 
	&& rm -r /var/lib/apt/lists/*

# настройка apache
RUN a2enmod ssl
RUN a2ensite default-ssl.conf
RUN a2enmod rewrite

COPY cfg/000-default.conf /etc/apache2/sites-enabled/ 
COPY cfg/default-ssl.conf /etc/apache2/sites-enabled/
COPY cfg/php.ini /etc/php/7.0/apache2/
COPY cfg/index.html /var/www/html/

# ключ и сертификат (тестовые и могут быть просрочены, в дальнейшем в нижесозданный каталог необходимо копировать ключи Let's encrypt)
RUN mkdir -p /usr/local/apache2/conf
COPY cfg/server.* /usr/local/apache2/conf/
RUN chmod 0600 /usr/local/apache2/conf/server.key
#RUN rm /var/www/html/index.html 

# установка Suite CRM
#https://suitecrm.com/files/160/SuiteCRM-7.10.7/297/SuiteCRM-7.10.7.zip

#ADD https://suitecrm.com/files/160/SuiteCRM-7.10.7/297/SuiteCRM-7.10.7.zip /tmp/
#ADD https://github.com/salesagility/SuiteCRM/archive/v${SUITE_CRM_VERSION}.zip /tmp/

#>COPY cfg/SuiteCRM-${SUITE_CRM_VERSION}.zip /tmp/
#>RUN unzip /tmp/SuiteCRM-${SUITE_CRM_VERSION}.zip -d /tmp
#>RUN rm /tmp/SuiteCRM-${SUITE_CRM_VERSION}.zip /var/www/html/index.html 
#>RUN chown -cRh www-data:www-data /tmp/SuiteCRM-${SUITE_CRM_VERSION}/*
#>RUN cp -rpf /tmp/SuiteCRM-${SUITE_CRM_VERSION}/* /var/www/html/ 
#>RUN rm -rf /tmp/SuiteCRM-${SUITE_CRM_VERSION} 

RUN rm /var/www/html/index.html 
COPY --chown=www-data:www-data cfg/SuiteCRM-${SUITE_CRM_VERSION} /var/www/html/

# тома контейнера, доступные на хосте в каталоге /var/lib/docker/volumes , доступ к ним должен быть организован через ссылки в каталоге /srv/docker/volumes/a_crm_httpd (где a_crm_httpd - имя образа) 
VOLUME /var/log/apache2
VOLUME /var/www/html
VOLUME /etc/apache2
VOLUME /usr/local/apache2/conf


EXPOSE 80 443 

CMD /usr/sbin/apache2ctl -D FOREGROUND


