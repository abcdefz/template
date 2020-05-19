FROM alpine:3.9

RUN echo $'https://mirrors.tuna.tsinghua.edu.cn/alpine/v3.9/main/\n\
https://mirrors.tuna.tsinghua.edu.cn/alpine/v3.9/community/' > /etc/apk/repositories

RUN apk update
RUN apk upgrade

RUN apk add git
RUN apk add ca-certificates
RUN update-ca-certificates
RUN apk add tzdata
ENV TZ=Asia/Shanghai

RUN apk add nginx
RUN apk add httpie
RUN apk add vim

COPY dist.tar.gz /usr/share/nginx/html/
RUN tar -zxf /usr/share/nginx/html/dist.tar.gz -C /usr/share/nginx/html --strip-components 1
RUN rm -f /usr/share/nginx/html/dist.tar.gz

COPY nginx.conf /
RUN chown -R nginx:nginx /usr/share/nginx/html
RUN mv /nginx.conf /etc/nginx/nginx.conf

CMD nginx && tail -f /var/log/nginx-access.log
