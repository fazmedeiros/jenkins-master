FROM centos

RUN yum -y install openssh-server

RUN useradd fazmedeiros && \
    echo "Samoa@029" | passwd remote_user --stdin && \
    mkdir /home/fazmedeiros/.ssh && \
    chmod 700 /home/fazmedeiros/.ssh

COPY remote-key.pub /home/fazmedeiros/.ssh/authorized_keys

RUN chown fazmedeiros:fazmedeiros -R /home/fazmedeiros/.ssh/ && \
    chmod 600 /home/fazmedeiros/.ssh/authorized_keys

RUN /usr/sbin/sshd-keygen

RUN yum -y install openconnect

CMD /usr/sbin/sshd -D
