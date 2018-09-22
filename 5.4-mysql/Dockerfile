FROM bitnami/minideb:wheezy

ENV DEBIAN_FRONTEND noninteractive

RUN install_packages php5-fpm php5-mysql nginx supervisor

ADD php-fpm.conf /etc/supervisor/conf.d/
ADD nginx.conf /etc/supervisor/conf.d/

ADD default.conf /etc/nginx/conf.d/

RUN sed -i 's/^\(\[supervisord\]\)$/\1\nnodaemon=true/' /etc/supervisor/supervisord.conf

ADD info.php /app/

CMD ["supervisord", "-c", "/etc/supervisor/supervisord.conf"]