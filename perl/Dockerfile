FROM ubuntu:trusty
MAINTAINER JJ Buckley <jj@bjjb.org>

# Ignore APT warnings about not having a TTY
ENV DEBIAN_FRONTEND noninteractive

# Ensure UTF-8 locale
RUN echo "LANG=\"en_US.UTF-8\"" > /etc/default/locale
RUN locale-gen en_US.UTF-8
RUN dpkg-reconfigure locales

RUN apt-get update && apt-get install -y curl
RUN curl -Ls http://install.perlbrew.pl | bash
