FROM almalinux/9-init

ENV HTTPD_PREFIX /usr/local/apache2
ENV PATH $HTTPD_PREFIX/bin:$PATH

RUN groupadd -r www-data && useradd -r --create-home -g www-data www-data
RUN mkdir -p "$HTTPD_PREFIX" \
    && chown www-data:www-data "$HTTPD_PREFIX"
WORKDIR  $HTTPD_PREFIX

SHELL [ "/bin/bash" ,"-o","pipefail","-c" ]

RUN dnf upgrade -y && \
    dnf install -y httpd && \
    dnf install 'dnf-command(config-manager)' -y && \
    dnf config-manager --set-enabled crb && \
    dnf install https://dl.fedoraproject.org/pub/epel/epel-release-latest-9.noarch.rpm -y && \
    dnf install dnf-utils http://rpms.remirepo.net/enterprise/remi-release-9.rpm -y && \
    dnf module enable php:remi-8.1 -y && \
    dnf install php -y  
    
COPY httpd-foreground  /usr/local/bin/
COPY ./conf/httpd.conf /etc/httpd/conf/
COPY ./conf/00-mpm.conf /etc/httpd/conf.modules.d/
RUN chmod 755 /usr/local/bin/httpd-foreground
CMD [ "httpd-foreground" ]
