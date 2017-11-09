FROM centos:7

# system update

# set locale
RUN yum -y update && yum clean all && yum reinstall -y glibc-common && yum clean all
RUN localedef -f UTF-8 -i ja_JP ja_JP.UTF-8
ENV LANG ja_JP.UTF-8
ENV LANGUAGE ja_JP:ja
ENV LC_ALL ja_JP.UTF-8
RUN unlink /etc/localtime \
    && ln -s /usr/share/zoneinfo/Japan /etc/localtime

# Install Apache and PHP packages
RUN yum install -y httpd \
    && rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm \
    && rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm \
    && yum install -y php70w php70w-opcache php70w-gd php70w-imap php70w-intl php70w-mbstring php70w-mcrypt php70w-mysql php70w-pear \
    && curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer \
    && sed 's/memory_limit = 128M/memory_limit = 512M/' /etc/php.ini > /tmp/php.ini \
    && mv -f /tmp/php.ini /etc/php.ini

EXPOSE 80

# enable service.
RUN systemctl enable httpd

# exec.
CMD ["/sbin/init"]