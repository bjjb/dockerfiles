FROM alpine:3.3
MAINTAINER JJ Buckley <jj@bjjb.org>
LABEL Description="A minimal NginX container image"
WORKDIR /etc/nginx
RUN apk add --no-cache nginx               && \
    rm -rv *.default /etc/nginx/default.d
COPY nginx.conf .
VOLUME /etc/nginx/conf.d
EXPOSE 80 443
ENTRYPOINT nginx
