FROM nginx

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update
RUN apt-get -y install wget php7.0-fpm supervisor php7.0-xml php7.0-mysql php7.0-mbstring php7.0-gd php7.0-ldap php7.0-zip php7.0-imap php7.0-pgsql
RUN wget https://github.com/LimeSurvey/LimeSurvey/archive/3.14.7+180827.tar.gz -O /tmp/ls.tar.gz
RUN mkdir /run/php/
ADD default.conf /etc/nginx/conf.d/
ADD www.conf /etc/php/7.0/fpm/pool.d/
ADD php-fpm.conf /etc/supervisor/conf.d/
ADD nginx.conf /etc/supervisor/conf.d/
RUN sed -i 's/^\(\[supervisord\]\)$/\1\nnodaemon=true/' /etc/supervisor/supervisord.conf

ADD info.php /app/

RUN cd /tmp && tar zxf /tmp/ls.tar.gz
RUN mv /tmp/LimeSurvey-*/* /app/
RUN chown -R www-data:www-data /app/tmp
RUN chown -R www-data:www-data /app/upload
RUN chown -R www-data:www-data /app/application/config
RUN chown -R www-data:www-data /var/lib/php/sessions 


CMD ["supervisord", "-c", "/etc/supervisor/supervisord.conf"]
