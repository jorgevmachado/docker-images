#Download base  da imagem alpine
FROM alpine
#Mantenedor
MAINTAINER Jorge Machado <jorge.vmachado@gmail.com>
# Adiciona o  repositorio do alpine
RUN echo "http://dl-cdn.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories
# Atualização de Repositorio do software
RUN apk update && apk upgrade
# Instalação do git
RUN apk add git
# Instalação de Utilitarios e do apache
RUN apk add     \
bash            \
apache2         \
curl            \
ca-certificates \
openssl         \
openssh
# Instalação do php base
RUN apk add  \
php7-apache2 \
php7         \
php7-phar    \
php7-json    \
php7-iconv   \
php7-openssl \
tzdata       \
openntpd     \
nano
# Instalação do Composer
RUN curl -sS https://getcomposer.org/installer | php \
&& mv composer.phar /usr/local/bin/composer
# Configuração apache e php
RUN apk add       \
  php7-fpm        \
  php7-ftp        \
  php7-xdebug     \
  php7-mcrypt     \
  php7-mbstring   \
  php7-soap       \
  php7-gmp        \
  php7-dom        \
  php7-zip        \
  php7-bcmath     \
  php7-gd         \
  php7-pdo        \
  php7-pdo_odbc   \
  php7-odbc       \
  php7-pdo_mysql  \
  php7-mysqli     \
  php7-pdo_sqlite \
  php7-sqlite3    \
  php7-pdo_pgsql  \
  php7-pdo_dblib  \
  php7-gettext    \
  php7-xmlreader  \
  php7-xmlwriter  \
  php7-tokenizer  \
  php7-xmlrpc     \
  php7-bz2        \
  php7-curl       \
  php7-ctype      \
  php7-session    \
  php7-redis      \
  php7-exif       \
  php7-opcache    \
  php7-zlib       \
  php7-xml        \
  php7-pcntl      \
  php7-posix      \
  php7-fileinfo   \
  php7-intl
# Problemas na instalação na pilha acima
RUN apk add php7-simplexml
RUN cp /usr/bin/php7 /usr/bin/php \
&& rm -f /var/cache/apk/*
# Adicione o apache para executar e configurar
RUN mkdir /run/apache2 \
&& sed -i "s/#LoadModule\ rewrite_module/LoadModule\ rewrite_module/" /etc/apache2/httpd.conf \
&& sed -i "s/#LoadModule\ session_module/LoadModule\ session_module/" /etc/apache2/httpd.conf \
&& sed -i "s/#LoadModule\ session_cookie_module/LoadModule\ session_cookie_module/" /etc/apache2/httpd.conf \
&& sed -i "s/#LoadModule\ session_crypto_module/LoadModule\ session_crypto_module/" /etc/apache2/httpd.conf \
&& sed -i "s/#LoadModule\ deflate_module/LoadModule\ deflate_module/" /etc/apache2/httpd.conf \
&& sed -i "s#^DocumentRoot \".*#DocumentRoot \"/app/public\"#g" /etc/apache2/httpd.conf \
&& sed -i "s#/var/www/localhost/htdocs#/app/public#" /etc/apache2/httpd.conf \
&& printf "\n<Directory \"/app/public\">\n\tAllowOverride All\n</Directory>\n" >> /etc/apache2/httpd.conf
RUN mkdir /app && mkdir /app/public && chown -R apache:apache /app && chmod -R 755 /app && mkdir bootstrap
ADD start.sh /bootstrap/
RUN chmod +x /bootstrap/start.sh
# Instalação do Laravel
RUN composer global require "laravel/installer" \
&& echo 'export PATH="$HOME/.composer/vendor/bin:$PATH"' >> ~/.bashrc
RUN source ~/.bashrc
EXPOSE 80
WORKDIR /app/public
ENTRYPOINT ["/bootstrap/start.sh"]
