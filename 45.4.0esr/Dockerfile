FROM node:6.2-slim
MAINTAINER david.enke@zalari.de
WORKDIR /tmp
# install node dependencies
RUN npm install -g \
    chai \
    chai-as-promised \
    jasmine \
    mocha \
    mocha-multi \
    mocha-proshot \
    protractor@4.0.9 \
    protractor-screenshot-reporter
RUN webdriver-manager update
RUN ln -s /usr/local/lib/node_modules/protractor/node_modules/webdriver-manager/selenium/geckodriver-v0.12.0 /usr/bin/geckodriver
ENV PATH "$PATH:/usr/bin/geckodriver"
# install marionette webdriver for firefox again
#RUN wget --no-parent https://github.com/mozilla/geckodriver/releases/download/v0.13.0/geckodriver-v0.13.0-linux64.tar.gz
#RUN tar xfz geckodriver-*.tar.gz
#RUN ln -s ./geckodriver /usr/bin/geckodriver
#ENV PATH "$PATH:/usr/bin/geckodriver"
# install dependencies
RUN apt-get update && apt-get install -y --force-yes \
    bzip2 \
    libasound-dev \
    libdbus-glib-1-dev \
    libfreetype6 \
    libfontconfig1 \
    libgtk2.0-0 \
    libxrender1 \
    libxt6 \
    libXext6 \
    libXdamage1 \
    libXfixes-dev \
    libXcomposite-dev \
    openjdk-7-jre \
    python-pip \
    xvfb
# install browser
RUN wget --no-parent https://ftp.mozilla.org/pub/firefox/releases/45.4.0esr/linux-x86_64/en-US/firefox-45.4.0esr.tar.bz2
RUN tar xfj firefox-*.tar.bz2
RUN ln -s ./firefox/firefox /usr/bin/firefox
ENV PATH "$PATH:/usr/bin/firefox"
# copy startup script
COPY ./protractor.sh /protractor.sh
# Fix for the issue with Selenium, as described here:
# https://github.com/SeleniumHQ/docker-selenium/issues/87
ENV DBUS_SESSION_BUS_ADDRESS=/dev/null
RUN mkdir /protractor
WORKDIR /protractor
ENTRYPOINT ["/protractor.sh"]
