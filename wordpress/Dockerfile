FROM wordpress:php7.1-fpm

RUN set -ex; \
	apt-get update; \
	apt-get install -y \
	ssmtp \
	libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng12-dev \
        libz-dev \
        less \
	libmagickwand-dev \
	imagemagick; \
	rm -rf /var/lib/apt/lists/*;

RUN pecl install imagick
RUN docker-php-ext-enable imagick

RUN curl https://getcomposer.org/download/$(curl -LSs https://api.github.com/repos/composer/composer/releases/latest | grep 'tag_name' | sed -e 's/.*: "//;s/".*//')/composer.phar > composer.phar \
    && chmod +x composer.phar \
    && mv composer.phar /usr/local/bin/composer \
    && curl https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar > wp-cli.phar \
    && chmod +x wp-cli.phar \
		&& mv wp-cli.phar /usr/local/bin/wp

RUN echo "mailhub=mail:1025\nUseTLS=NO\nFromLineOverride=YES" > /etc/ssmtp/ssmtp.conf
