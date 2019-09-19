FROM ruby:2.6.4-stretch

LABEL maintainer="Lakshmi Narasimhan <lakshmi@shapeblock.com>"

LABEL io.k8s.description="Rails Debian" \
      io.k8s.display-name="Rails debian base image" \
      io.openshift.s2i.scripts-url="image:///usr/libexec/s2i" \
      io.openshift.expose-services="3000:http" \
      io.openshift.tags="rails"

RUN mkdir -p /usr/libexec/s2i
COPY ./s2i/bin/ /usr/libexec/s2i

RUN apt-get update && apt-get install -y --no-install-recommends build-essential default-libmysqlclient-dev ghostscript imagemagick libbz2-1.0 libc6 libcomerr2 libcurl3 libffi6 libgcc1 libgcrypt20 libgmp-dev libgmp10 libgnutls30 libgpg-error0 libgssapi-krb5-2 libhogweed4 libidn11 libidn2-0 libk5crypto3 libkeyutils1 libkrb5-3 libkrb5support0 libldap-2.4-2 libncurses5 libnettle6 libnghttp2-14 libp11-kit0 libpq5 libpsl5 libreadline-dev libreadline7 librtmp1 libsasl2-2 libsqlite3-0 libssh2-1 libssl1.0.2 libssl1.1 libstdc++6 libtasn1-6 libtinfo5 libunistring0 libxml2-dev libxslt1-dev netcat-traditional zlib1g zlib1g-dev apt-transport-https


# nodejs
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash - && apt-get -y install --no-install-recommends nodejs && rm -rf /var/lib/apt/lists/*

# Install Yarn
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
    echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list && \
    apt-get update && apt-get -y install --no-install-recommends yarn

# install bundler
RUN gem install --force bundler -v '< 2'


RUN useradd -u 1001 -r -g 0 -d /app -s /bin/bash -c "Default Application User" default \
    && mkdir -p /app \
    && chown -R 1001:0 /app && chmod -R g+rwX /app

WORKDIR /app

EXPOSE 3000

USER 1001

CMD ["/usr/libexec/s2i/usage"]
