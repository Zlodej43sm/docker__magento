FROM ubuntu:14.04
MAINTAINER ALEC POVOLOTSKIY <a.povolotskiy@gmail.com>

# Get Apache, mysql client, PHP etc (subset of a full LAMP stack - no MySQL server)
RUN apt-get update && \
    apt-get install -y openssh-server supervisor apache2 nano zip apache2 mysql-client php5 php5-curl php5-mcrypt php5-gd php5-mysql php5-xdebug php5-dev php5-json curl python-pip nodejs npm && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /docker-build

# Environment variables from /etc/apache2/apache2.conf
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid
# Enable Apache rewrite module
RUN a2enmod rewrite

# Add the Apache virtual host file
ADD config/lecot_vhost.conf /etc/apache2/sites-available/vhost.conf
ADD config/supervisord.conf /etc/supervisor/conf.d/supervisord.conf
ADD config/auth.json /root/.composer/auth.json

#ADD config/20-mcrypt.ini /etc/php5/cli/conf.d/20-mcrypt.ini
#ADD config/20-mcrypt.ini /etc/php5/apache2/conf.d/20-mcrypt.ini
ADD config/xdebug.ini /etc/php5/cli/conf.d/20-xdebug.ini
ADD config/xdebug.ini  /etc/php5/apache2/conf.d/20-xdebug.ini
RUN echo "PS1='\[\033[1;36m\]\u\[\033[1;31m\]@\[\033[1;32m\]\h:\[\033[1;35m\]\w\[\033[1;31m\]\$\[\033[0m\] '" >> /root/.bashrc

RUN if test -d /the/dir; then chmod 777 /var/www; fi
RUN a2ensite lecot
CMD ["/usr/bin/supervisord"]