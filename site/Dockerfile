FROM node:14.5.0

RUN mkdir /app && git clone https://github.com/mlogclub/bbs-go.git /app/bbs-go

WORKDIR /app/bbs-go/site

RUN  npm install --registry=https://registry.npm.taobao.org
RUN export NODE_ENV=docker && npm run build

FROM node:14-alpine

WORKDIR /app/bbs-go/site

COPY --from=0 /app/bbs-go/site /app/bbs-go/site

CMD ["node", "/app/bbs-go/site/node_modules/.bin/nuxt", "start" ]