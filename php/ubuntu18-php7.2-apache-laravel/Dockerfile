#Download base  da imagem ubuntu 18.04
FROM ubuntu:18.04
#Mantenedor
MAINTAINER Jorge Machado <jorge.vmachado@gmail.com>
ENV DEBIAN_FRONTEND=noninteractive
# Atualização de Repositorio do software
RUN apt-get update
# Instalação do git
RUN apt-get install -yq --no-install-recommends git
# Instalação de Utilitarios
RUN apt-get install -yq --no-install-recommends apt-utils \
curl                 \
openssl              \
nano                 \
graphicsmagick       \
imagemagick          \
ghostscript          \
iputils-ping         \
locales
# Instalação do apache
RUN apt-get install -yq --no-install-recommends apache2
# Istalação SQL  (MySql e SQLite)
RUN apt-get install -yq --no-install-recommends mysql-client sqlite3 libsqlite3-dev
# Instalação do php7.2
RUN apt-get install -yq --no-install-recommends libapache2-mod-php7.2 \
php7.2-cli              \
php7.2-json             \
php7.2-curl             \
php7.2-gd               \
php7.2-ldap             \
php7.2-mbstring         \
php7.2-mysql            \
php7.2-soap             \
php7.2-sqlite3          \
php7.2-xml              \
php7.2-zip              \
php7.2-intl             \
php7.2-opcache          \
php-imagick             \
php7.2-fpm
# Instalação do Composer
RUN apt-get install -yq --no-install-recommends ca-certificates \
&& curl -sS https://getcomposer.org/installer -o composer-setup.php \
&& HASH=93b54496392c062774670ac18b134c3b3a95e5a5e5c8f1a9f115f203b75bf9a129d5daa8ba6a13e2cc8a1da0806388a8 \
&& php composer-setup.php --install-dir=/usr/local/bin --filename=composer \
&& chmod +x /usr/local/bin/composer
# Definir localizações
RUN locale-gen pt_BR.UTF-8 en_US.UTF-8 en_GB.UTF-8 de_DE.UTF-8 es_ES.UTF-8 fr_FR.UTF-8 it_IT.UTF-8 km_KH sv_SE.UTF-8 fi_FI.UTF-8
RUN a2enmod rewrite expires
# configuração apache
RUN chmod +x /etc/apache2/sites-available/000-default.conf \
&& printf "<virtualhost *:80>\n" >> /etc/apache2/sites-available/000-default.conf \
&& printf "\n\tserveradmin webmaster@localhost\n\tdocumentroot /var/www/html\n" >> /etc/apache2/sites-available/000-default.conf \
&& printf "\n\t<directory “/var/www/html”>\n\t\tallowoverride all\n\t</directory>\n" >> /etc/apache2/sites-available/000-default.conf \
&& printf "\n\terrorlog ${apache_log_dir}/error.log\n\tcustomlog ${apache_log_dir}/access.log combined\n" >> /etc/apache2/sites-available/000-default.conf \
&& printf "\n</virtualhost>" >> /etc/apache2/sites-available/000-default.conf \
&& chmod -R 644 /etc/apache2/sites-available/000-default.conf \
&& service apache2 restart
# configuração php.ini
RUN chmod +x /etc/php/7.2/apache2/php.ini \
&& echo "error_log =/tmp/php_errors.log" >> /etc/php/7.2/apache2/php.ini \
&& echo "display_errors = On" >> /etc/php/7.2/apache2/php.ini \
&& echo "memory_limit = 256M" >> /etc/php/7.2/apache2/php.ini \
&& echo "max_execution_time = 120" >> /etc/php/7.2/apache2/php.ini \
&& echo "error_reporting  = E_ALL" >> /etc/php/7.2/apache2/php.ini \
&& echo "file_uploads = On" >> /etc/php/7.2/apache2/php.ini \
&& echo "post_max_size = 100M" >> /etc/php/7.2/apache2/php.ini \
&& echo "upload_max_filesize = 100M" >> /etc/php/7.2/apache2/php.ini \
&& echo "session.gc_maxlifetime = 14000" >> /etc/php/7.2/apache2/php.ini \
&& chmod -R 644 /etc/php/7.2/apache2/php.ini \
&& service apache2 restart
# Instalação do Laravel
RUN composer global require "laravel/installer" \
&& echo 'export PATH="$HOME/.composer/vendor/bin:$PATH"' >> ~/.bashrc \
#&& source ~/.bashrc
EXPOSE 80 443
WORKDIR /var/www/html
CMD ["/bin/bash","apache2ctl", "-D", "FOREGROUND"]
