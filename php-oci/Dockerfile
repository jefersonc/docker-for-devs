FROM php:7.2.21-fpm-alpine3.9

ENV LD_LIBRARY_PATH /usr/local/instantclient
ENV ORACLE_HOME /usr/local/instantclient

ADD instantclient-sdk-linux.x64-11.2.0.4.0.tar.gz /usr/local
ADD instantclient-sqlplus-linux.x64-11.2.0.4.0.tar.gz /usr/local
ADD instantclient-basic-linux.x64-11.2.0.4.0.tar.gz /usr/local

RUN apk add make php7-pear php7-dev gcc musl-dev libnsl libaio &&\
  ln -s /usr/local/instantclient_11_2 ${ORACLE_HOME} && \
  ln -s ${ORACLE_HOME}/libclntsh.so.* ${ORACLE_HOME}/libclntsh.so && \
  ln -s ${ORACLE_HOME}/libocci.so.* ${ORACLE_HOME}/libocci.so && \
  ln -s ${ORACLE_HOME}/lib* /usr/lib && \
  ln -s ${ORACLE_HOME}/sqlplus /usr/bin/sqlplus &&\
  ln -s /usr/lib/libnsl.so.2.0.0  /usr/lib/libnsl.so.1 &&\
  docker-php-ext-configure pdo_oci --with-pdo-oci=instantclient,${ORACLE_HOME} \
       && echo 'instantclient,${ORACLE_HOME}' | pecl install oci8 \
       && docker-php-ext-install \
               pdo_oci \
       && docker-php-ext-enable \
               oci8 && \
  apk del php7-pear php7-dev gcc musl-dev &&\
  rm -rf /tmp/*.zip /var/cache/apk/* /tmp/pear/

EXPOSE 9000
CMD ["php-fpm"]
