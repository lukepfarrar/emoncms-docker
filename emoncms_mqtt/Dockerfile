FROM php:7.3.9-cli
# ENTRYPOINT [ "tail", "-f", "/dev/null" ]


RUN apt-get update && apt-get install -y libmosquitto-dev gettext libc-ares-dev libcurl4-openssl-dev libmariadb-dev-compat libmariadb-dev uuid-dev git libssl-dev mosquitto-dev xsltproc libcjson1 libcjson-dev docbook-xsl docbook

RUN docker-php-ext-install -j$(nproc) mysqli gettext json

RUN pecl install redis && docker-php-ext-enable redis
RUN pecl install Mosquitto-beta && docker-php-ext-enable mosquitto

RUN git clone https://github.com/eclipse/mosquitto.git
RUN git clone https://github.com/jpmens/mosquitto-auth-plug.git

RUN cd mosquitto && make
RUN ln -s /mosquitto/include/mosquitto_broker.h /usr/include
RUN cd mosquitto-auth-plug && cp config.mk.in config.mk && make

