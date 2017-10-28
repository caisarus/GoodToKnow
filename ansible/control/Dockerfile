FROM ubuntu:trusty

ENV AUTHORIZED_KEYS_FILE /.ssh/authorized_keys

RUN apt-get update && apt-get install -y openssh-server

RUN useradd ansible && mkdir /home/ansible && chown ansible:ansible /home/ansible && echo "ansible ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers && usermod -s /bin/bash ansible

ADD authorized_keys /home/ansible/.ssh/

ADD id_rsa /home/ansible/.ssh/

RUN chown -R ansible:ansible /home/ansible && chmod 0600 /home/ansible/.ssh/authorized_keys && mkdir /var/run/sshd && chmod 0755 /var/run/sshd


EXPOSE 22

ENV TERM xterm

ADD entrypoint.sh /
RUN chmod +x /entrypoint.sh

CMD ["/entrypoint.sh"]
