FROM       ubuntu:trusty
MAINTAINER JJ Buckley <jj@bjjb.org>

# Ignore APT warnings about not having a TTY
ENV DEBIAN_FRONTEND noninteractive

# Set $PATH so that non-login shells will see the Ruby binaries
ENV PATH $PATH:/opt/rubies/ruby-2.1.2/bin

# Ensure UTF-8 locale
RUN echo "LANG=\"en_US.UTF-8\"" > /etc/default/locale
RUN locale-gen en_US.UTF-8
RUN dpkg-reconfigure locales

# Update and install system software
RUN apt-get update && apt-get upgrade -y && apt-get install -y build-essential curl nginx

# Install ruby-install
RUN curl -Ls https://github.com/postmodern/ruby-install/archive/v0.4.3.tar.gz | tar -xzv && \
    make -C ruby-install-0.4.3 install && \
    rm -r ruby-install-0.4.3

# Install ruby (with ruby-install)
RUN ruby-install ruby 2.3.0

# Install bundler (with rubygems)
RUN gem install bundler

# Ensure nginx doesn't start daemonized
RUN echo "daemon off;\n" >> /etc/nginx/nginx.conf

# Clean up
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Open the HTTP port
EXPOSE 80

# Start nginx
CMD service nginx start
