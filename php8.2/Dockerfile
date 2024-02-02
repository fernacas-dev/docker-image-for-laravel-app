FROM php:8.2-apache

# Uncomment if you are using SQL Server
#ENV ACCEPT_EULA=Y
LABEL maintainer="fernan2cas96@gmail.com"

# Download script to install PHP extensions and dependencies
ADD https://raw.githubusercontent.com/mlocati/docker-php-extension-installer/master/install-php-extensions /usr/local/bin/

RUN apt update
RUN chmod uga+x /usr/local/bin/install-php-extensions && sync

RUN DEBIAN_FRONTEND=noninteractive apt update -q
RUN DEBIAN_FRONTEND=noninteractive apt-get install -qq -y curl nano
RUN DEBIAN_FRONTEND=noninteractive apt-get install -qq -y git gnupg
RUN DEBIAN_FRONTEND=noninteractive apt-get install -qq -y zip unzip apt-utils curl

# Uncomment if you are using SQL Server --- SLQ_SERVER_DEPENDENCIES
#RUN curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
#RUN curl https://packages.microsoft.com/config/debian/10/prod.list > /etc/apt/sources.list.d/mssql-release.list
#RUN DEBIAN_FRONTEND=noninteractive apt update -q
#RUN DEBIAN_FRONTEND=noninteractive apt-get install -qq -y msodbcsql17
#RUN echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
#RUN echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
#RUN source ~/.bashrc

# optional: for unixODBC development headers
RUN DEBIAN_FRONTEND=noninteractive apt-get install -qq -y unixodbc-dev
# optional: kerberos library for debian-slim distributions
RUN DEBIAN_FRONTEND=noninteractive apt-get install -qq -y libgssapi-krb5-2

#RUN install-php-extensions memcached

# Uncomment if you are using SQL Server
#RUN install-php-extensions pdo_sqlsrv
#RUN install-php-extensions sqlsrv   

RUN install-php-extensions bcmath
RUN install-php-extensions bz2
RUN install-php-extensions calendar
RUN install-php-extensions exif
RUN install-php-extensions gd
RUN install-php-extensions intl
RUN install-php-extensions ldap
RUN install-php-extensions mysqli
RUN install-php-extensions opcache
RUN install-php-extensions pdo_mysql
RUN install-php-extensions pdo_pgsql
RUN install-php-extensions pgsql
RUN install-php-extensions redis
RUN install-php-extensions soap
RUN install-php-extensions xsl
RUN install-php-extensions zip
RUN install-php-extensions sockets
RUN install-php-extensions odbc

RUN a2enmod rewrite
RUN a2enmod ssl

# Install Composer.
ENV PATH=$PATH:/root/composer2/vendor/bin:/root/composer1/vendor/bin \
  COMPOSER_ALLOW_SUPERUSER=1 \
  COMPOSER_HOME=/root/composer2 \
  COMPOSER1_HOME=/root/composer1

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

ENV APACHE_DOCUMENT_ROOT=/var/www/html

#RUN rm /etc/apache2/sites-enabled/000-default.conf
#COPY ./root  /root
#COPY ./etc/apache2/sites-enabled /etc/apache2/sites-enabled
