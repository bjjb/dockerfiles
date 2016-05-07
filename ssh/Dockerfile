FROM alpine:3.3

MAINTAINER JJ Buckley <jj@bjjb.org> (http://bjjb.org)

ARG user

RUN adduser -D $user
RUN mkdir /home/$user/.ssh
COPY id_rsa.pub /home/$user/.ssh/authorized_keys
RUN chown -Rv $user:$user /home/$user/.ssh
RUN chmod 600 /home/$user/.ssh/authorized_keys
RUN chmod 700 /home/$user/.ssh

RUN apk add --no-cache openssh
RUN ssh-keygen -f /etc/ssh/ssh_host_rsa_key -N '' -t rsa
COPY sshd_config /etc/ssh/sshd_config

EXPOSE 22 2222

CMD ["/usr/sbin/sshd", "-D"]
