FROM nginx

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update
RUN apt-get -y install php7.0-fpm supervisor
RUN mkdir /run/php/
ADD ../default.conf /etc/nginx/conf.d/
ADD ../www.conf /etc/php/7.0/fpm/pool.d/
ADD ../php-fpm.conf /etc/supervisor/conf.d/
ADD ../nginx.conf /etc/supervisor/conf.d/
RUN sed -i 's/^\(\[supervisord\]\)$/\1\nnodaemon=true/' /etc/supervisor/supervisord.conf

ADD info.php /app/

CMD ["supervisord", "-c", "/etc/supervisor/supervisord.conf"]
