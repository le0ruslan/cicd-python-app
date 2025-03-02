FROM node:22-alpine3.21 AS builder

LABEL version="1.0" maintainer="le0ruslan@mail.ru"

WORKDIR /app

COPY package.json yarn.lock ./

RUN npm install

COPY . .

RUN npm run build

FROM nginx:1.26-alpine

LABEL version="1.0" maintainer="le0ruslan@mail.ru"

COPY --from=builder /app/build /usr/share/nginx/html

COPY ./nginx.conf.template /etc/nginx/templates/default.conf.template

EXPOSE 3000

ENV NGINX_HOST=localhost
ENV NGINX_PORT=3000
