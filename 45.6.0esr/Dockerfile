FROM node:slim
MAINTAINER david.enke@zalari.de
WORKDIR /tmp
RUN apt-get update && apt-get install -y --force-yes \
    bzip2 \
    libfreetype6 \
    libfontconfig1 \
    libxrender1 \
    libXext6 \
    libXdamage1 \
    libXfixes-dev \
    libXcomposite-dev \
    libasound-dev \
    libdbus-glib-1-dev \
    libgtk2.0-0 \
    libxt6 \
    python-pip \
    xvfb \
    openjdk-7-jre
# install browser
RUN wget --no-parent https://ftp.mozilla.org/pub/firefox/releases/45.6.0esr/linux-x86_64/en-US/firefox-45.6.0esr.tar.bz2
RUN tar xfj firefox-*.tar.bz2
RUN ln -s ./firefox/firefox /usr/bin/firefox
# install node dependencies
RUN npm install -g protractor protractor-screenshot-reporter mocha mocha-multi mocha-proshot chai chai-as-promised
RUN webdriver-manager update
RUN mkdir /protractor
# copy startup script
COPY ./protractor.sh /protractor.sh
# Fix for the issue with Selenium, as described here:
# https://github.com/SeleniumHQ/docker-selenium/issues/87
ENV DBUS_SESSION_BUS_ADDRESS=/dev/null
WORKDIR /protractor
ENTRYPOINT ["/protractor.sh"]
