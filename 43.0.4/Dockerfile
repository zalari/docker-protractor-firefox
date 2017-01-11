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
RUN sh -c 'echo "deb http://packages.linuxmint.com debian import" >> /etc/apt/sources.list'
RUN apt-get update && apt-get install -y --force-yes \
    firefox=43.0~linuxmint1+betsy \
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
