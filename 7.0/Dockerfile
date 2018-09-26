FROM anvibo/baseimage:18.04

ENV DEBIAN_FRONTEND noninteractive

RUN install-clean php7.0-fpm supervisor nginx

ADD default7.0.conf /etc/nginx/conf.d/
ADD www.conf /etc/php/7.0/fpm/pool.d/
ADD php-fpm7.0.conf /etc/supervisor/conf.d/
ADD nginx.conf /etc/supervisor/conf.d/
RUN sed -i 's/^\(\[supervisord\]\)$/\1\nnodaemon=true/' /etc/supervisor/supervisord.conf

ADD info.php /app/

CMD ["supervisord", "-c", "/etc/supervisor/supervisord.conf"]
