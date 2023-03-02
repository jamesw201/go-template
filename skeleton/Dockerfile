FROM alpine:latest
ENV PORT=3000
ENV HOST=0.0.0.0
RUN apk update && apk upgrade && \
    apk add --no-cache bash git openssh
RUN apk add --no-cache ca-certificates
RUN mkdir /app
WORKDIR /app
COPY ./docker-infrastructure-api-server /app/docker-infrastructure-api-server
RUN chmod +x /app/docker-infrastructure-api-server
EXPOSE 3000
CMD ["/app/infrastructure-api-server"]
