FROM local/c8-systemd

# fix repo
RUN cd /etc/yum.repos.d/ && \
    sed -i 's/mirrorlist/#mirrorlist/g' /etc/yum.repos.d/CentOS-* && \
    sed -i 's|#baseurl=http://mirror.centos.org|baseurl=http://vault.centos.org|g' /etc/yum.repos.d/CentOS-* && \
    yum update -y

# enable remi repo
RUN dnf install https://rpms.remirepo.net/enterprise/remi-release-8.rpm -y && \
    dnf install epel-release -y
RUN dnf module enable php:remi-8.0 -y

# httpd 2.4
RUN dnf install httpd -y

# php 8.0
RUN dnf install -y php php-bcmath php-cli php-common php-gd php-intl php-json php-ldap php-mbstring php-mysqlnd php-pdo php-pear php-soap php-xml php-xmlrpc php-pecl-zip php-pgsql

# composer
RUN dnf -y install wget && \
    wget https://getcomposer.org/installer -O composer-installer.php && \
    php composer-installer.php --filename=composer --install-dir=/usr/local/bin

# nodejs
RUN dnf module enable nodejs:12 -y && \
    dnf install nodejs -y

# config
RUN mkdir /var/www/html/web

# finish
EXPOSE 80/tcp
CMD ["/usr/sbin/init"]