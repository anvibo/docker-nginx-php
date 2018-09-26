FROM anvibo/baseimage:18.04

ENV DEBIAN_FRONTEND noninteractive

RUN install-clean php7.2-fpm php7.2-mysql supervisor nginx

RUN mkdir /run/php
ADD default7.2.conf /etc/nginx/conf.d/
ADD www.conf /etc/php/7.2/fpm/pool.d/
ADD php-fpm7.2.conf /etc/supervisor/conf.d/
ADD nginx.conf /etc/supervisor/conf.d/
RUN sed -i 's/^\(\[supervisord\]\)$/\1\nnodaemon=true/' /etc/supervisor/supervisord.conf

ADD info.php /app/

CMD ["supervisord", "-c", "/etc/supervisor/supervisord.conf"]
