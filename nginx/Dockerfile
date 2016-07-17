FROM alpine:3.3
MAINTAINER JJ Buckley <jj@bjjb.org>
LABEL Description="A minimal vanilla NginX image"
RUN apk add --no-cache nginx curl
COPY nginx.conf /etc/nginx
VOLUME ["/etc/nginx/conf.d", "/var/www"]
EXPOSE 80 443
CMD nginx
