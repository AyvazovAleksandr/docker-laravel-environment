FROM php:7.4-fpm-alpine

COPY ./compose/beta/workspace/run.sh /tmp

WORKDIR /var/www/html

ENTRYPOINT ["/tmp/run.sh"]