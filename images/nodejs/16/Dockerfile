FROM node:16

RUN groupadd -g 1002 app \
    && useradd -g 1002 -u 1002 -d /var/www -s /bin/bash app

RUN npm install -g @vue/cli

RUN mkdir -p /etc/nginx/html /var/www/html /var/www/html/views /sock \
  && chown -R app:app /etc/nginx /var/www /sock

USER app:app

VOLUME /var/www

WORKDIR /var/www/html/views
EXPOSE 9001