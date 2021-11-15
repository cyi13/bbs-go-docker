FROM node:14.5.0

RUN mkdir /app && git clone https://gitee.com/whale_haha/bbs-go.git /app/bbs-go

WORKDIR /app/bbs-go/admin

RUN  npm install --registry=https://registry.npm.taobao.org && npm run build

FROM nginx:1.21.4-alpine

ADD default.conf /etc/nginx/conf.d

WORKDIR /app/bbs-go

COPY --from=0 /app/bbs-go/admin/dist /app/bbs-go/dist

EXPOSE 80