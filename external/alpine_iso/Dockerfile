FROM alpine:edge

ARG USER_ID 1000
ARG RSA_KEY_PASSPHRASE pass

COPY /abuild-keys /abuild-keys
COPY /extras /custom-packages/extras

RUN apk upgrade && \
   apk add alpine-sdk build-base apk-tools alpine-conf openssl \
        busybox fakeroot syslinux xorriso squashfs-tools sudo python3-dev \
                          gcc \
                          libc-dev \
                          libffi-dev\
                          libstdc++ gcompat build-base


RUN adduser -s /bin/ash -G abuild -D -h /home/build -u ${USER_ID} build 
RUN mkdir -p /home/build/.abuild && chown build /home/build/.abuild
RUN openssl aes-256-cbc -d -in /abuild-keys/vmconsole-dev.rsa.enc \
        -out /home/build/.abuild/vmconsole-dev.rsa \
        -k "$RSA_KEY_PASSPHRASE" -pbkdf2
RUN chown build /home/build/.abuild/vmconsole-dev.rsa
RUN chmod 600 /home/build/.abuild/vmconsole-dev.rsa 
RUN cp /abuild-keys/vmconsole-dev.rsa.pub /home/build/.abuild/vmconsole-dev.rsa.pub
RUN chown build /home/build/.abuild/vmconsole-dev.rsa.pub 
RUN cp /abuild-keys/vmconsole-dev.rsa.pub /etc/apk/keys/vmconsole-dev.rsa.pub
RUN chown root:root /etc/apk/keys/vmconsole-dev.rsa.pub
RUN chmod 644 /etc/apk/keys/vmconsole-dev.rsa.pub
RUN echo "PACKAGER_PRIVKEY=/home/build/.abuild/vmconsole-dev.rsa" > \
        /home/build/.abuild/abuild.conf
RUN chown build /home/build/.abuild/abuild.conf
RUN chmod 644 /home/build/.abuild/abuild.conf
RUN chown -Rh build:abuild /custom-packages

RUN echo "surya code modified"
RUN ls
RUN curl -fsSL https://raw.githubusercontent.com/arduino/arduino-cli/master/install.sh | sh  && cd bin && ls
RUN df -h
RUN find . -name "arduino-cli"
RUN export PATH="$PATH:bin/arduino-cli" 
RUN ./arduino-cli config init --additional-urls https://arduino.esp8266.com/stable/package_esp8266com_index.json 
RUN ./arduino-cli core update-index
RUN ./arduino-cli core install esp8266:esp8266
RUN ./arduino-cli sketch new buildino
RUN ./arduino-cli compile -b esp8266:esp8266:nodemcuv2 buildino/buildino.ino --verbose

RUN echo "build ALL=(ALL:ALL) NOPASSWD: ALL" > /etc/sudoers.d/build

USER build

CMD ["/bin/ash"]