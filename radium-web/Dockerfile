FROM node:8 as builder

WORKDIR /app
RUN \
  apt-get update && apt-get install -y git

RUN \
  git clone https://github.com/ztl8702/jitsi-meet && \
  cd jitsi-meet && git checkout local-recording && \
  cat package-lock.json | grep url-polyfill && \
  npm install && \
  make && \
  rm -rf node_modules

FROM jitsi/web

RUN rm -rf /usr/share/jitsi-meet

COPY --from=builder /app/jitsi-meet /usr/share/jitsi-meet