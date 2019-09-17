FROM ruby:2.6-alpine

LABEL maintainer="Lakshmi Narasimhan <lakshmi@shapeblock.com>"

LABEL io.k8s.description="Rails Alpine" \
      io.k8s.display-name="Rails alpine base image" \
      io.openshift.s2i.scripts-url="image:///usr/libexec/s2i" \
      io.openshift.expose-services="3000:http" \
      io.openshift.tags="rails"

RUN mkdir -p /usr/libexec/s2i
COPY ./s2i/bin/ /usr/libexec/s2i

COPY fix-permissions /usr/local/bin

RUN apk add --update --no-cache \
    build-base \
    postgresql-dev \
    git \
    imagemagick \
    nodejs \
    yarn ruby-bundler \
    tzdata

# workaround for numeric UIDs in alpine.
# https://blog.openshift.com/jupyter-on-openshift-part-6-running-as-an-assigned-user-id/
RUN chmod g+w /etc/passwd

RUN mkdir /cache


RUN adduser -u 1001 -g 0 -D -h /app -s /bin/sh default \
    && mkdir -p /app \
    && chown -R 1001:0 /app && chmod -R g+rwX /app \
    && chown -R 1001:0 /cache && chmod -R g+rwX /cache

WORKDIR /app

EXPOSE 3000

USER 1001

CMD ["/usr/libexec/s2i/usage"]
