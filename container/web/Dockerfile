FROM centos:centos6
MAINTAINER ima0123

RUN yum update -y &&  yum install -y \ 
    epel-release \
    git \
    httpd \
    mod_ssl \
    openssh-server \
    php \
    php-devel \
    php-dom \
    php-gd \
    php-mbstring \
    php-mysql \
    php-pdo \
    php-pecl-apc \
    php-soap \
    rsync \
    tar \
    unzip \
    vim \
    zip 

EXPOSE 22 80 443


COPY ./etc/httpd/httpd.conf /etc/httpd/conf/
COPY ./etc/httpd/conf.d/drupal.conf /etc/httpd/conf.d/
COPY ./etc/php.ini /etc/
COPY ./etc/php.d/apc.ini /etc/php.d/


# Setup bash
COPY ./etc/bashrc /root/.bashrc

# Setup drush
RUN curl -sS https://getcomposer.org/installer | php && \
    mv composer.phar /usr/local/bin/composer

RUN /usr/local/bin/composer global require 'drush/drush:6.*'
RUN /usr/local/bin/composer global install

# RUN yum install -y php-pecl-xdebug

WORKDIR /var/www/html

ENTRYPOINT ["/usr/sbin/apachectl", "-D", "FOREGROUND"]
ENTRYPOINT service sshd start && /usr/sbin/apachectl -D FOREGROUND
