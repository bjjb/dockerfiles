FROM alpine:3.4
MAINTAINER JJ Buckley <jj@bjjb.org>
LABEL description="A small cron container"
RUN apk add --no-cache apk-cron
VOLUME ["/etc/crontabs", "/etc/periodic"]
CMD ["crond", "-f"]
