FROM       ubuntu:18.04

RUN apt-get update && apt-get install -y openssh-server && apt-get install -y openconnect && apt-get install -y sshpass
RUN mkdir /var/run/sshd
RUN echo 'root:root' | chpasswd
RUN sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config

# SSH login fix. Otherwise user is kicked off after login
RUN sed -ri 's/^#?PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config

RUN mkdir /root/.ssh

ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile

RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ENV VPN_SERVER='nvpn.novabase.pt'
ENV VPN_SERVER_CERT='/home/felipemedeiros/Documents/personal_certificate/felipemedeiros.new.crt'
ENV VPN_LOGIN='nb25144'
ENV VPN_PASSWORD='Samoa@029'

COPY ssht.sh /scripts/ssht.sh

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]