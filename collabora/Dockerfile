
ARG BUILD_FROM=ghcr.io/hassio-addons/debian-base/amd64:7.2.0

# hadolint ignore=DL3006
FROM ${BUILD_FROM}
ARG BUILD_ARCH

ARG SEMAPHORE_VERSION=2.9.37

# Set shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# hadolint ignore=DL3008
RUN apt-get update \
    && apt-get install -y wget \
    && wget --progress=dot:giga https://collaboraoffice.com/downloads/gpg/collaboraonline-release-keyring.gpg -P /usr/share/keyrings/ \
    && echo -e "Types: deb" >> /etc/apt/sources.list.d/collaboraonline.sources \
    && echo -e "URIs: https://www.collaboraoffice.com/repos/CollaboraOnline/CODE-deb" >> /etc/apt/sources.list.d/collaboraonline.sources \
    && echo -e "Suites: ./" >> /etc/apt/sources.list.d/collaboraonline.sources \
    && echo -e "Signed-By: /usr/share/keyrings/collaboraonline-release-keyring.gpg" >> /etc/apt/sources.list.d/collaboraonline.sources \
    && apt-get update \
    && apt-get install -y coolwsd code-brand \
    && rm -fr \
        /tmp/* \
        /etc/nginx \
        /var/{cache,log}/* \
        /var/lib/apt/lists/* \
    \
    && mkdir -p /var/log/nginx \
    && touch /var/log/nginx/error.log

# Copy root filesystem
COPY rootfs /

# Build arguments
ARG BUILD_DATE
ARG BUILD_DESCRIPTION
ARG BUILD_NAME
ARG BUILD_VERSION

# Labels
LABEL \
    io.hass.name="${BUILD_NAME}" \
    io.hass.description="${BUILD_DESCRIPTION}" \
    io.hass.arch="${BUILD_ARCH}" \
    io.hass.type="addon" \
    io.hass.version=${BUILD_VERSION} \
    maintainer="Pedro Luis <contact@pedrol.me>" \
    org.opencontainers.image.title="${BUILD_NAME}" \
    org.opencontainers.image.description="${BUILD_DESCRIPTION}" \
    org.opencontainers.image.vendor="Home Assistant Collabora Add-on" \
    org.opencontainers.image.authors="Pedro Luis <contact@pedrol.me>" \
    org.opencontainers.image.licenses="MIT" \
    org.opencontainers.image.url="https://addons.community" \
    org.opencontainers.image.source="https://github.com/${BUILD_REPOSITORY}" \
    org.opencontainers.image.documentation="https://github.com/${BUILD_REPOSITORY}/blob/main/README.md" \
    org.opencontainers.image.created=${BUILD_DATE} \
    org.opencontainers.image.revision=${BUILD_REF} \
    org.opencontainers.image.version=${BUILD_VERSION}
