# vim: set ft=dockerfile:
FROM alpine:latest
# Author with no obligation to maintain
MAINTAINER Paul Tötterman <paul.totterman@iki.fi>

ENV DBHOST="mariadb" \
    DBNAME="racktables" \
    DBUSER="racktables" \
    DBPASS=""

COPY entrypoint.sh /entrypoint.sh
RUN apk --no-cache add php5-fpm php5-gd php5-pdo_mysql php5-ldap php5-snmp php5-pcntl php5-json php5-bcmath php5-curl \
    && chmod +x /entrypoint.sh \
    && wget -O /racktables.tar.gz 'http://downloads.sourceforge.net/project/racktables/RackTables-0.20.11.tar.gz?r=&ts=1456138604&use_mirror=netassist' \
    && mkdir /opt \
    && tar -xz -C /opt -f /racktables.tar.gz \
    && mv /opt/RackTables-0.20.11 /opt/racktables \
    && rm -f /racktables.tar.gz \
    && sed -i \
    -e 's|^listen =.*$|listen = 9000|' \
    -e 's|^;daemonize =.*$|daemonize = no|' \
    /etc/php5/php-fpm.conf

VOLUME /opt/racktables/wwwroot
EXPOSE 9000
ENTRYPOINT ["/entrypoint.sh"]
CMD ["/usr/bin/php-fpm"]
