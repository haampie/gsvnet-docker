FROM nginx

ADD nginx.conf /etc/nginx/
ADD gsvnet.conf /etc/nginx/conf.d/default.conf
ADD mailcatcher.conf /etc/nginx/conf.d/mailcatcher.conf

RUN echo "upstream php-upstream { server php:9000; }" > /etc/nginx/conf.d/upstream.conf

EXPOSE 80
EXPOSE 443
