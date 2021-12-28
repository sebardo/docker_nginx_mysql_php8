FROM aciliadevops/nginx:latest

ADD etc/nginx/sites-enabled /etc/nginx/sites-enabled/

ADD root/ssl/openssl.conf /root/ssl
RUN /root/ssl/sign.sh

WORKDIR /home