FROM ubuntu:16.04
MAINTAINER ALEC POVOLOTSKIY <a.povolotskiy@gmail.com>

RUN apt-get update && \
    apt-get install -y openssh-server supervisor apache2 nano zip php libapache2-mod-php php-mysql mysql-client php-gd php-dom php-simplexml php-curl php-intl php-xsl php-mbstring php-zip php-xml php-mcrypt php-xdebug composer bash-completion rsync xinetd net-tools redis-server nodejs npm && \
    mkdir -p /var/lock/apache2 /var/run/apache2 /var/run/sshd /var/log/supervisor

# Environment variables from /etc/apache2/apache2.conf
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid

ADD config/vhost.conf /etc/apache2/sites-available/vhost.conf
ADD config/supervisord.conf /etc/supervisor/conf.d/supervisord.conf
ADD config/auth.json /root/.composer/auth.json
ADD config/xdebug.ini /etc/php/7.0/mods-available/xdebug.ini
ADD config/rsyncd.conf /etc/rsyncd.conf
ADD config/xinetd_rsync.conf /etc/xinetd.d/rsync
RUN a2enmod rewrite
RUN echo "PS1='\[\033[1;36m\]\u\[\033[1;31m\]@\[\033[1;32m\]\h:\[\033[1;35m\]\w\[\033[1;31m\]\$\[\033[0m\] '" >> /root/.bashrc

RUN a2ensite vhost && rm /var/www/html/index.html
RUN if test -d /the/dir; then chmod 777 /var/www/html; fi

CMD ["/usr/bin/supervisord"]