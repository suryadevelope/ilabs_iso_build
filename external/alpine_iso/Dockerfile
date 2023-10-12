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
                          libffi-dev
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
RUN echo "build ALL=(ALL:ALL) NOPASSWD: ALL" > /etc/sudoers.d/build

USER build

CMD ["/bin/ash"]