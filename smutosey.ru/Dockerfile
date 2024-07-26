FROM nginx:alpine as build
LABEL authors="smutosey"

ARG HUGO_VERSION="0.129.0"
RUN apk add --update wget
RUN wget --quiet "https://github.com/gohugoio/hugo/releases/download/v${HUGO_VERSION}/hugo_${HUGO_VERSION}_Linux-64bit.tar.gz" && \
    tar xzf hugo_${HUGO_VERSION}_Linux-64bit.tar.gz && \
    rm -r hugo_${HUGO_VERSION}_Linux-64bit.tar.gz && \
    mv hugo /usr/bin && \
    chmod 755 /usr/bin/hugo
WORKDIR /src
COPY . /src
# Build the Hugo site
RUN hugo --environment production

FROM nginx:alpine
COPY --from=build /src/public /usr/share/nginx/html