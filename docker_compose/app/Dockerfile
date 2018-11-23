FROM golang:latest

RUN mkdir -p /go/src/gitlab.com/tfs18f-ekb-devops/public/application.git/
WORKDIR /go/src/gitlab.com/tfs18f-ekb-devops/public/application.git/
COPY application/ .

RUN CGO_ENABLED=0 go build -o application gitlab.com/tfs18f-ekb-devops/public/application.git


FROM alpine:latest

RUN apk update && apk add ca-certificates && rm -rf /var/cache/apk/*

COPY --from=0 /go/src/gitlab.com/tfs18f-ekb-devops/public/application.git/application /application
COPY --from=0 /go/src/gitlab.com/tfs18f-ekb-devops/public/application.git/static /static

EXPOSE 8080

CMD ["/application"]