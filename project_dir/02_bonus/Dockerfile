FROM ubuntu
MAINTAINER skholodn@student.unit.ua
# 3000 - server port, 35729 - livereload port, 443 - https port, 80 - http port, 8080 - instectors port
EXPOSE 3000 35729 443 8080 80

RUN apt-get update -q && apt-get install -y \
	curl \
	git \
	ssh \
	gcc \
	make \
	build-essential \
	libkrb5-dev \
	apt-utils \
	&& apt-get clean

# Node.js install
RUN apt-get install -y nodejs \
	&& apt-get clean

# Yarn install
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
	echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
RUN apt-get install yarn

# MEAN.JS install
RUN yarn install --quiet -g gulp bower yo mocha karma-cli pm2 && yarn cache clean

RUN mkdir -p /opt/mean.js/public/lib
WORKDIR /opt/mean.js

# Copies the local package.json file to the container
# and utilities docker container cache to not needing to rebuild
# and install node_modules/ everytime we build the docker, but only
# when the local package.json file changes.
# Install npm packages

COPY package.json /opt/mean.js/package.json
RUN yarn install --quiet && npm cache clean

# Install bower packages
COPY bower.json /opt/mean.js/bower.json
COPY .bowerrc /opt/mean.js/.bowerrc
RUN bower install --quiet --allow-root --config.interactive=false

COPY . /opt/mean.js

# Run MEAN.JS server
CMD npm install && npm start