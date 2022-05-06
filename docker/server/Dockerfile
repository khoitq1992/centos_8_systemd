FROM centos:centos8

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
RUN dnf -y install wget unzip && \
    wget https://getcomposer.org/installer -O composer-installer.php && \
    php composer-installer.php --filename=composer --install-dir=/usr/local/bin

# nodejs
RUN dnf module enable nodejs:12 -y && \
    dnf install nodejs -y

# install font
RUN cd /usr/local/src/ && \
    dnf install -y google-noto-sans-cjk-ttc-fonts && \
    wget https://logotype.jp/wp-content/uploads/2020/10/logofont-m_1.1-ah9kl7yha.zip -O logofont-m.zip && \
    unzip -j logofont-m.zip -d logofont-m && \
    mv logofont-m /usr/share/fonts/logofont-m && \
    wget https://typingart.net/fontdata/hannari.zip --referer="https://typingart.net/?p=44" -O hannari.zip && \
    unzip -j hannari.zip -d Hannari && \
    mv Hannari /usr/share/fonts/Hannari && \
    wget http://modi.jpn.org/download/MODI_kurobara-gothic_2018_1102.zip -O MODI_kurobara-gothic.zip && \
    unzip -j MODI_kurobara-gothic.zip -d MODI_kurobara-gothic && \
    mv MODI_kurobara-gothic /usr/share/fonts/MODI_kurobara-gothic

# config
RUN mkdir /var/www/html/web

# finish
EXPOSE 80/tcp
CMD ["/usr/sbin/init"]