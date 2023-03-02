FROM alpine:latest
ENV PORT=3000
ENV HOST=0.0.0.0
RUN apk update && apk upgrade && \
    apk add --no-cache bash git openssh
RUN apk add --no-cache ca-certificates
RUN mkdir /app
WORKDIR /app
COPY ./infrastructure-api-server /app/infrastructure-api-server
RUN chmod +x /app/infrastructure-api-server
EXPOSE 3000
CMD ["/app/infrastructure-api-server"]
