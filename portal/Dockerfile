FROM nginx:alpine
WORKDIR /usr/share/nginx/html

RUN rm -rf ./*

COPY ./html ./

EXPOSE 80

LABEL nome="João Facin Demutti" \
        matricula="26128316"