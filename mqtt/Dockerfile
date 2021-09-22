FROM alpine

RUN apk add --no-cache git gcc musl-dev mariadb-connector-c-dev make g++ cjson cjson-dev libxslt libuuid util-linux-dev

RUN git clone https://github.com/eclipse/mosquitto.git
RUN cd mosquitto && git checkout v1.5.7
COPY config.mk /mosquitto
RUN cd mosquitto && make install

RUN git clone https://github.com/jpmens/mosquitto-auth-plug.git
RUN cd mosquitto-auth-plug && cp config.mk.in config.mk && make

COPY mosquitto.conf /mosquitto/mosquitto.conf
CMD ["./mosquitto/src/mosquitto", "-c", "/mosquitto/mosquitto.conf"]

