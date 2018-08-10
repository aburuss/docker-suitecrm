# Repository
FROM debian:latest

#RUN groupadd -r mysql && useradd -r -g mysql mysql

# Update the repository sources list
RUN apt-get clean && apt-get update

RUN apt-get install -y --no-install-recommends apt-utils

#RUN groupadd -g 124 -r mysql && useradd -u 118 -r -g mysql mysql

RUN echo "debconf debconf/frontend select noninteractive" | debconf-set-selections

#RUN apt-get install -qy supervisor

RUN apt-get install -qy net-tools vim php7.0-mysql mariadb-client cron 
#RUN apt-get install -qy wget curl zip unzip
RUN apt-get install -qy apache2 libapache2-mod-php7.0 php7.0 php7.0-gd php7.0-opcache php7.0-mbstring php7.0-xml php7.0-json php7.0-zip php7.0-curl php7.0-imap

#RUN apt-get -qy install mariadb-server php7.0-mysql mariadb-client

#ADD supervisor.conf /etc/supervisor/conf.d/supervisor.conf

#RUN mkdir -p /var/lock/apache2 /var/run/apache2 /var/log/supervisor


#RUN rm -rf /var/lib/mysql; 
#RUN mkdir -p /var/lib/mysql /var/run/mysqld; 
#RUN	chown -R mysql:mysql /var/lib/mysql /var/run/mysqld; 
#RUN	chmod 777 /var/run/mysqld; 

#VOLUME ["/etc/apache2", "/var/log/apache2", "/var/www", "/var/lib/mysql"]
#VOLUME /var/www/html
#VOLUME ["/etc/apache2", "/var/log/apache2", "/var/www", "/var/lib/mysql"]

EXPOSE 80 443 

#CMD /usr/bin/supervisord -n
#CMD /usr/bin/mysqld_safe
CMD /usr/sbin/apache2ctl -D FOREGROUND
