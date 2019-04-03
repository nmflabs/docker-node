FROM node:10.15.3-alpine

MAINTAINER Nabil Muhammad Firdaus <123.nabil.dev@gmail.com>

ENV PUPPETEER_SKIP_CHROMIUM_DOWNLOAD true
ENV CHROME_PATH /usr/bin/chromium-browser

RUN apk add --no-cache --update \
        # Need some tools to make node_module dependencies work.
        automake \
        make \
        g++ \
        llvm-libunwind \
        openssl-dev \
        zlib-dev \
        libc6-compat \
        libjpeg-turbo-dev \
        libpng-dev \
        autoconf \
        libtool \
        procps \
        bash \
    # Installs latest Chromium (72) package.
    && echo @edge http://nl.alpinelinux.org/alpine/edge/community >> /etc/apk/repositories \
    && echo @edge http://nl.alpinelinux.org/alpine/edge/main >> /etc/apk/repositories \
    && apk add --no-cache --update \
        chromium@edge \
        nss@edge \
        freetype@edge \
        harfbuzz@edge \
        ttf-freefont@edge \
    # Puppeteer v1.11.0 works with Chromium 72.
    && yarn global add puppeteer@1.11.0 \
    # Add user so we don't need --no-sandbox.
    && addgroup -S pptruser && adduser -S -g pptruser pptruser \
        && mkdir -p /home/pptruser/Downloads \
        && chown -R pptruser:pptruser /home/pptruser

USER pptruser

CMD ["/bin/bash"]
