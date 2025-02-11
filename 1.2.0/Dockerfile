FROM ubuntu:16.04

ENV DEBIAN_FRONTEND=noninteractive
ENV TERM=xterm
ENV LC_ALL=C.UTF-8
ENV LANG=C.UTF-8
ENV LANGUAGE=C.UTF-8

RUN cat /etc/issue
RUN echo "wireshark-common wireshark-common/install-setuid boolean true" | debconf-set-selections
RUN echo "tzdata tzdata/Areas select Europe" | debconf-set-selections && echo "tzdata tzdata/Zones/Europe select Paris" | debconf-set-selections
RUN apt-get update && apt-get install -y \
	apt-utils \
	software-properties-common \
	&& apt update \
	&& add-apt-repository ppa:ondrej/php -y \
	&& apt-get update \
	&& apt-get install -y \
	vim \
	php-common \
	recode \
	sox \
	lame \
	sqlite3 \
	libgeoip-dev \
	libndpi-dev \
	libjson-c-dev \
	wget \
	gnupg2 \
	apt-transport-https \
	lsb-release \
	#libmaxminddb0 \
	#libmysqlclient20 \
	libpcap0.8 \
	libpq5 \
	#libssl1.1 \
	libx11-6 \
	libxt6 \
	tshark \
	python3-httplib2 \
	python3-psycopg2 \
	apache2 \
	libssl1.0.0 \
	libjson-c2\
	libmysqlclient20\
	libapache2-mod-php\
	php-sqlite3\
	php-cli\
	php-json\
	&& rm -rf /var/lib/apt/lists/*

COPY xplico_1.2.0_amd64.deb /tmp/

RUN dpkg -i /tmp/xplico_1.2.0_amd64.deb || apt-get install -f -y

EXPOSE 9876

CMD ["/bin/bash", "-c", "/etc/init.d/apache2 start && sleep 3 && /etc/init.d/xplico start && tail -F /var/log/apache2/*"]
