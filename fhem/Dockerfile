ARG BUILD_FROM=ghcr.io/hassio-addons/base:12.2.7
# hadolint ignore=DL3006
FROM ${BUILD_FROM}

# Setup base
RUN \
    apk add --no-cache \
    nginx \
    wget \
    perl \
    perl-socket \
    perl-switch \
    perl-sys-hostname-long \
    perl-json \
    perl-io-socket-ssl \
    perl-crypt-openssl-rsa \
    perl-crypt-openssl-dsa \
    perl-xml-simple \
    perl-socket \
    perl-crypt-rijndael \
    perl-lwp-protocol-https \
    perl-device-serialport \
    perl-net-telnet \
    \
    perl-dev \
    perl-app-cpanminus \
    gcc \
    g++ \
    make \
    \
    && cpanm Digest::CRC \
    \
    && curl -L -s "http://fhem.de/fhem-6.1.tar.gz" \
        | tar zxvf - -C /opt \
    \
    && mv /opt/fhem-6.1 /opt/fhem \
    \
    && echo "attr global nofork 1" | tee -a /opt/fhem/fhem.cfg \
    \
    && rm -r /etc/nginx

## Setting timezone
RUN \
    cp /usr/share/zoneinfo/Europe/Berlin /etc/localtime \
    \
    && echo "Europe/Brussels" > /etc/timezone

# Copy root filesystem
COPY rootfs /

# Build arguments
ARG BUILD_ARCH
ARG BUILD_DATE
ARG BUILD_DESCRIPTION
ARG BUILD_NAME
ARG BUILD_REF
ARG BUILD_REPOSITORY
ARG BUILD_VERSION

# Labels
LABEL \
    io.hass.name="${BUILD_NAME}" \
    io.hass.description="${BUILD_DESCRIPTION}" \
    io.hass.arch="${BUILD_ARCH}" \
    io.hass.type="addon" \
    io.hass.version=${BUILD_VERSION} \
    maintainer="Michael Paul" \
    org.opencontainers.image.title="${BUILD_NAME}" \
    org.opencontainers.image.description="${BUILD_DESCRIPTION}" \
    org.opencontainers.image.vendor="Home Assistant Add-on" \
    org.opencontainers.image.authors="Michael Paul" \
    org.opencontainers.image.licenses="MIT" \
    org.opencontainers.image.url="https://addons.community" \
    org.opencontainers.image.source="https://github.com/${BUILD_REPOSITORY}" \
    org.opencontainers.image.documentation="https://github.com/${BUILD_REPOSITORY}/blob/main/README.md" \
    org.opencontainers.image.created=${BUILD_DATE} \
    org.opencontainers.image.revision=${BUILD_REF} \
    org.opencontainers.image.version=${BUILD_VERSION}