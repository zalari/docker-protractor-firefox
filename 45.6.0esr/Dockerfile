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
# install dependencies
RUN apt-get update && apt-get install -y --force-yes \
    firefox-esr=45.6.0esr-1~deb8u1 \
    openjdk-7-jre \
    xvfb
# copy startup script
COPY ./protractor.sh /protractor.sh
# Fix for the issue with Selenium, as described here:
# https://github.com/SeleniumHQ/docker-selenium/issues/87
ENV DBUS_SESSION_BUS_ADDRESS=/dev/null
RUN mkdir /protractor
WORKDIR /protractor
ENTRYPOINT ["/protractor.sh"]
