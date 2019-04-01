FROM anvibo/baseimage:14.04

ENV DEBIAN_FRONTEND noninteractive

RUN install-clean php5-fpm php5-mysql nginx supervisor

ADD php-fpm5.5.conf /etc/supervisor/conf.d/php-fpm.conf
ADD nginx.conf /etc/supervisor/conf.d/

ADD default5.5.conf /etc/nginx/sites-available/default

RUN sed -i 's/^\(\[supervisord\]\)$/\1\nnodaemon=true/' /etc/supervisor/supervisord.conf

RUN sed -i 's/^short_open_tag.*/short_open_tag = On/' /etc/php5/fpm/php.ini || echo "short_open_tag = On" >> /etc/php5/fpm/php.ini
RUN sed -i 's/^memory_limit.*/memory_limit = 256M/' /etc/php5/fpm/php.ini || echo "memory_limit = 256M" >> /etc/php5/fpm/php.ini

ADD info.php /app/

CMD ["supervisord", "-c", "/etc/supervisor/supervisord.conf"]
