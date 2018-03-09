FROM arm32v6/node:8-alpine
LABEL maintainer "h-mineta <h-mineta@0nyx.net>"

ENV DOCKER="YES"

RUN set -x \
	&& apk upgrade --update \
	&& apk add \
		bash \
		coreutils \
		libusb \
		curl \
		ca-certificates \
		util-linux \
        boost \
	\
	&& apk add --virtual .build-deps \
		git \
		make \
        cmake \
		gcc \
		g++ \
		gzip \
        boost-dev \
	\
	&& npm install pm2 -g \
	\
	# mirakurun
	&& npm install mirakurun@latest -g --unsafe --production \
	\
	# recfsusb2n
    && git clone https://github.com/MadPepperJP/recfsusb2n /tmp/recfsusb2n \
    && cd /tmp/recfsusb2n \
    && mkdir build \
    && cd build \
    && cmake .. \
	&& make \
	&& make install \
	\
	# cleaning
	&& cd / \
	&& npm cache verify \
	&& apk del --purge .build-deps \
	#&& rm -rf /tmp/* \
	&& rm -rf /tmp/recfsusb2n \
	&& rm -rf /var/cache/apk/* \
	
	# forward request and error logs to docker log collector
	&& ln -sf /dev/stdout /usr/local/var/log/mirakurun.stdout-0.log \
	&& ln -sf /dev/stderr /usr/local/var/log/mirakurun.stderr-0.log

COPY services.sh /usr/local/bin

WORKDIR /usr/local/lib/node_modules/mirakurun
CMD ["/usr/local/bin/services.sh"]
EXPOSE 40772
