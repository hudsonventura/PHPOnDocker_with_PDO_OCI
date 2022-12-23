FROM php:7.2.2-fpm
MAINTAINER Hudson Ventura <hudsonventura@outlook.com>

ENV PHP_VERSION=7.2.2 \
    ORACLE_INSTANTCLIENT_VERSION="18_5" \
    PHP_OCI_VERSION=2.2.0

RUN echo 'deb http://httpredir.debian.org/debian jessie contrib' >> /etc/apt/sources.list

RUN apt-get update && apt install -y unzip

RUN export DEBIAN_FRONTEND=noninteractive && apt-get install -y --force-yes libssl-dev curl  libcurl4-gnutls-dev libxml2-dev libicu-dev libmcrypt4 libmemcached11 openssl

#CONFIGURAÇÕES DO OPCACHE
RUN docker-php-ext-install opcache

#CONFIGURAÇÕES DO APCU
RUN pecl install apcu-5.1.5 && docker-php-ext-enable apcu

#LIBS EXTRAS
RUN docker-php-ext-install bcmath
RUN apt-get install -y libbz2-dev
RUN docker-php-ext-install bz2
RUN docker-php-ext-install mbstring
RUN apt-get install -y libpq-dev
RUN apt-get install -y libicu-dev
RUN docker-php-ext-install intl
#RUN apt install -y software-properties-common && add-apt-repository ppa:ondrej/php && apt-get update
#RUN apt-get install -y php7.4-dev




#GD
RUN apt-get install -y libfreetype6-dev libjpeg62-turbo-dev libpng16-16
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/
RUN docker-php-ext-install gd


#PDO - CUSTOMIZAR A SEU DISPOR
RUN docker-php-ext-install pdo_pgsql soap sockets
RUN pecl install xdebug


# Copy Oracle Instantclient files
COPY instantclient/instantclient-basic-linux.x64-18.5.0.0.0dbru.zip /instantclient.zip
COPY instantclient/instantclient-sdk-linux.x64-18.5.0.0.0dbru.zip /instantclient_sdk.zip

# Install Oracle Instantclient
RUN unzip /instantclient.zip -d /usr/local && \
    unzip /instantclient_sdk.zip -d /usr/local && \
    ln -s /usr/local/instantclient_${ORACLE_INSTANTCLIENT_VERSION} /usr/local/instantclient && \
    ln -s /usr/local/instantclient/lib* /usr/lib && \
    rm /instantclient.zip && rm /instantclient_sdk.zip


# Install PHP OCI8 extension
RUN pecl channel-update pecl.php.net && \
    echo 'export LD_LIBRARY_PATH="/usr/local/instantclient"' >> /root/.bashrc && \
    echo 'umask 002' >> /root/.bashrc && \
    echo 'instantclient,/usr/local/instantclient' | pecl install oci8-${PHP_OCI_VERSION} && \
    #echo "extension=oci8.so" > /etc/php/${PHP_VERSION}/fpm/conf.d/php-oci8.ini && \
    #echo "extension=oci8.so" > /usr/local/etc/php/php-oci8.ini && \
    #echo "extension=oci8.so" > /usr/local/etc/php/php-oci8.ini && \
    #echo "extension=oci8.so" > /etc/php/${PHP_VERSION}/cli/conf.d/php-oci8.ini && \
    pecl clear-cache

RUN docker-php-ext-configure oci8 --with-oci8=instantclient,/usr/local/instantclient && docker-php-ext-install oci8
RUN docker-php-ext-configure pdo_oci --with-pdo-oci=instantclient,/usr/local/instantclient && docker-php-ext-install pdo_oci

# verificar se tem alguma biblioteca faltante: ldd /usr/local/lib/php/extensions/no-debug-non-zts-20170718/oci8.so
# se houverem lib faltantes, instalar
RUN apt install libaio1

#LDAP
RUN apt-get update && \
    apt-get install libldap2-dev -y && \
    rm -rf /var/lib/apt/lists/* && \
    docker-php-ext-configure ldap --with-libdir=lib/x86_64-linux-gnu/ && \
    docker-php-ext-install ldap

#PDO_SQLITE
RUN apt-get update && \
    apt-get install -y libsqlite3-dev &&\
    docker-php-ext-install pdo_sqlite

#remais plugins
RUN docker-php-ext-install curl fileinfo gettext mbstring exif




EXPOSE 9003
CMD ["php-fpm"]

