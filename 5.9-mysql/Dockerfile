FROM anvibo/baseimage:14.04-18.2609.3 

ENV DEBIAN_FRONTEND noninteractive

RUN install-clean php5-fpm php5-mysql nginx supervisor

ADD php-fpm5.conf /etc/supervisor/conf.d/php-fpm.conf
ADD nginx.conf /etc/supervisor/conf.d/

ADD default5.conf /etc/nginx/conf.d/default.conf

RUN sed -i 's/^\(\[supervisord\]\)$/\1\nnodaemon=true/' /etc/supervisor/supervisord.conf

ADD info.php /app/

CMD ["supervisord", "-c", "/etc/supervisor/supervisord.conf"]
