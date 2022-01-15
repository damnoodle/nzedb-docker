#
# nZEDb PHP Dockerfile
# Create a quick and clean dev environment
#

FROM alpine:3.14
MAINTAINER damnoodle <https://github.com/damnoodle>

# Set correct environment variables.
ENV TZ America/Chicago
ENV HOME /root
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US.UTF-8
ENV LC_ALL en_US.UTF-8

# Make sure system is up-to-date.
RUN \
  apk update && \
  apk upgrade

# Install PHP.
RUN apk add git php7 php7-pear php7-gd php7-mysqli php7-curl php7-json php7-phar php7-imagick php7-pdo_mysql php7-mcrypt php7-common php7-xml php7-openssl php7-zlib php7-ctype php7-exif php7-iconv php7-sockets php7-fpm memcached php7-memcache
# RUN sed -ri 's/(max_execution_time =) ([0-9]+)/\1 120/' /etc/php7/php.ini
# RUN sed -ri 's/(memory_limit =) ([0-9]+)/\1 -1/' /etc/php7/php.ini
# RUN sed -ri 's/;(date.timezone =)/\1 Europe\/London/' /etc/php7/php.ini
ADD php.ini /etc/php7/php.ini
ADD php-fpm.conf /etc/php7/php-fpm.conf
#RUN \
#  set -x && \
#  addgroup -g 82 -S www-data && \
#  adduser -u 82 -D -S -G www-data www-data

# Install simple_php_yenc_decode.
# Commented out because it causes problems.
# RUN \
#   apk add git boost-dev build-base && \
#   cd /tmp && \
#   git clone https://github.com/kevinlekiller/simple_php_yenc_decode
# ADD simple_php_yenc_decode.sh /tmp/simple_php_yenc_decode/simple_php_yenc_decode.sh
# RUN \
#   cd /tmp/simple_php_yenc_decode/ && \
#   ./simple_php_yenc_decode.sh && \
#   apk del git boost-dev build-base && \
#   apk add boost

# Install yydecode
RUN \
  apk add build-base && \
  cd /tmp && \
  mkdir -p yydecode && \
  cd yydecode && \
  wget http://netassist.dl.sourceforge.net/project/yydecode/yydecode/0.2.10/yydecode-0.2.10.tar.gz && \
  tar xf yydecode-0.2.10.tar.gz && \
  cd yydecode-0.2.10 && \
  ./configure && \
  make && \
  make install && \
  apk del build-base

# Expose ports
EXPOSE 9000

# Clean up when done.
RUN rm -rf /tmp/* /var/tmp/*

# Run.
CMD ["php-fpm"]
