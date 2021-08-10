FROM nginx:1.21.0

WORKDIR /nginx

COPY nginx.conf /etc/nginx/nginx.conf

COPY /files/includes/. /etc/nginx/includes/

COPY /files/ssl/. /etc/ssl/certs/nginx/