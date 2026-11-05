ARG BUILD_FROM=ghcr.io/home-assistant/base:latest
FROM ${BUILD_FROM}

RUN apk add --no-cache nodejs npm

WORKDIR /app
COPY package.json package-lock.json ./
RUN npm ci --omit=dev

COPY . /app
COPY rootfs /
RUN chmod a+x /etc/services.d/zonepro/run
