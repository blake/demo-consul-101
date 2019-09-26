FROM golang as builder

ARG APPNAME
ARG BASEDIR

COPY $BASEDIR/../../services/$APPNAME/main.go /opt/build

WORKDIR /opt/build

RUN go build .

FROM alpine:3.7
WORKDIR /app
COPY --from=builder main /app
# ADD . /app
EXPOSE 9001
ENV PORT 9001
CMD ["./counting-service"]
