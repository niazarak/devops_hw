FROM golang:latest

RUN mkdir -p /go/src/gitlab.com/tfs18f-ekb-devops/public/application.git/
WORKDIR /go/src/gitlab.com/tfs18f-ekb-devops/public/application.git/
COPY application/ .

RUN CGO_ENABLED=0 go build -o application gitlab.com/tfs18f-ekb-devops/public/application.git


FROM scratch

COPY --from=0 /go/src/gitlab.com/tfs18f-ekb-devops/public/application.git/application /application
COPY --from=0 /go/src/gitlab.com/tfs18f-ekb-devops/public/application.git/static /static

ENV REDIS_ADDRESS=redis://redis:6379
ENV POSTGRES_ADDRESS=postgres://feed:feed@db:5432/feed?sslmode=disable
ENV RSS_URL=http://rss.nytimes.com/services/xml/rss/nyt/HomePage.xml

EXPOSE 8080

ENTRYPOINT ["/application"]