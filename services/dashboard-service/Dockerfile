FROM golang:1.12.17 as builder
ARG TARGETOS
ARG TARGETARCH

COPY main.go src/dashboard-service/main.go
COPY assets src/dashboard-service/assets

RUN cd src/dashboard-service && \
    go get && \
    go get github.com/GeertJohan/go.rice/rice && \
    rice embed-go && \
    CGO_ENABLED=0 GOARCH=${TARGETARCH} GOOS=${TARGETOS} go build -v

FROM alpine:3.7
WORKDIR /app
COPY --from=builder /go/src/dashboard-service/dashboard-service /app/
EXPOSE 9002
ENV PORT 9002
ENV COUNTING_SERVICE_URL http://counting.service.consul:9001
CMD ["./dashboard-service"]
