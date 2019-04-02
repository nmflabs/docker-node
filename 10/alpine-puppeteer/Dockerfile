FROM node:10.15.3-alpine

MAINTAINER Nabil Muhammad Firdaus <123.nabil.dev@gmail.com>

ENV PUPPETEER_SKIP_CHROMIUM_DOWNLOAD true
ENV CHROME_PATH /usr/bin/chromium-browser

RUN apk update && apk upgrade \
    # Install some tools.
    && apk --no-cache add \
        build-base \
        autoconf \
        libtool \
        procps \
        bash \
    # Installs latest Chromium (72) package.
    && echo @edge http://nl.alpinelinux.org/alpine/edge/community >> /etc/apk/repositories \
    && echo @edge http://nl.alpinelinux.org/alpine/edge/main >> /etc/apk/repositories \
    && apk --no-cache add \
        chromium@edge \
        nss@edge \
        freetype@edge \
        harfbuzz@edge \
        ttf-freefont@edge \
    # Puppeteer v1.11.0 works with Chromium 72.
    && yarn global add puppeteer@1.11.0 \
    # Add user so we don't need --no-sandbox.
    && addgroup -S pptruser && adduser -S -g pptruser pptruser \
        && mkdir -p /home/pptruser/Downloads /app \
        && chown -R pptruser:pptruser /home/pptruser \
        && chown -R pptruser:pptruser /app

USER pptruser

WORKDIR /app

CMD ["/bin/bash"]
