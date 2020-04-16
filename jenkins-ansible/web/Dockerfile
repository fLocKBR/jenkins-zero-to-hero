FROM remote-host

COPY ./conf/nginx.repo /etc/yum.repos.d/nginx.repo

RUN                                                                          \
  yum -y install nginx-1.12.2 openssl --enablerepo=nginx                  && \
  yum -y install epel-release yum-utils                               && \
  yum -y install http://rpms.remirepo.net/enterprise/remi-release-7.rpm      && \
  yum-config-manager --enable remi-php73                                  && \
  yum -y install php php-common php-opcache php-mcrypt php-cli php-gd php-curl php-mysqlnd php-fpm

EXPOSE 80 443

VOLUME /var/www/html /var/log/nginx /var/log/php-fpm /var/lib/php-fpm

COPY ./conf/nginx.conf /etc/nginx/conf.d/default.conf

COPY ./bin/start.sh /start.sh

RUN chmod +x /start.sh

RUN systemctl start php-fpm

CMD /start.sh