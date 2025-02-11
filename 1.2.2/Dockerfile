FROM ubuntu:18.04

ENV DEBIAN_FRONTEND=noninteractive
ENV TERM=xterm

RUN cat /etc/issue
RUN echo "wireshark-common wireshark-common/install-setuid boolean true" | debconf-set-selections
RUN echo "tzdata tzdata/Areas select Europe" | debconf-set-selections && echo "tzdata tzdata/Zones/Europe select Paris" | debconf-set-selections
RUN apt-get update && apt-get install -y \
	apt-utils \
	vim \
	wget \
	gnupg2 \
	apt-transport-https \
	lsb-release \
	libjson-c3 \
	libmaxminddb0 \
	libmysqlclient20 \
	libpcap0.8 \
	libpq5 \
	libssl1.1 \
	libx11-6 \
	libxt6 \
	tshark \
	python3-httplib2 \
	python3-psycopg2 \
	apache2 \
	software-properties-common \
	php-common \
	recode \
	sox \
	lame \
	sqlite3 \
	libgeoip-dev \
	libndpi-dev \
	libjson-c-dev \
	&& add-apt-repository ppa:ondrej/php -y \
	&& apt-get update \
	&& apt-get install -y \
	php7.2-common \
	php7.2-cli \
	php7.2-json \
	php7.2-sqlite3 \
	php7.2-pgsql \
	php7.2-mysql \
	libapache2-mod-php7.2 \
	php7.2-json \
	php7.2-cli \
	php7.2-common \
	&& rm -rf /var/lib/apt/lists/*

COPY xplico_1.2.2_amd64.deb /tmp/

RUN dpkg -i /tmp/xplico_1.2.2_amd64.deb || apt-get install -f -y

EXPOSE 9876

CMD ["/bin/bash", "-c", "/etc/init.d/apache2 start && sleep 3 && /etc/init.d/xplico start && tail -F /var/log/apache2/*"]
