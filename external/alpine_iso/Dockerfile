FROM alpine:edge

ARG USER_ID 1000
ARG RSA_KEY_PASSPHRASE pass

COPY /abuild-keys /abuild-keys
COPY /extras /custom-packages/extras

RUN apk upgrade && \
    apk add alpine-sdk build-base apk-tools alpine-conf openssl \
        busybox fakeroot syslinux xorriso squashfs-tools sudo 
    

USER build

CMD ["/bin/ash"]
