# Copyright 2017-2017 Amazon.com, Inc. or its affiliates. All Rights Reserved.
#
# Licensed under the Amazon Software License (the "License"). You may not use this file except in compliance with the License.
# A copy of the License is located at
#
#    http://aws.amazon.com/asl/
#
# or in the "license" file accompanying this file.
# This file is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, express or implied.
# See the License for the specific language governing permissions and limitations under the License.
#

FROM ubuntu:18.04

# DEBIAN_FRONTEND=noninteractive required to stop the tzdata package install interaction
ENV DEBIAN_FRONTEND=noninteractive \
    DOCKER_BUCKET="download.docker.com" \
    DOCKER_VERSION="17.09.0-ce" \
    DOCKER_CHANNEL="stable" \
    DOCKER_SHA256="a9e90a73c3cdfbf238f148e1ec0eaff5eb181f92f35bdd938fd7dab18e1c4647" \
    DIND_COMMIT="3b5fac462d21ca164b3778647420016315289034" \
    DOCKER_COMPOSE_VERSION="1.21.2" \
    GITVERSION_VERSION="3.6.5"

# Install git, SSH, and other utilities
RUN set -ex \
    && echo 'Acquire::CompressionTypes::Order:: "gz";' > /etc/apt/apt.conf.d/99use-gzip-compression \
    && apt-get update \
    && apt-get install software-properties-common -y --no-install-recommends \
    && apt-add-repository ppa:git-core/ppa \
    && apt-get update \
    && apt-get install git=1:2.* -y --no-install-recommends \
    && git version \
    && apt-get install -y --no-install-recommends openssh-client \
    && mkdir ~/.ssh \
    && touch ~/.ssh/known_hosts \
    && ssh-keyscan -t rsa,dsa -H github.com >> ~/.ssh/known_hosts \
    && ssh-keyscan -t rsa,dsa -H bitbucket.org >> ~/.ssh/known_hosts \
    && chmod 600 ~/.ssh/known_hosts \
    && apt-get install -y --no-install-recommends \
    apache2-dev aspell aspell-en autoconf automake autopoint autotools-dev bison bsdmainutils chrpath comerr-dev debhelper default-libmysqlclient-dev default-mysql-server \
    dh-autoreconf dh-strip-nondeterminism dh-systemd dictionaries-common emacsen-common file firebird-dev firebird3.0-common firebird3.0-common-doc flex fontconfig-config \
    fonts-dejavu-core freetds-common freetds-dev gettext gettext-base gir1.2-glib-2.0 gir1.2-harfbuzz-0.0 groff-base icu-devtools intltool-debian krb5-multidev libaio1 \
    libapparmor-dev libapparmor1 libapr1 libapr1-dev libaprutil1 libaprutil1-dev libarchive-zip-perl libargon2-0 libargon2-0-dev libaspell-dev libaspell15 libbison-dev libbsd-dev \
    libbz2-dev libc-client2007e libc-client2007e-dev libcroco3 libct4 libcurl4-openssl-dev libdb-dev libdb5.3-dev libedit-dev libelf1 libenchant-dev libenchant1c2a libevent-2.1-6 \
    libevent-core-2.1-6 libevent-dev libevent-extra-2.1-6 libevent-openssl-2.1-6 libevent-pthreads-2.1-6 libexpat1-dev libfbclient2 libfile-stripnondeterminism-perl libfontconfig1 \
    libfontconfig1-dev libfreetype6 libfreetype6-dev libgcrypt20-dev libgd-dev libgd3 libgirepository-1.0-1 libglib2.0-0 libglib2.0-bin libglib2.0-data libglib2.0-dev \
    libglib2.0-dev-bin libgmp-dev libgmp3-dev libgmpxx4ldbl libgpg-error-dev libgraphite2-3 libgraphite2-dev libgssrpc4 libharfbuzz-dev libharfbuzz-gobject0 libharfbuzz-icu0 \
    libharfbuzz0b libhunspell-1.6-0 libib-util libice-dev libice6 libicu-dev libicu-le-hb-dev libicu-le-hb0 libicu60 libiculx60 libjbig-dev libjbig0 libjpeg-dev libjpeg-turbo8 \
    libjpeg-turbo8-dev libjpeg8 libjpeg8-dev libkadm5clnt-mit11 libkadm5srv-mit11 libkdb5-9 libkrb5-dev libldap2-dev libltdl-dev libltdl7 liblzma-dev libmagic-dev libmagic-mgc \
    libmagic1 libmhash-dev libmhash2 libmpdec2 libmysqlclient-dev libmysqlclient20 libncurses5-dev libnss-myhostname libnuma1 libodbc1 libonig-dev libonig4 libpam0g-dev libpci-dev \
    libpci3 libpcre16-3 libpcre3-dev libpcre32-3 libpcrecpp0v5 libpipeline1 libpng-dev libpng16-16 libpq-dev libpq5 libpspell-dev libpthread-stubs0-dev libpython-stdlib \
    libpython2.7-minimal libpython2.7-stdlib libpython3-stdlib libpython3.6-minimal libpython3.6-stdlib libqdbm-dev libqdbm14 librecode-dev librecode0 libsasl2-dev libsctp-dev \
    libsctp1 libsensors4 libsensors4-dev libsigsegv2 libsm-dev libsm6 libsnmp-base libsnmp-dev libsnmp30 libsodium-dev libsodium23 libsqlite3-dev libssl-dev libsybdb5 libsystemd-dev \
    libtext-iconv-perl libtidy-dev libtidy5 libtiff-dev libtiff5 libtiff5-dev libtiffxx5 libtimedate-perl libtommath1 libtool libudev-dev libvpx-dev libvpx5 libwebp-dev libwebp6 \
    libwebpdemux2 libwebpmux3 libwrap0 libwrap0-dev libx11-dev libxau-dev libxcb1-dev libxdmcp-dev libxml2 libxml2-dev libxmlrpc-epi-dev libxmlrpc-epi0 libxmltok1 libxmltok1-dev \
    libxpm-dev libxpm4 libxslt1-dev libxslt1.1 libxt-dev libxt6 libzip-dev libzip4 locales-all m4 man-db mime-support mlock mysql-client-5.7 mysql-client-core-5.7 mysql-common \
    mysql-server-5.7 mysql-server-core-5.7 netcat-traditional odbcinst odbcinst1debian2 pkg-config po-debconf psmisc python python-minimal python2.7 python2.7-minimal python3 \
    python3-distutils python3-lib2to3 python3-minimal python3.6 python3.6-minimal re2c systemtap-sdt-dev tzdata ucf unixodbc-dev uuid-dev x11-common x11proto-core-dev x11proto-dev \
    xorg-sgml-doctools xtrans-dev zlib1g-dev wget unzip build-essential curl libreadline-dev \
    && rm -rf /var/lib/apt/lists/* \
    && apt-get clean

# Download and set up GitVersion
RUN set -ex \
    && wget "https://github.com/GitTools/GitVersion/releases/download/v${GITVERSION_VERSION}/GitVersion_${GITVERSION_VERSION}.zip" -O /tmp/GitVersion_${GITVERSION_VERSION}.zip \
    && mkdir -p /usr/local/GitVersion_${GITVERSION_VERSION} \
    && unzip /tmp/GitVersion_${GITVERSION_VERSION}.zip -d /usr/local/GitVersion_${GITVERSION_VERSION} \
    && rm /tmp/GitVersion_${GITVERSION_VERSION}.zip \
    && echo "mono /usr/local/GitVersion_${GITVERSION_VERSION}/GitVersion.exe \$@" >> /usr/local/bin/gitversion \
    && chmod +x /usr/local/bin/gitversion

# Install Docker
RUN set -ex \
    && curl -fSL "https://${DOCKER_BUCKET}/linux/static/${DOCKER_CHANNEL}/x86_64/docker-${DOCKER_VERSION}.tgz" -o docker.tgz \
    && echo "${DOCKER_SHA256} *docker.tgz" | sha256sum -c - \
    && tar --extract --file docker.tgz --strip-components 1  --directory /usr/local/bin/ \
    && rm docker.tgz \
    && docker -v \
# set up subuid/subgid so that "--userns-remap=default" works out-of-the-box
    && addgroup dockremap \
    && useradd -g dockremap dockremap \
    && echo 'dockremap:165536:65536' >> /etc/subuid \
    && echo 'dockremap:165536:65536' >> /etc/subgid \
    && wget "https://raw.githubusercontent.com/docker/docker/${DIND_COMMIT}/hack/dind" -O /usr/local/bin/dind \
    && curl -L https://github.com/docker/compose/releases/download/${DOCKER_COMPOSE_VERSION}/docker-compose-Linux-x86_64 > /usr/local/bin/docker-compose \
    && chmod +x /usr/local/bin/dind /usr/local/bin/docker-compose \
# Ensure docker-compose works
    && docker-compose version

# Install dependencies by all python images equivalent to buildpack-deps:jessie
# on the public repos.

RUN set -ex \
    && wget "https://bootstrap.pypa.io/2.6/get-pip.py" -O /tmp/get-pip.py \
    && python /tmp/get-pip.py \
    && pip install awscli==1.* \
    && rm -fr /var/lib/apt/lists/* /tmp/* /var/tmp/*

VOLUME /var/lib/docker

COPY dockerd-entrypoint.sh /usr/local/bin/

ENV PHP_VERSION=7.2.8 \
    PHPPATH="/usr/local/php" \
    PHP_INI_DIR="/usr/local/php/etc" \
    COMPOSER_VERSION=1.6.3 \
    COMPOSER_DOWNLOAD_SHA="52cb7bbbaee720471e3b34c8ae6db53a38f0b759c06078a80080db739e4dcab6"

ENV COMPOSER_URL="https://getcomposer.org/download/$COMPOSER_VERSION/composer.phar"

# Install PHP
RUN git clone git://github.com/php-build/php-build \
    && php-build/install.sh \
    && php-build -V \
    && php-build $PHP_VERSION $PHPPATH \
    && rm -rf php-build \

    # Increase the memory size, default is 128M
    && touch "$PHP_INI_DIR/conf.d/memory.ini" \
    && echo "memory_limit = 1G;" >> "$PHP_INI_DIR/conf.d/memory.ini"

ENV PATH="$PHPPATH/bin:/usr/local/php/bin:$PATH"

RUN php -v

# Install Composer globally
RUN set -xe; \
    wget $COMPOSER_URL; \
    echo "$COMPOSER_DOWNLOAD_SHA *composer.phar" | sha256sum -c -; \
    mv ./composer.phar /usr/local/bin/composer; \
    chmod +x /usr/local/bin/composer;

WORKDIR $PHPPATH
