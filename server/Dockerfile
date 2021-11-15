FROM golang:1.17.3

RUN mkdir /app && git clone https://github.com/mlogclub/bbs-go.git /app/bbs-go

WORKDIR /app/bbs-go/server

RUN  go env -w GOPROXY=https://goproxy.cn,direct && \
     GOOS=linux GOARCH=amd64 CGO_ENABLED=0 go build -o bbs-server
    
FROM alpine:latest as prod

WORKDIR /app/bbs-go/server

COPY --from=0 /app/bbs-go/server/bbs-server ./
COPY --from=0 /app/bbs-go/server/bbs-go.docker.yaml .

RUN apk add tzdata && cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

RUN mv bbs-go.docker.yaml bbs-go.yaml && mkdir -p /data/logs /data/www

CMD ["./bbs-server", "-config", "bbs-go.yaml"]