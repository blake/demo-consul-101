FROM golang:1.12.17 as builder
ARG TARGETOS
ARG TARGETARCH

COPY ./main.go src/counting-service/main.go

RUN cd src/counting-service && \
    go get && \
    CGO_ENABLED=0 GOARCH=${TARGETARCH} GOOS=${TARGETOS} go build -v

FROM alpine:3.7
WORKDIR /app
COPY --from=builder /go/src/counting-service/counting-service /app/
EXPOSE 9001
ENV PORT 9001
CMD ["./counting-service"]
